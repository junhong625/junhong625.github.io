---
layout : post
title : '[Java] @NoArgsConstructor, @RequiredArgsConstructor, @AllArgsConstructor'
subtitle : '[Java] 생성자'
gh-repo: junhong625/Study
gh-badge: [star, fork, follow]
tags : [CS, Java, Study]
comments: true
---

# @NoArgsConstructor, @RequiredArgsConstructor, @AllArgsConstructor

> **Lombok 라이브러리**에서 제공하는 애너테이션으로, **생성자**를 자동으로 생성해주는 역할을 한다.
> 

# *Lombok ?*

> Java의 라이브러리로 반복되는 메소드를 Annotation을 사용해서 자동으로 작성해주는 라이브러리
> 
> 
> 코드 자체가 반복되는 메서드로 인한 복잡함을 줄여주는 역할을 수행
> 

### 사용하는 이유

- DTO, Entity의 경우 여러 속성이 존재
- 이들이 가지는 속성에 대해서 Getter나 Setter, 생성자 등을 매번 작성해줘야 하는 경우가 있음
- 이러한 부분을 자동으로 만들어줌

### 장점

- 어노테이션 기반의 코드 자동생성을 통한 생산성 향상
- 반복되는 코드를 줄여 가독성 및 유지보수성 향상
- Getter/Setter 외 빌더 패턴이나 로그생성 등 다양한 방면으로 활용 가능

---

## *생성자 ?*

