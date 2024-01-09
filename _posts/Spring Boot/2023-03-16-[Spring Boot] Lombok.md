---
layout : post
title : '[Spring Boot] Lombok이란?'
subtitle : Java Library
gh-repo: junhong625/TIL
gh-badge: [star, fork, follow]
tags : [Java, Spring Boot]
comments: true
---

# Lombok이란?

Java 기반에서 작성하는 VO, DTO, Entity 관련 작업을 Lombok의 annotation들을 통해 코드를 자동완성 해주고 작업을 간소화 시켜주는 **코드 다이어터** 라이브러리입니다.

Lombok을 이용하면 `Getter`, `Setter`, `ToString`, `Equals`, `HashCode`, `Builder` 메소드들을 간편하게 사용할 수 있습니다.

Spring 프로젝트에서 JPA 환경과 함께 사용할 경우 가독성이 좋은 코드를 작성할 수 있습니다.
<br>
<br>


# Lombok 기능 및 사용 예제

## @Getter, @Setter
<br>

- `@Getter` : 클래스의 필드 값을 가져오는 Lombok의 annotation
- `@Setter` : 클래스의 필드 값을 변경하는 Lombok의 annotation

[Lombok 미사용 시]
``` java
public class person {
    private int age;
    private String name;

    public getAge() {
        return this.age;
    }
    
    public void setAge(age) {
        this.age = age;
    }
    
    public getName() {
        return this.Name;
    }

    public void setName(Name) {
        this.Name = Name;
    }
}
```
<br>

[Lombok 사용 시]
``` java
import lombok.*;

@Getter
@Setter
public class person {
    private int age;
    private String name;
} 
```

<br>

---

## @NoArgsConstructor, @AllArgsConstructor, @RequiredArgsConstructor
<br>

- `@NoArgsConstructor` : 기본 생성자 생성 annotation
- `@AllArgsConstructor` : 모든 필드 값을 사용하는 생성자를 만들어주는 annotation
- `@RequiredArgsConstructor` : 초기화 되지 않은 final 필드나 @NotNull인 필드 값만 parameter로 사용하는 생성자를 만들어주는 annotation

<br>


[Lombok 미사용 시]
``` java
@Service
public class ServiceImpl implements Service {
    
    private ServiceRepository servicerepository

    // NoArgsConstructor
    public ServiceRepository() { }

    // AllArgsConstructor
    public ServiceRepository(int age, String name) {
        this.age = age;
        this.name = name;
    }

    // RequiredConstructor
    @Autowired
    public ServiceRepository(int age, String name) {
        this.age = age;
        this.name = name;
    }
}
```
<br>

[Lombok 사용 시]
``` java
@Service
public class ServiceImpl implements Service {

    private final ServiceRepository servicerepository
}
```

<br>

---

## @EqualsAndHashCode

<br>

- `@EqualsAndHashCode` : 클래스에 대한 equals 함수와 hashCode 함수를 자동 생성해주는 annotation

<br>

[Lombok 사용 시]
``` java
public class Person {
    private int age;
    private String name;

    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;
        Student student = (Student) o;
        return studentNum == student.studentNum &&
        age == student.age &&
        Objects.equals(name, student.name);
    }

    @Override
    public int hashCode() {
        return Objects.hash(studentNum, name, age);
    }
}
```

<br>

[Lombok 미사용 시]
```java
@EqualsAndHashCode
public class Person {
    private int age;
    private String name;
}
```

<br>

---

## @ToString

<br>

- `@ToString` : 클래스의 변수들을 기반으로 ToString 메소드를 자동으로 완성시켜주는 annotation

<br>

[Lombok 미사용 시]
``` java
public class Person {
    private int age;
    private String name;

    @Override
    public String toString() {
        return "Person{" +
                "age = " + age +
                ", name = " + name +
                "}";
    }
}
```

<br>

[Lombok 사용 시]
```java
@ToString
public class Person {
    private int age;
    private String name;
}
```

<br>

---

## @Data

<br>

### `@Data` : `@Getter`, `@Setter`, `@EqualsAndHashCode`, `@ToString`, `@RequiredArgsConstructor`모든 annotation을 내포하고 있는 annotation
<br>

**주의사항**  
`@Data` 사용은 지양해야 합니다. 무분별한 `@Setter` 사용을 막아 객체의 안전성을 보장하기 위함입니다.

<br>

---

## @Builder

<br>

- `@Builder` : 객체 생성에 Builder Pattern을 적용시켜주는 annotation

<br>

[Lombok 미사용 시] (ex: 점층적 생성 패턴)
```java
public class Person {

    private int age;
    private String name;

    public Person() {}

    public Person(int age, String name) {
        this.age = age;
        this.name = name;
    }
}
```

```java
public class TestBuilderPattern {

    public static void main(String[] args) {
        Person person = new Person(28, "AJH");
    }
}
```

<br>

[Lombok 사용 시]
```java
public class Person {

    private int age;
    private String name;

    @Build
    public Person(int age, String name) {
        this.age = age;
        this.name = name;
    }
}
```
```java
public class TestBuilderPattern {

    public static void main(String[] args) {
        Person person = Person.builder()
                            .age(age)
                            .name(name)
    }
}
```
**장점**  
- 가독성
- 객체불변성
- 객체일관성 유지
@Builder를 사용해 객체를 생성 시 파라미터에 대한 입력 값을 명확히 할 수 있어 
> Builder와 관련한 자세한 설명은 [@Builder란?]()에서 이어나가도록 하겠습니다.
