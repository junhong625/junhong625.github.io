---
layout : post
title : '접근 제어자'
categories : [Java]
tags : [languages, java]
---

## public? static? final?

### 1. **접근 제어자** (Access Modifier)

---

- 변수나 메서드의 사용 권한 설정
    - 객체 사용자가 객체 내부적으로 사용하는 변수나 메서드에 접근함으로써 개발자가 의도하지 못한 오동작을 일으키는 것 방지
- 접근 제어자
    - `private`
    - `default`
    - `protected`
    - `public`
- `private` → `default` → `protected` → `public` 순으로 보다 많은 접근 허용

#### 1.1. **private**

- `private`이 붙은 변수, 메서드는 해당 클래스에서만 접근 가능
- 예시
    
    ```java
    public class Sample {
        private String secret;
        private String getSecret() {
            return this.secret;
        }
    }
    ```
    
    - `secret` 변수와 `getSecret` 메서드는 Sample 클래스에서만 접근이 가능하고 다른 클래스에서는 접근 불가능

#### 1.2. **default**

- 접근 제어자를 별도로 설정하지 않는다면 `default` 접근 제어자가 됨
- 해당 패키지 내에서만 접근 가능
    - 패키지: 비슷한 성격의 자바 클래스들을 모아 놓은 자바의 디렉토리 (폴더와 동일한 개념)
- 예시
    
    *house/HouseKim.java*
    
    ```java
    package house;
    
    public class HouseKim {
        String lastname = "kim";  // default 접근제어자로 설정됨
    }
    ```
    
    *house/HousePark.java*
    
    ```java
    package house;  // 동일 패키지
    
    public class HousePark {
        String lastname = "park";
    
        public static void main(String[] args) {
            HouseKim kim = new HouseKim();
            System.out.println(kim.lastname);  // kim
        }
    }
    ```
    
    - `HouseKim`과 `HousePark`의 패키지는 `house`로 동일하기 때문에 `HousePark` 클래스에서 `HouseKim`의 `lastname` 변수에 접근이 가능

#### 1.3. **protected**

- `protected`가 붙은 변수, 메서드는 동일 패키지의 클래스 또는 해당 클래스를 상속받은 다른 패키지의 클래스에서만 접근 가능
- 예시
    
    *house/HousePark.java*
    
    ```java
    package house;
    
    public class HousePark {
        protected String lastname = "park";
    }
    ```
    
    *house/person/EungYongPark.java*
    
    ```java
    package house.person;  // 다른 패키지
    
    import house.HousePark;
    
    public class EungYongPark extends HousePark {  // HousePark 상속
        public static void main(String[] args) {
            EungYongPark eyp = new EungYongPark();
            System.out.println(eyp.lastname);  // park
        }
    }
    ```
    
    - `EungYongPark` 클래스는 `HousePark` 클래스와 패키지가 다르지만 `HousePark`의 `lastname` 변수가 `protected`이기 때문에 `eyp.lastname`과 같은 접근이 가능
    - 만약 `lastname`의 접근제어자가 `protected`가 아닌 `default`였다면 `eyp.lastname` 문장은 컴파일 오류 발생

#### 1.4. **public**

- `public` 접근제어자가 붙은 변수, 메서드는 어떤 클래스에서라도 접근 가능
- 예시
    
    ```java
    package house;
    
    public class HousePark {
        protected String lastname = "park";
        public String info = "this is public message.";
    }
    ```
    
    ```java
    import house.HousePark;
    
    public class Sample {
        public static void main(String[] args) {
            HousePark housePark = new HousePark();
            System.out.println(housePark.info); // this is public message.
        }
    }
    ```
    
    - `HousePark`의 `info` 변수는 `public` 접근 제어자가 붙어 있으므로 어떤 클래스라도 접근 가능

> 위 예제들은 변수만을 대상으로 설명했지만 클래스나 메서드도 마찬가지의 접근제어자 규칙을 따름
{: .prompt-tip}


### 2. 기타 제어자

---

#### 2.1. **static**

