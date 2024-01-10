---
layout : post
title : 'String, StringBuffer, StringBuilder'
categories : [Java] 
tags : [languages, java, cs]
---

## String, StringBuffer, StringBuilder

---

> 자바에서의 문자열 클래스

**String**, **StringBuffer**, **StringBuilder** → 문자열을 저장하고 관리하는 클래스

### 왜 구분해야 되는거지?

---

연산횟수가 적다면 사실 어떤걸 써도 관계가 없다.

하지만 연산횟수가 많아지거나, 멀티쓰레드, `Race condition` 등의 상황이 자주 일어난다면?

> **Race condition**
공유 자원에 대해 여러 프로세스가 동시에 접근을 시도할 때, 타이밍이나 순서 등이 결과값에 영향을 줄 수 있는 상태
{: .prompt-info}

## String vs StringBuffer, StringBuilder

---

### String 은 불변(immutable)의 속성을 가진다.


```java
String str = "hello"; 
str = str + "world";
```

String으로 선언된 참조변수 str 은 그 값이 변하지 않는다. → 즉 메모리 값 자체가 변하지 않는다.

str 은 “hello world” 라는 값을 가지는 새로운 메모리 영역을 가리키게 되고 **→ 새로운 인스턴스 생성**

기존 “hello” 메모리는 Unreachable 의 상태가 된다. **→ GC 의 대상이 된다.**

### ※ new String(”hello”);


리터럴을 이용해 String 을 생성하는 경우 Heap 영역의 String Constant Pool 에 등록된다.

### String 언제 사용할까?


변하지 않는 문자열을 자주 읽어오는 경우

### String 언제 사용하면 안될까?


문자열의 추가, 수정, 삭제 등의 연산이 자주 일어나는 경우

→ Heap 영역에 많은 가비지가 생성되어 Heap 메모리가 부족해 질 수 있다.

### StringBuffer/StringBuilder 은 가변성을 가진다.


.append(), .delete() 등의 메서드를 이용하여 동일 객체내에서 문자열 변경이 가능

```java
StringBuffer str = new StringBuffer("hello");
str.append(" world")
```

<br>

## StringBuffer vs StringBuilder

---

### 동기화의 유무


StringBuffer → 동기화 지원 → 멀티 스레드 환경에서 안전하다.

StringBuilder → 동기화를 지원하지 않음 → 싱글 스레드에서 좋은 성능을 보인다.

> **스레드 안전(Thread-Safety)**
> 
> - 스레드 안전(Thread-Satety)란 멀티 스레드 프로그래밍에서 일반적으로 어떤 함수나 변수, 혹은 객체가 여러 스레드로부터 동시에 접근이 이루어져도 프로그램의 실행에 문제가 없는 것을 말한다.
> - 하나의 함수가 한 스레드로부터 호출되어 실행 중일 때, 다른 스레드가 그 함수를 호출하여 동시에 함께 실행되더라도 각 스레드에서의 함수의 수행 결과가 옳바르게 나오는 것을 말한다.
> 
> 즉, 두 개 이상의 스레드가 race condition에 들어가거나 같은 객체에 동시에 접근해도 연산 결과는 정합성이 보장될 수 있게 메모리 가시성이 확보된 상태
{: .prompt-info}

> **메모리 가시성**
>
>멀티 스레트 환경에서는 한 스레드가 공유자원의 값을 변경했을때 바로 다음 쓰레드가 그 변경된 값을 사용할 수 있어야 한다.
{: .prompt-tip}

<br>

---
- 참조  
    [스레드 안전(Thread-Safety)란?](https://developer-ellen.tistory.com/205)

    [[Java] 메모리 가시성(Visibility)](https://hbase.tistory.com/317)

    [[Java] String, StringBuffer, StringBuilder 차이 및 장단점](https://ifuwanna.tistory.com/221)

    [[Java] 문자열 비교하기 == , equals() 의 차이점](https://coding-factory.tistory.com/536)