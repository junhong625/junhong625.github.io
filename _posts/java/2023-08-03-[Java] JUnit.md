---
layout : post
title : 'JUnit'
categories : [Java] 
tags : [languages, java, cs]
---

## TDD

> 테스트 주도 개발 (Test Driven Development)
> 
- 테스트를 먼저 설계 및 구축 후 테스트를 통과할 수 있는 코드를 짜는 것
- 선 테스트 코드 작성 후 실제 코드 개발
- 애자일 개발 방식 중 하나
    - 짧은 개발 주기의 반복에 의존하는 개발 프로세스
{: .prompt-info}
    

### TDD 개발 주기

1. **`Red`**: 실패하는 테스트 코드를 먼저 작성한다.
    - edge case, failure case 위주로 작성
2. **`Green`**: 테스트 코드를 성공시키기 위한 실제 코드를 작성한다.
    - Testing이 fully passed 될 때까지 기능을 작성
3. **`Blue`**: 중복 코드 제거, 일반화 등의 리팩토링을 수행한다.

> **중요한 점**
> 
> 1. 실패하는 테스트 코드를 작성할 때까지 실제 코드를 작성하지 않는 것
> 2. 실패하는 테스트를 통과할 정도의 최소한의 실제 코드를 작성해야 하는 것
>
> → 실제 코드에 기대되는 바를 보다 명확하게 정의함으로써 **불필요한 설계를 피할 수 있음 !**
{: .prompt-tip}

### TDD의 장점

1. 설계에 대한 피드백이 빠르고 재설계 시간을 단축
    - 테스트 코드를 먼저 작성하기 때문에 지금 무엇을 해야하는지 분명히 정의하고 개발을 시작하게 됨
    - 요구사항에 맞춰 개발 코드를 구현 하므로 불필요한 구현을 방지
    - 개발 진행 중 전반적인 설계가 변경되는 것을 방지
2. 디버깅 시간의 단축
    - 기능을 작성한 후에 뒤늦게 side effect를 발견하는 경우가 생김
    - 테스트 시나리오를 작성하면서 다양한 예외사항을 생각해볼 수 있음
        - ex) 빈 문자열이나 빈 리스트가 들어왔을 경우에 대한 test case를 작성하여 실제 기능 개발 단계에서의 오작동을 막을 수 있음
3. 코드의 모듈화
    - 함수 또는 메서드나 클래스를 작성하기 전에 테스트를 작성하다보면,
        - test case를 작성하기 어렵거나
        - test case의 크기가 커지거나
        - test case의 가독성이 떨어지면
            
            ⇒ 기능의 설계가 잘못된 것!
            
            ⇒ 적당한 수준의 추상화나 모듈화가 이뤄지지 않았음을 의미함
            
    - 특히 함수의 경우 **단일 책임 원칙**이 지켜지지 않고, 하나의 함수가 많은 기능을 하고 있을 수도 있음
        
        > **단일 책임 원칙 (Single Responsibility principle)**
        >
        > 하나의 객체는 반드시 하나의 기능만을 수행하는 책임을 가져야하는 원칙
        > 
        > = 클래스를 변경하는 이유는 오직 하나뿐이어야 한다!
        > 
        > (객체지향 5대 원칙 SOLID 중 하나)
        {: .prompt-info}
        
    - 작은 단위로 테스트를 작성하기 때문에 자연스럽게 적절한 수준의 모듈화가 이뤄질 수 있음
4. 자동으로 높아지는 테스트 커버리지
    - 테스트 코드를 먼저 작성하니까 자연스레 테스트 커버리지가 높아짐
    
    > **테스트 커버리지 (Test Coverage)**
    > 
    > 코드가 얼만큼 테스트되고 있는지 나타내는 소프트웨어의 품질 지표
    > → 테스트 커버리지가 높은 소프트웨어는 버그 발생 확률이 적기 때문에 사용자가 더욱 신뢰하고 사용할 수 있음!
    {: .prompt-info}
    

---

## JUnit

> 자바 프로그램의 단위 테스트를 위한 대표적인 프레임 워크
> 
- 어노테이션을 제공하여 쉽고 간결하게 테스트 코드를 작성하여 실행이 가능
- JUnit 5 - Java 8 이상 요구됨
- **`@Test`** 메서드가 호출될 때마다 새로운 인스턴스를 생성하여 독립적 테스트를 수행
    - @Test : 단위 테스트 메서드임을 나타냄
- **`assertXXX`** 메서드로 테스트 케이스의 수행 결과를 판단
- 특정 조건에 따라 테스트를 실행할 수 있음
- 테스트를 그룹화 할 수 있음 (모듈별, 단위/통합 구분, 기타 조건)
{: .prompt-info}

### JUnit 5의 모듈 구성

1. JUnit Platform : 테스트를 실행해주는 런처와 TestEngine API 제공
    1. 테스트를 발견하고 테스트 계획을 생성하는 TestEngine 인터페이스를 가지고 있음
    2. TestEngine을 통해서 테스트를 발견하고 실행하여 결과를 보고함