> 객체를 생성하는 역할
> 
> 
> 그 과정에서 최초로 수행해야 하는 메소드를 정의하고 지정하여 초기화 작업을 수행
> 
- 주로 의존성 주입(Dependency Injection)에 사용됨
    - 의존성 주입은 객체 간의 관계를 느슨하게 결합하기 위해 사용되는 디자인 패턴
    - 코드의 유연성, 재사용성, 테스트 용이성 등을 향상시킬 수 있음
    - 자세한 내용은.. [의존성주입](https://www.notion.so/Spring-DI-8b59640da41143f6aae1df97af5f87f7?pvs=21) 을 참고해주세용

---

# 💡  Lombok에서 자주 사용되는 어노테이션

### @Getter, @Setter

> 클래스의 모든 필드에 대한 getter, setter를 간단하게 자동으로 생성
> 
> 
> 필드의 이름이 X 라면 getX(), setX() 식으로 사용
> 

```java
import lombok.Getter;
import lombok.Setter;

@Getter
@Setter
public class Car {
    private String brand;
    private String model;
    private int year;
    
    // ...
}
```

```java
Car car = new Car();
car.setBrand("Toyota");
car.setModel("Camry");
car.setYear(2022);

System.out.println(car.getBrand()); // 출력: Toyota
System.out.println(car.getModel()); // 출력: Camry
System.out.println(car.getYear());  // 출력: 2022
```

- **`@Getter`**에 의해 **`getBrand()`**, **`getModel()`**, **`getYear()`** 메서드가 자동으로 생성
    - 해당 메서드를 사용하여 필드에 접근할 수 있음
    - 이를 통해 필드 값을 읽거나 변경할 수 있음
    - **`car.getBrand()`**는 **`brand`** 필드의 값을 반환하고, **`car.setYear(2022)`**는 **`year`** 필드의 값을 변경

<aside>
💡 이렇게 자동으로 생성된 getter와 setter 메서드를 사용하면 외부에서 클래스의 필드에 접근할 때 메서드 호출을 통해 간접적으로 접근할 수 있음

</aside>

### 🚨  하지만 실전에서 Setter는 지양해야한다!

- 필드가 늘어나는 만큼 그때마다 set을 써야 됨
- 객체 하나를 만들기 위해 set 함수를 여러 번 호출해야하는데
    - 객체가 완전히 생성되기 전까지는 일관성이 무너진 상태에 놓이게 됨!
- 또 public으로 설정되어있기 때문에 어떤 곳에서든 변경이 가능해짐
    - 개인 프로젝트라면 상관이 없겠지만 현업에서 고객의 중요한 데이터가 바뀌면 대참사가 나게 됨..
    

### 따라서 **Setter 대신에 → 생성자를 사용하여 객체에 값을 지정해주는 것이 바람직!**

그런데…

```java
@Getter
class User {
  private Long id;
  private Integer age;
  private String nickname;
  private String email;
}

// 생성자
public User(Long id, Integer age, String nickname, String email){
	this.id = id;
	this.age = age;
	this.nickname = nickname;
	this.email = email;
}

// 유저 나이 변경
public void changeAge(Integer age){
	this.age = age;
}

// 생성자 단점 예시
User user = new User(1L, 25, null, null);
```

- 닉네임과 이메일 정보는 필수 정보가 아니어서 없을 땐 null로 우선 DB에 저장해줘야 한다면,
    - 나 혼자 코드를 짤 때는 ‘저 뒤에 null 2개는 닉네임과 이메일 정보고, 클라이언트로부터 넘어오지 않아서 null 처리를 한 거지’ 라고 생각하겠지만..
    - 다른 개발자들이 볼 때는 무슨 정보인지 전혀 모르는 것!!!
- 필드가 4개이지만, 10개로 늘어나게 되면, 한줄에 너무 많은 정보가 들어가서 가독성이 떨어지게 됨.
    - 개발자는 필연적으로 다른 개발자들과 협업할 수 밖에 없기에 이런 식의 코드는 좋지 않음
    - 따라서 **빌더 패턴 (Builder Pattern)**을 사용해야 함!
    

<aside>
❓ **빌더 패턴(Builder Pattern)이란?**

→ 복합 객체의 생성 과정과 표현 방법을 분리하여 **동일한 생성 절차에서 서로 다른 표현 결과를 만들 수 있게 하는 패턴**

→ `**@Builder**`사용으로, 불변성을 유지하면서 가변적인 객체를 생성할 수 있는 것!

### 장점

- ****생성자의 입력 값에 대한 순서가 바뀔 경우에 대한 오류를 줄일 수 있다.****
- ****가독성이 높은 코드를 작성할 수 있다.****
- ****변경 가능성을 최소화할 수 있다.****
- ****선택적으로 객체를 구성할 수 있습니다.****

---

이 외에 다른 패턴들 존재,,

⇒ 이 블로그를 참고해주세용

[[Java] 생성자 패턴 이해하기 : 점층적 생성자, 자바 빈즈, Builder 패턴)](https://adjh54.tistory.com/78)

</aside>

```java
@Getter
@Builder
@AllArgsConstructor
class User {
  private Long id;
  private Integer age;
  private String nickname;
  private String email;
}

public User(Long id, Integer age, String nickname, String email){
	this.id = id;
	this.age = age;
	this.nickname = nickname;
	this.email = email;
}

User user = User.builder()
			.id(1L)
			.age(25)
			.nickname(null)
			.email(null)
			.build();
```

### @Builder

> 클래스에 대한 빌더 패턴을 생성
> 
- 클래스에 @Builder 작성 → 모든 필드에 대한 빌더를 만들어줌
- 원하는 필드에 대해서만 빌더를 작성하고 싶은 경우 → 생성자를 작성하고 그 위에 @Builder 작성

```java
import lombok.Builder;
import lombok.Getter;

@Getter
@Builder
public class Person {
    private String name;
    private int age;
    
    // ...
}
```

```java
Person person = Person.builder()
                    .name("John")
                    .age(30)
                    .build();

System.out.println(person.getName());     // 출력: John
System.out.println(person.getAge());      // 출력: 30
```

- **`Person.builder()`**를 호출하여 빌더 객체를 얻은 후
- 필드 값을 설정하고 **`build()`** 메서드를 호출하여 최종적으로 **`Person`** 객체를 생성

<aside>
💡 클래스에 작성할 경우, 모든 종류의 객체를 만들 수 있다보니 원치 않는 객체를 생성할 위험이 있음

⇒  받아야 하는 **생성자를 필요조건에 따라 지정**하고 **그 위에 @Builder**를 붙이는게 바람직!

</aside>

```java
public class Member {

    @Builder
    public Member(String email, String name) {
        this.email = email;
        this.name = name;
    }
}
```

---

### @NoArgsConstructor

> ‘인자가 없는’ 생성자를 자동으로 생성
> 
> 
> 매개변수가 없는 기본 생성자를 자동으로 생성
> 

```java
public class User{
	private Long id;
	private String name;
	private String password;
	private Integer age;
}
--------------------------------
User testUser = new User(); -> 불가능! 생성자가 없기 때문에!!
```

```java
// 이런 식으로 생성자를 만들어줘야 함.

// 1.
public class User{
	private Long id;
	private String name;
	private String password;
	private Integer age;

	public User(){
	}
}
-----------------------------------

// 2.

@NoArgsConstructor
public class User{
	private Long id;
	private String name;
	private String password;
	private Integer age;
}
```

### 필요한 이유

- java의 ORM 기술인 **JPA는 기본 스펙상 기본 생성자를 요구**한다. (없으면 에러남)
- **`@NoArgsConstructor`**이 붙어있지 않은 경우도 있는데,
    - 그 이유는 **`@Entity`** 이 내부적으로 **기본 생성자**를 자동으로 만들어준다.
- 그럼에도 사용하는 이유는, **접근 권한을 제한하기 위해!**
    
    ```java
    // 예시
    
    @NoArgsConstructor(access = AccessLevel.PROTECTED)
    @Getter
    @Table( name = "abc" )
    @Entity
    public class abcd {
    ...중략
    ```
    

- ORM 기술이라는 것은 기본적으로 **영속성** 이라는 개념이 있다.
    - 간단히 말해, 데이터베이스의 실제 데이터와 그 엔티티가 일관된 상태를 유지하고 있어야한다는 것!
- 따라서 엔티티에는 **`@Setter`** 어노테이션을 붙이지 않는다!
    - 각 필드들에 대해 일관성을 유지해야하는데
    - 언제, 어느 코드에서, 누가, **`set()`** 를 여는 순간 그게 다 깨지기 때문!!
- 하지만 그럼에도 값을 넣어줘야 하므로 생성자를 쓰는 것!
    - **`@NoArgsConstructor`**를 활용해서 기본생성자를 추가하되, **접근제한을 걸어서 안전성도 높인**
    - 실제로 패턴상 안전한 방법
- **`@NoArgsConstructor(access = AccessLevel.PUBLIC)`**를 사용하면 객체 생성 시 안전성을 어느 정도 보장받을 수 있다.
    - 기본 생성자 접근을 **`protected`**으로 변경하면 외부에서 해당 생성자를 접근 할 수 없으므로 생성자를 통해서 객체를 생성 해야한다.
- **`private`**이 아닌 `**protected**`인 이유
    - JPA가 받아들일 수 있는 최대 수준의 생성자가 **`Protected`** !
    - 할 수 있는 선에서 최대한의 접근 제한을 건 것이다.
    - *참고자료*
        
        [[JPA] Entity Class의 @NoargsConstructor (access = AccessLevel.PROTECTED)](https://erjuer.tistory.com/106)
        

### @AllArgsConstructor

> ‘모든’ 인자를 가지는 생성자를 자동으로 생성
> 
> 
> 클래스에 선언된 모든 필드를 인자로 받는 생성자를 생성
> 
> 필드의 순서에 따라 인자가 생성자에 포함
> 

```java
public class User{
	private Long id;
	private String name;
	private String password;
	private Integer age;

	public User(Long id, String name, String password, Integer age){
		this.id = id;
		this.name = name;
		this.password = password;
		this.age = age;
	}
}
-----------------------------------------------------------------------

@AllArgsConstructor
public class User{
	private Long id;
	private String name;
	private String password;
	private Integer age;
}
```

### 필요한 이유

- ORM에서 중요한 건 setter를 쓰지 않고, **new()** 방식으로 객체를 생성하는 것 또한 **추천하지 않는다**.
    - 일관성이 깨질 위험이 있기 때문
- 그렇기 때문에 주로 **`@Builder`** **빌더 패턴**을 사용하게 된다.
    - 빌더 패턴은 기본적으로 **빌더 어노테이션이 적용된 전체 필드에 대한** 값을 요구하기 때문에 생성자가 반드시 필요함
    - 빌더는 해당 클래스에 생성자가 없다면 만들어주고, 생성자가 있다면 그걸 사용
    - 기존의 클래스에 `**@NoArgsConstructor**`가 있을 때엔 생성자가 있다고 판단하여,
        - 빌더는 생성자를 만들지 않고 **이미 있는 생성자에 접근**을 시도
    - 그런데 여기서 **Protected**로 막혀있어서 접근을 거절당하고 결국 **에러**를 띄우게 된다!
    - 결국 빌더 패턴에서 요구하는 생성자는 **전체 필드에 대한 생성자**

### 그런데…

- **`@AllArgsConstructor`**만 적용한 경우엔 기본 생성자가 만들어지지 않는 문제가 생겨버리게 됨
- **`@Entity`**는 생성자를 추가하는 코드를 쓰지 않아도 **자동으로 기본생성자**는 만들어주지만,
    - 이미 생성자가 있을 경우에는 **만들지 않는다!**

따라서

```java
@AllArgsConstructor
@NoArgsConstructor
@Getter
@Entity
public class User {
...중략
```

이런 식으로 함께 작성하면,

- **`@AllArgsConstructor`** 로 생성자를 넣어줌으로써 빌더 패턴을 챙길 수 있고
- **`@AllArgsConstructor`** 때문에 자동생성 되지 않은 기본 생성자를 `**@NoArgsConstructor**` 로 직접 추가하여 사용할 수 있다.

### @RequiredArgsConstructor

> ‘필수’ 인자를 가지는 생성자를 자동으로 생성
> 
> 
> 해당 클래스의 final 필드나 **`@NonNull`** 애너테이션이 붙은 필드에 대한 생성자를 생성
> 
> 다른 필드는 생성자에 포함되지 않음
> 

```java
@RequiredArgsConstructor
public class User{
	@NonNull
	private Long id;
	private String name;
	private String password;
	@NonNull
	private Integer age;
}
```

```java
// 이런 생성자를 만들어줌!
public User(Long id, Integer age){
	this.id = id;
	this.age = age;
}
```

```java
User testUser = new User(이기태, 25); -> 가능!
```

### 필요에 따라 어노테이션을 함께 사용!

<aside>
💡 **객체 생성 시 반드시 생성되어야 하는 것들에 대한 안전성을 높이는 시각을 갖는 것이 중요 !**

**클린 코드, 유지보수 하기 좋은 코드는 이런 사소한 객체 생성부터 생각해보는 것이 많은 도움이 됨 !**

</aside>

---

- **참고자료**