- `static` 변수
    - `static` 키워드가 붙은 변수는 메모리 할당을 한 번만 수행 → 메모리 효율, 공유
    - 객체 생성 없이도 사용할 수 있음 (클래스가 메모리에 올라갈 때 이미 자동적으로 생성)
    - 예시: 메모리 효율
        
        ```java
        class HouseLee {
            String lastname = "이";
        }
        
        public class Sample {
            public static void main(String[] args) {
                HouseLee lee1 = new HouseLee();
                HouseLee lee2 = new HouseLee();
            }
        }
        ```
        
        - 클래스를 만들고 객체를 생성하면 객체마다 변수 `lastname`을 저장하기 위한 메모리가 별도로 할당됨
        - 하지만 항상 값이 변하지 않는 경우라면 `static` 사용하여 메모리 상의 이점 얻을 수 있음
        
        ```java
        class HouseLee {
            **static** String lastname = "이";
        }
        
        public class Sample {
            public static void main(String[] args) {
                HouseLee lee1 = new HouseLee();
                HouseLee lee2 = new HouseLee();
            }
        }
        ```
        
        - `lastname` 변수에 `static` 키워드를 붙이면 자바는 메모리 할당을 딱 한번 실행
    - 예시: 공유
        
        ```java
        class Counter  {
            int count = 0;
            Counter() {
                this.count++;
                System.out.println(this.count);
            }
        }
        
        public class Sample {
            public static void main(String[] args) {
                Counter c1 = new Counter(); // 1
                Counter c2 = new Counter(); // 1
            }
        }
        ```
        
        - `c1`, `c2` 객체 생성 시 생성자에서 객체변수인 `count`의 값을 1씩 증가하더라도 `c1`과 `c2`의 `count`는 서로 다른 메모리를 가리키고 있기 때문에 원하던 결과가 나오지 않음 (객체변수는 항상 독립적인 값을 가짐)
        
        ```java
        class Counter  {
            static int count = 0;
            Counter() {
                count++;  // count는 더이상 객체변수가 아니므로 this 제거
                System.out.println(count);  // this 제거
            }
        }
        
        public class Sample {
            public static void main(String[] args) {
                Counter c1 = new Counter(); // 1
                Counter c2 = new Counter(); // 2
            }
        }
        ```
        
        - `count` 값이 공유되어 `count`가 증가되어 출력
- `static` 메서드
    - `static` 메서드의 경우 객체 생성 없이 클래스를 통해 직접 메서드 호출 가능
    - 보통 유틸리티성 메서드에 많이 사용
    - 예시
        
        ```java
        class Counter  {
            static int count = 0;
            Counter() {
                count++;
                System.out.println(count);
            }
        
            public static int getCount() {
                return count; // 객체 변수가 아니라서 사용 가능
            }
        }
        
        public class Sample {
            public static void main(String[] args) {
                Counter c1 = new Counter();
                Counter c2 = new Counter();
        
                System.out.println(Counter.getCount());
            }
        }
        ```
        
        - 메서드 앞에 static 키워드를 붙이면 `Counter.getCount()` 와 같이 객체 생성없이 클래스를 통해 메서드를 직접 호출할 수 있음
            
            > 💡 static 메서드는 인스턴스 생성 없이 호출 가능한 반면, 인스턴스 변수는 인스턴스를 생성해야만 존재한다.
            > 
            >static이 붙은 메서드를 호출할 때 인스턴스가 생성되어 있을 수도 그렇지 않을 수도 있어서 static이 붙은 메서드에서 인스턴스 변수의 사용을 허용하지 않는다.
            > 
            > 반대로, 인스턴스 변수나 인스턴스 메서드에서는 static이 붙은 멤버들을 사용하는 것이 언제나 가능하다. 인스턴스 변수가 존재한다는 것은 static이 붙은 변수가 이미 메모리에 존재한다는 것을 의미하기 때문이다.
            {: .prompt-info}
            
    - 예시: 현재 날짜 구하기
        
        ```java
        import java.text.SimpleDateFormat;
        import java.util.Date;
        
        class Util {
            public static String getCurrentDate(String fmt) {
                SimpleDateFormat sdf = new SimpleDateFormat(fmt);
                return sdf.format(new Date());
            }
        }
        
        public class Sample {
            public static void main(String[] args) {
                System.out.println(Util.getCurrentDate("yyyyMMdd"));
            }
        }
        ```
        