2. JUnit Jupiter : JUnit 5를 위한 테스트 API와 실행 엔진을 제공
    1. TestEngine의 실제 구현체는 별도 모듈이며, 그 중 하나가 jupiter-engine
    2. jupiter-api를 사용해서 작성한 테스트 코드를 발견하고 실행
    3. JUnit 5에 새롭게 추가된 테스트 코드용 API로서, 개발자는 Jupiter API를 사용해서 테스트 코드 작성
3. JUnit Vintage : 하위 호완성을 위해 JUnit 3 또는 4로 작성된 테스트를 JUnit 5 플랫폼에서 실행하기 위한 모듈을 제공

### JUnit 5가 제공하는 어노테이션

#### @Test

- 해당 어노테이션이 선언된 메서드는 테스트를 수행하는 메서드가 됨 (단위 테스트 선언)
- @Test(timeout=6000) : 단위는 millisecond로, 해당 시간을 넘기면 실패
- @Test(expected=NullPointerException) : NullPointerException이 발생하면 통과

#### @Disabled

- 해당 어노테이션이 붙은 메서드는 테스트를 실행하지 않음

#### @BeforeEach

- 테스트 메소드가 실행되기 전에 먼저 실행할 메서드를 지정
- @Test 메소드가 실행 될 때마다 객체를 생성하여 실행
- 주로 @Test 메서드에서 공통으로 사용하는 코드를 @Before 메서드에 선언하여 사용

#### @AfterEach

- 테스트 메소드가 실행된 후에 실행할 메서드를 지정
- @Test 메소드가 실행 될 때마다 객체를 생성하여 실행
- 주로 동일한 마무리 작업을 수행할 경우에 사용

#### @BeforeAll

- @Test 메소드보다 먼저 한번만 수행되어야 할 경우에 사용
- 모든 테스트 메소드가 동작하기 전 공통적으로 실행해야 하는 작업 수행
- @BeforeEach와 차이점은 한번만 실행되고 static으로 선언한 메서드여야 하는 것

#### @AfterAll

- @Test 메소드보다 나중에 한번만 수행되어야 할 경우에 사용
- 모든 테스트 메소드가 실행되고 난 후에 한번 실행하는 메소드
- @AfterEach와 차이점은 한번만 실행되고 static으로 선언한 메서드여야 하는 것

### 테스트 메서드의 구성

- 준비 → 동작 → 확인 과정으로 진행
    - 준비: Arrange, 테스트를 수행하기 위한 테스트 환경 조성 부분
        - 테스트 대상 클래스의 객체 생성
        - 필요할 경우 특정 상태가 되도록 유도
    - 동작: Act, 실제 테스트 대상 기능 실행
    - 확인: Assert, 동작의 실제 실행 결과와 기대 결과를 비교하여 확인
        - Assertion 구문 사용

```java
public class SomeTest{
	
    //합계테스트 / 유닛테스트1
	  @Test
    public void testSum(){
	    	int result = 0; -> "준비"
        
        Something some = new Somthing(); -> "준비"
        result = som.sum(10); -> "동작"
        assertEquals(55, result); -> "확인"
        
    //정렬테스트 / 유닛테스트2
    @Test
    public void testSort(){
	    	int[] a = {44, 33, 66, 22, 55, 11}; -> "준비"
        int[] b = {11, 22, 33, 44, 55, 66}; -> "준비"
        
        Somthing some = new Somthing(); -> "준비"
        some.bubble_sort(a); -> "동작"
        assertArrayEquals(b, a); -> "확인"
    }
    
}
```

#### Assertion 구문

- 어떤 연산의 결과와 예상한 결과를 비교하여 확인을 수행하는 동작
- **org.junit.jupiter.api.Assertions** 에서 검증을 위한 다양한 메서드 제공
    - **assertEquals(expected, actual)**
        - 기대한 값(expected)이 실제 값(actual)과 같은지 확인하는 메서드
        - 세번째 파라미터로 메시지를 줄 수 있는데, 이때 람다를 사용하면 실패한 경우에만 해당 메시지를 만들 수 있음
    - **assertNotNull(actual)**
        - 결과 값(actual)이 null 인지 아닌지 확인하는 메서드
    - **assertTrue(boolean)**
        - 다음 조건이 참인지 확인하는 메서드
    - **assertAll(executable...)**
        - 모든 구문 확인 메서드
            
            ```java
            @DisplayName("스터디 만들기 ")
            @Test
            void create_new_study() {
                Study study = new Study();
                assertNotNull(study);
            
                assertAll(
                        ()->assertEquals(StudyStatus.DRAFT, study.getStatus(),()-> "스터디를 처음 만들면 DRAFT 상태다. "),
                        ()->assertTrue(study.getLimit() > 0, ()-> "스터디 최대 참석 가능 인원은 0명 이상이어야 한다. ")
                );
            }
            ```
            
    - **assertThrows(expectedType, executable)**
        - 예외 발생 확인 메서드
        - 예외 검증 후 해당 예외를 반환해주기에 예외 메시지 검증이 가능
            
            ```java
            @DisplayName("스터디 만들기 ")
            @Test
            void create_new_study() {
                IllegalArgumentException exception = assertThrows(IllegalArgumentException.class, () -> new Study(-1));
                assertEquals(exception.getMessage(), "limit 은 0보다 커야한다.");
            }
            ```
            
    - **assertTimeout(duration, executable)**
        - 특정 시간 내에 실행 완료되는지 확인하는 메서드
    

