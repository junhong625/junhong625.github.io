---
layout : post
title : Programmers[SQL] SUM, MAX, MIN
subtitle : SQL 고득점 Kit
gh-repo: junhong625/SQL
gh-badge: [star, fork, follow]
tags : [SQL]
comments: true
---
# Programmers SQL 고득점 Kit

## SUM, MAX, MIN 문제
<br>

### 1. 최댓값 구하기
**문제 풀이**
> `가장 최근에 들어온 동물은 언제 들어왔는지 조회`하는 SQL 문을 작성해주세요.

- `가장 최근에 들어온 동물은 언제 들어왔는지 조회` : **ORDER BY () DESC**를 이용하여 역순으로 정렬 후 **LIMIT 1**을 통해 가장 먼저 나오는 하나의 데이터만 조회

**정답**
```
SELECT DATETIME AS "시간" FROM ANIMAL_INS 
ORDER BY DATETIME DESC 
LIMIT 1;
```
<br>

### 2. 최솟값 구하기
**문제 풀이**
> 동물 보호소에 `가장 먼저 들어온 동물은 언제 들어왔는지 조회`하는 SQL 문을 작성해주세요.

- `가장 먼저 들어온 동물은 언제 들어왔는지 조회` : **ORDER BY**를 이용하여 정렬 후 **LIMIT 1**을 통해 가장 먼저 나오는 하나의 데이터만 조회

**정답**
```
SELECT DATETIME AS "시간" 
FROM ANIMAL_INS 
ORDER BY DATETIME ASC 
LIMIT 1;
```
<br>

### 3. 동물 수 구하기
**문제 풀이**
> 동물 보호소에 동물이 `몇 마리 들어왔는지 조회`하는 SQL 문을 작성해주세요.

- `몇 마리 들어왔는지 조회` : **COUNT**함수를 이용하여 동물의 수 조회

**정답**
```
SELECT COUNT(*) 
FROM ANIMAL_INS;
```
<br>

### 4. 중복 제거하기
**문제 풀이**
> 동물 보호소에 들어온 `동물의 이름은 몇 개인지 조회`하는 SQL 문을 작성해주세요. 이때 `이름이 NULL인 경우는 집계하지 않으며` `중복되는 이름은 하나로 칩니다.`

- `동물의 이름은 몇 개인지 조회` : **COUNT**함수를 이용하여 이름 개수 조회
- `이름이 NULL인 경우는 집계하지 않으며` : **WHERE**과 **is not**을 이용
- `중복되는 이름은 하나로 칩니다.` : **DISTINCT**를 이용하여 중복 제거

**정답**
```
SELECT COUNT(DISTINCT NAME) 
FROM ANIMAL_INS 
WHERE NAME IS NOT NULL;
```
