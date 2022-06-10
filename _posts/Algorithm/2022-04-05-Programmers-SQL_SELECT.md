---
layout : post
title : Programmers[SQL] SELECT
subtitle : SQL 고득점 Kit
gh-repo: junhong625/SQL
gh-badge: [star, fork, follow]
tags : [SQL]
comments: true
---
# Programmers SQL 고득점 Kit

## SELECT 문제
<br>

### 1. 모든 레코드 조회하기
**문제 풀이**
> 동물 보호소에 들어온 `모든 동물의 정보`를 `ANIMAL_ID순으로 조회`하는 SQL문을 작성해주세요. 

- `모든 동물의 정보` : __*__을 이용하여 모든 정보를 조회
- `ANIMAL_ID순으로 조회` : **ORDER BY**를 이용하여 정렬

**정답**
```
SELECT * 
FROM ANIMAL_INS 
ORDER BY ANIMAL_ID ASC;
```
<br>

### 2. 역순 정렬하기
**문제 풀이**
> 동물 보호소에 들어온 `모든 동물의 이름과 보호 시작일을 조회`하는 SQL문을 작성해주세요. 이때 결과는 `ANIMAL_ID 역순`으로 보여주세요.

- `모든 동물의 이름과 보호 시작일을 조회` : **NAME, DATETIME**으로 **SELECT**
- `ANIMAL_ID 역순` : **ORDER BY () DESC**를 이용하여 역순으로 조회

**정답**
```
SELECT NAME, DATETIME 
FROM ANIMAL_INS
ORDER BY ANIMAL_ID DESC;
```
<br>

### 3. 아픈 동물 찾기
**문제 풀이**
> 동물 보호소에 들어온 동물 중 `아픈 동물의 아이디와 이름을 조회`하는 SQL 문을 작성해주세요. 이때 결과는 `아이디 순`으로 조회해주세요.

- `아픈 동물의 아이디와 이름을 조회` : **ANIMAL_ID, NAME**으로 **SELECT**후  **WHERE**을 이용하여 조건을 설정 
- `아이디 순` : **ORDER BY**를 이용하여 정렬

**정답**
```
SELECT ANIMAL_ID, NAME 
FROM ANIMAL_INS
WHERE INTAKE_CONDITION = "Sick" 
ORDER BY ANIMAL_ID ASC;
```
<br>

### 4. 어린 동물 찾기
**문제 풀이**
> 동물 보호소에 들어온 동물 중 `젊은 동물의 아이디와 이름을 조회`하는 SQL 문을 작성해주세요. 이때 결과는 `아이디 순`으로 조회해주세요.

- `젊은 동물의 아이디와 이름을 조회` : **WHERE**를 이용하여 조건을 설정 
- `아이디 순` : **ORDER BY**를 이용하여 정렬

**정답**
```
SELECT ANIMAL_ID, NAME 
FROM ANIMAL_INS
WHERE INTAKE_CONDITION != "Aged"
ORDER BY ANIMAL_ID ASC;
```
<br>

### 5. 동물의 아이디와 이름
**문제 풀이**
> 동물 보호소에 들어온 `모든 동물의 아이디와 이름`을 `ANIMAL_ID순으로 조회`하는 SQL문을 작성해주세요.

- `모든 동물의 아이디와 이름` : **ANIMAL_ID, NAME**로 **SELECT**
- `ANIMAL_ID순으로 조회` : **ORDER BY**를 이용하여 정렬

**정답**
```
SELECT ANIMAL_ID, NAME 
FROM ANIMAL_INS
ORDER BY ANIMAL_ID ASC;
```
<br>

### 6. 여러 기준으로 정렬하기
**문제 풀이**
> 동물 보호소에 들어온 `모든 동물의 아이디와 이름, 보호 시작일`을 `이름 순으로 조회`하는 SQL문을 작성해주세요. 단, `이름이 같은 동물 중에서는 보호를 나중에 시작한 동물을 먼저 보여줘야 합니다.`

- `모든 동물의 아이디와 이름, 보호 시작일` : **ANIMAL_ID, NAME**로 **SELECT**
- `이름 순으로 조회` : **ORDER BY**로 정렬 
- `이름이 같은 동물 중에서는 보호를 나중에 시작한 동물을 먼저 보여줘야 합니다.` : **ORDER BY NAME ASC**뒤에 또 다시 정렬할 COLUMN을 세팅

**정답**
```
SELECT ANIMAL_ID, NAME, DATETIME 
FROM ANIMAL_INS
ORDER BY NAME ASC, DATETIME DESC;
```
<br>

### 7. 상위 n개 레코드
**문제 풀이**
> 동물 보호소에 `가장 먼저 들어온 동물의 이름을 조회`하는 SQL 문을 작성해주세요.

- `가장 먼저 들어온 동물의 이름을 조회` : **ORDER BY DATETIME**으로 오름차순 정렬 후 **LIMIT 1**으로 가장 먼저 먼저 들어온 동물의 데이터만 출력

**정답**
```
SELECT NAME 
FROM ANIMAL_INS
ORDER BY DATETIME ASC
LIMIT 1;
```
