---
layout : post
title : Programmers[SQL]
subtitle : SQL 문제
gh-repo: junhong625/SQL
gh-badge: [star, fork, follow]
tags : [SQL]
comments: true
---
# Programmers SQL 고득점 Kit

### SELECT 문제
#### 1. 모든 레코드 조회하기
**문제 풀이**
> 동물 보호소에 들어온 `모든 동물의 정보`를 `ANIMAL_ID순으로 조회`하는 SQL문을 작성해주세요. 

- `모든 동물의 정보` : __*__을 이용하여 모든 정보를 조회
- `ANIMAL_ID순으로 조회` : **ORDER BY**를 이용하여 정렬

**정답**
```
SELECT * FROM ANIMAL_INS ORDER BY ANIMAL_ID ASC;
```

#### 2. 역순 정렬하기
**문제 풀이**
> 동물 보호소에 들어온 `모든 동물의 이름`과 `보호 시작일을 조회`하는 SQL문을 작성해주세요. 이때 결과는 `ANIMAL_ID 역순`으로 보여주세요.

- `모든 동물의 이름`과 `보호 시작일을 조회` : **SELECT NAME, DATETIME**으로 조회
- `ANIMAL_ID 역순` : **DESC**를 이용하여 역순으로 조회

#### 3. 아픈 동물 찾기