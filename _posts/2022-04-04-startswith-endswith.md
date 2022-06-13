---
layout : post
title : '[Python]startswith, endswith 사용법'
subtitle : startswith, endswith
gh-repo: junhong625/Algorithm
gh-badge: [star, fork, follow]
tags : [Python]
comments: true
---
  
startswith, endswith는 [Programmers[전화번호 목록]](https://junhong625.github.io/2022-04-04-Programmers-%EC%A0%84%ED%99%94%EB%B2%88%ED%98%B8%EB%AA%A9%EB%A1%9D/)문제를 풀고나서 다른 사람들의 풀이를 보며 공부하다 알게 된 함수로 유용하게 사용할 수 있을 것 같아 공부하고 해당 내용을 기록하기 위해 한 포스팅입니다.

* * *
startswith, endswith는 호출하지 않아도 되며 사용하기 쉽고 접두어 관련한 문제에 간편하게 사용할 수 있는 함수입니다.
```python
str1.startswith(str2, beg=0, end=len(string))
str1.endswith(str2, beg=0, end=len(string)) 
```
str1 : 비교대상 문자열(문자)
str2 : 찾고자 하는 문자열(문자)
beg : 검색 시작 위치를 설정하는 인덱스 값
end : 검색 끝 위치를 설정하는 인덱스 값
  
위와 같은 형식으로 사용하며
str1이 str2로 시작하거나 끝나면 True를 반환하고 그렇지 않으면 False를 반홥합니다.

- 유의할 점 - str1과 str2 모두 (str)형식이여야 한다.  

## 예시

> startswith함수를 사용했을 때 True를 반환하는 예

```python
str1 = "Apple's color is red!"

print(str1.startswith("App"))
print(str1.startswith("color", 8))
print(str1.startswith("Apple's", 0, 7)) # 마지막 문자열이 위치한 인덱스 값의 +1을 더한 값을 end파라미터에 집어넣어야 올바르게 작동  
```

> endswith함수를 사용했을 때 True를 반환하는 예

```python
str1 = "Banana's color is yellow!"

print(str1.endswith("yellow"))
print(str1.endswith("color", 0, 14))
print(str1.endswith("is", 0, -8)) # -8을 집어넣으면 인덱스 -8 값과 똑같이 작동하기에 True값이 반환 됨
```

> startswith, endswith함수를 사용했을 때 False를 반환하는 예

```python
str1 = "Sky's color is skyblue!"

print(str1.startswith("app")) # 대소문자가 틀린 경우
print(str1.endswith("skyblue!", -2)) # 시작 위치가 틀린 경우
print(str1.startswith("Apple's", 0, 3)) # 시작 위치는 맞으나 검색 끝 위치가 틀린 경우
```

위 예시와 같이 대소문자, 시작 위치, 끝 위치 틀리는 것만 유의한다면 유용하게 사용할 수 있을 것으로 생각됩니다.
