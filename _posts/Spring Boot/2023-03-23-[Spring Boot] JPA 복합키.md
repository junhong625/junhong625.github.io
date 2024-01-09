---
layout : post
title : '[Spring Boot] JPA 복합키 사용법'
subtitle : Spring Boot JPA
gh-repo: junhong625/TIL
gh-badge: [star, fork, follow]
tags : [Spring Boot]
comments: true
---

# JPA 복합키 사용법

보편적으로 entity에는 하나의 기본키가 설정이 됩니다.
하지만 테이블의 키가 복합키로 이뤄져 있다면 entity 설계 시 이를 고려해야합니다.
Spring Boot JPA 에서는 두 가지 방법으로 복합키 사용을 지원합니다.

<br>

###  1. @IdClass
###  2. @Embeddedable & @EmbeddedId

<br>

### [하나의 PK를 사용하는 entity]
``` java
@Entity
@Table(name = "chat_image")
public class ChatImage {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    @Column(name = "id")
    private Long id;

    @ManyToOne
    @JoinColumn(name = "missing_id")
    private PersonalData personalData;

    @ManyToOne
    @JoinColumn(name = "user_id")
    private User user;

    @Cloumn(name = "image_path")
    private String imagePath;
}
```  

<br>

## @IdClass
> DB 방식에 가까운 복합키 설계 방식

<br>

### 생성 규칙
- 식별자 클래스의 필드명과 엔티티의 필드명이 동일해야 합니다. 
- **Serializable** 인터페이스를 구현해야합니다.
- **equals()**, **hashCode()**를 구현해야 합니다.
- 기본 생성자를 선언해야 합니다.
- 클래스의 접근제한자는 **public**이어야 합니다.

<br>

> 위 규칙을 지키며 복합키를 생성해보겠습니다.
```java
@Data
public class ChatImageId implements Serializable {
    private Long userId;
    private Long missingId;
}
```

```java
@Entity
@IdClass(ChatImageId.class)
public class ChatImage {
    @ManyToOne
    @JoinColumn(name = "user_id")
    private User user;

    @ManyToOne
    @JoinColumn(name = "missing_id")
    private PersonalData personalData;

    @Column(name = "image_path")
    private String imagePath;
}
```

<br>

## @EmbeddedId
> 객체 방식에 가까운 복합키 설계 방식

<br>

### 생성 규칙
- 식별자 클래스에 `@Embeddable`을 사용해야 합니다.
- **Serializable** 인터페이스를 구현해야 합니다.
- **equals()**, **hashCode()**를 구현해야 합니다.
- 기본 생성자를 선언해야 합니다.
- 클래스의 접근제한자는 **public**이어야 합니다.

<br>

> 위 규칙을 지키며 설계 해보겠습니다.
```java
@Embeddable
@Data
public class ChatImageId implements Serializable {
    @ManyToOne
    @JoinColumn(name = "user_id")
    private User user;

    @ManyToOne
    @JoinColumn(name = "missing_id")
    private PersonalData personalData;
}
```
```java
@Entity
@Data
public class ChatImage {

    @EmbeddedId
    private ChatImageId chatImageId;

    @Column(name = "image_path")
    private String imagePath;
```