##### 2.1.1. **싱글톤 패턴 (singleton pattern)**

- 하나의 클래스가 단 하나의 객체만을 생성하게 강제하는 패턴
- 예시
    
    ```java
    class Singleton {
        private Singleton() {
        }
    }
    
    public class Sample {
        public static void main(String[] args) {
            Singleton singleton = new Singleton();  // 컴파일 오류 발생
        }
    }
    ```
    
    - `Singleton` 클래스 생성자에 `private` 키워드로 다른 클래스에서의 접근을 막았기 때문에 오류 발생
    - 이렇게 생성자를 `private` 으로 만들어 버리면 다른 클래스에서 `Singleton` 클래스를 `new` 를 이용하여 생성할 수 없게 됨 → 그러면 어떻게 생성?
    
    ```java
    class Singleton {
        private Singleton() {
        }
    
        public static Singleton getInstance() {
            return new Singleton();  // 같은 클래스이므로 생성자 호출 가능
        }
    }
    
    public class Sample {
        public static void main(String[] args) {
            Singleton singleton = **Singleton.getInstance()**;
        }
    }
    ```
    
    - `getInstance`라는 `static` 메서드를 이용하여 `Singleton` 클래스의 객체를 생성할 수 있음
    - 하지만 `getInstance`를 호출할 때마다 새로운 객체 생성 → 싱글톤이 아님!
    
    ```java
    class Singleton {
        private static Singleton one;
        private Singleton() {
        }
    
        public static Singleton getInstance() {
            if(one==null) {
                one = new Singleton();
            }
            return one;
        }
    }
    
    public class Sample {
        public static void main(String[] args) {
            Singleton singleton1 = Singleton.getInstance();
            Singleton singleton2 = Singleton.getInstance();
            System.out.println(singleton1 == singleton2);  // true
        }
    }
    ```
    
    - `Singleton` 클래스에 `one` 이라는 `static` 변수를 두고 `getInstance` 메서드에서 `one` 값이 null 인 경우에만 객체를 생성하도록 하여 `one` 객체가 딱 한번만 만들어지도록 함

#### 2.2. final

- 한 번 설정되면 그 값을 바꿀 수 없음
- `final` 클래스
    
    ```java
    public final class MyFinalClass {...}  // final 클래스 선언
    public class ThisIsWrong extends MyFinalClass {...}  // 상속 불가
    ```
    
    - `final`이 붙은 클래스는 상속할 수 없음 → 보안, 효율성 장점
    - 자바에서 기본적으로 제공하는 라이브러리 클래스는 `final` 사용
- `final` 메서드
    
    ```java
    public class Base {
        public       void m1() {...}
        public final void m2() {...}  // final 메서드 선언
    }
    
    public class Derived extends Base {
        public void m1() {...}  // Base 클래스의 m1() 상속
        public void m2() {...}  // 오버라이딩 불가
    }
    ```
    
    - 클래스의 `final` 메서드는 오버라이딩으로 수정할 수 없음
- `final` 변수
    
    ```java
    public class Sphere {
    
        public static final double PI = 3.141592;
    
        public final double radius;
        public final double xPos;
        public final double yPos;
        public final double zPos;
    
        Sphere(double x, double y, double z, double r) {
            radius = r;
            xPos = x;
            yPos = y;
            zPos = z;
        }
    
        [...]
    }
    ```
    
    - `final` 변수는 한 번 값을 할당하면 수정할 수 없음 → 초기화는 한 번만 가능

---

- 참조  
    [07-02 접근제어자 (Access Modifier)](https://wikidocs.net/232)

    [07-03 스태틱(static)](https://wikidocs.net/228)

    [[Java] final 그게 뭔데, 어떻게 쓰는 건데](https://makemethink.tistory.com/184)