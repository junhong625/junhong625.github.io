---
layout : post
title : '[Spring Boot] MultipartFile Unsupported Media Type 에러'
subtitle : Spring Boot Error
gh-repo: junhong625/TIL
gh-badge: [star, fork, follow]
tags : [Spring Boot]
comments: true
---

# MultipartFile Unsupported Media Type 에러

![](https://user-images.githubusercontent.com/83000975/226265525-26880224-d4db-42b8-b7f0-76020f817b66.png)

<br>

[예시 코드]
```java
public void create(@RequestBody PersonalDataRequestDto personalDataRequestDto){
        personalDataService.save(personalDataRequestDto);
    }
```

위 이미지와 같이 PostMan에서 POST 요청으로 `MultipartFile`을 전송을 할 때 예시 코드와 같이 메소드에서 `@RequestBody`로 받으면   `Unsupported Media Type`에러가 발생하게 됩니다.

<br>

## 에러 발생 이유
`@RequestBody` annotation은 JSON으로 들어오는 데이터를 parsing 해주는 것이기 때문입니다. 그렇기에 이미지는 JSON으로 변경할 수 없어 오류가 발생하게 됩니다. 이에 대한 해결책으로 이미지를 base64 인코딩을 한 후 데이터들과 함께 전달하는 방법이 있지만 이보다 더 간단한 해결 방법이 있습니다.

<br>

## 해결책
`@RequestBody`대신 `@ModelAttribute`를 사용하면 간단하게 해결됩니다.  
```java
public void create(@ModelAttribute PersonalDataRequestDto personalDataRequestDto){
        personalDataService.save(personalDataRequestDto);
    }
```

`@ModelAttribute`는 클라이언트로부터 일반 HTTP 요청 파라미터나 multipart/form-data 형태의 parameter를 객체로 받아 사용하고 싶을 때 사용하는 annotation으로 이미지를 전송하고 싶을 때 적합한 annotation입니다.