#### 조건에 따라 테스트 실행

- 특정 OS, 환경 변수, 시스템 변수에 따라 테스트 실행 결정 가능
- **org.junit.jupiter.api.Assumptions.*** 에서 메서드 제공
    - `assumeTrue(condition)`
        - 해당 조건이 통과해야 아래 로직을 수행
    - `assumingThat(condition, test)`
        - 조건(condition)이 통과하면 두 번째 파라미터로 전달한 로직 수행
- 어노테이션으로 조건 설정 가능
    - **@EnabledOnOs**
        - 특정 OS일 때만 테스트가 동작하게 할 수도 있다.
        - @EnabledOnOs(OS.MAC)
    - **@EnabledOnJre**
        - 특정 JRE버전일 때만 테스트가 동작하게 할 수도 있다.
        - @EnabledOnJre({JRE.JAVA_8, JRE.JAVA_9, JRE.JAVA_10, JRE.JAVA_11})
    - **@EnabledIfEnvironmentVariable**
        - 위에서 사용한 assumeXX 메서드는 해당 어노테이션을 통해 환경 변수 조건 설정이 가능하다.
        - @EnabledIfEnvironmentVariable(named = "TEST_ENV", matches = "local")
        

#### 반복해서 테스트를 실행해야 할 때,

- 인자가 랜덤 값이거나 테스트 발생 시점에 따라 달라지는 값 때문에 테스트 내용이 반복돼야 하는 경우
    - 어노테이션으로 테스트 반복 설정 가능

##### **@RepeatedTest**

- 속성을 통해 반복 횟수와 반복 테스트 이름 설정 가능

##### @**ParameterizedTest**

- 테스트에 여러 다른 매개변수를 대입해가며 반복 실행 가능
- 테스트할 인자 값을 어노테이션으로 지정하여 테스트 반복 가능
    - **@CsvSource** : 속성에 여러 인자를 콤마(,)로 구분하여 메서드에 파라미터로 넘겨줌
    - **@ValueSource** : 단일 값을 제공하는 경우에 사용
    - **@MethodSource** : 특정 메서드를 호출하여 값을 가져오는 경우에 사용
    - **@EnumSource** :  Enum의 값을 제공해 주는 어노테이션

### 테스트 그룹화

#### @Tag

- 테스트를 그룹화 할 수 있음
    
    ```java
    import org.junit.jupiter.api.Tag;
    import org.junit.jupiter.api.Test;
    
    @Tag("fast")
    public class TagExample {
    
        @Test
        @Tag("math")
        void testAddition() {
            // 테스트 로직
        }
    
        @Test
        @Tag("math")
        @Tag("advanced")
        void testAdvancedMath() {
            // 테스트 로직
        }
    
        @Test
        @Tag("slow")
        void testSlowOperation() {
            // 테스트 로직
        }
    }
    ```
    
- 태그 필터링
    - 원하는 테스트만 실행하거나 제외할 수 있음
    - Maven, Gradle 또는 JUnit Platform Console Launcher를 사용하여 가능
    - **`--include-tags`** 또는 **`--exclude-tags`** 옵션을 사용하여 원하는 태그가 포함된 테스트를 실행하거나, 원하지 않는 태그가 포함된 테스트를 제외하여 실행
    
    ```bash
    # JUnit Platform Console Launcher를 사용하는 방법
    
    # 특정 태그가 포함된 테스트 실행
    java -jar junit-platform-console-standalone.jar --include-tags=fast,math
    
    # 특정 태그가 포함되지 않은 테스트 실행
    java -jar junit-platform-console-standalone.jar --exclude-tags=slow
    ```

<br>

---

- 참고자료
    
    [TDD 해보기](https://wiki.lucashan.space/programming/TDD/03.let-it-tdd/#1-tdd의-절차)
    
    [[Java] JUnit을 이용한 TDD 간단 체험하기(진짜 간단함 주의)](https://makemethink.tistory.com/155)
    
    [[Java] TDD 어떻게 하는가?](https://velog.io/@jkijki12/Java-TDD)
    
    [Spring Framework로 하는 TDD 감 익히기](https://show400035.tistory.com/165)
    
    [[Test] JUnit5](https://velog.io/@daydream/Test-JUnit5)