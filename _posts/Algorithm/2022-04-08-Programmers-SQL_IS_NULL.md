---
layout : post
title : Programmers[SQL] IS NULL
subtitle : SQL 고득점 Kit
gh-repo: junhong625/SQL
gh-badge: [star, fork, follow]
tags : [SQL]
comments: true
---
# Programmers SQL 고득점 Kit
## IS NULL 문제
<br>

### 1. 이름이 없는 동물의 아이디
**문제 풀이**
> 동물 보호소에 들어온 동물 중, `이름이 없는 채로 들어온 동물의 ID를 조회`하는 SQL 문을 작성해주세요. 단, `ID는 오름차순 정렬`되어야 합니다.

- `이름이 없는 채로 들어온 동물의 ID를 조회` : `WHERE`절에 `IS NULL`을 이용하여 조회
- `ID는 오름차순 정렬` : `ORDER BY`로 정렬

**정답**
```
SELECT ANIMAL_ID 
FROM ANIMAL_INS 
WHERE NAME IS NULL 
ORDER BY ANIMAL_ID ASC;
```
<br>

### 2. 이름이 있는 동물의 아이디
**문제 풀이**
> 동물 보호소에 들어온 동물 중, `이름이 있는 동물의 ID를 조회`하는 SQL 문을 작성해주세요. 단, `ID는 오름차순 정렬`되어야 합니다.

- `이름이 있는 동물의 ID를 조회` : `WHERE`절에 `IS NOT NULL`을 이용하여 조회
- `ID는 오름차순 정렬` : `ORDER BY`로 정렬

**정답**
```
SELECT ANIMAL_ID 
FROM ANIMAL_INS 
WHERE NAME IS NOT NULL 
ORDER BY ANIMAL_ID ASC;
```
<br>

### 3. NULL 처리하기
**문제 풀이**
> 입양 게시판에 동물 정보를 게시하려 합니다. `동물의 생물 종, 이름, 성별 및 중성화 여부를 아이디 순으로 조회`하는 SQL문을 작성해주세요. 이때 프로그래밍을 모르는 사람들은 NULL이라는 기호를 모르기 때문에, `이름이 없는 동물의 이름은 "No name"으로 표시`해 주세요.

- `동물의 생물 종, 이름, 성별 및 중성화 여부를 아이디 순으로 조회` : `SELECT`문 과 `ORDER BY`를 이용하여 정렬 및 조회
- `이름이 없는 동물의 이름은 "No name"으로 표시` : `CASE`절에 `IS NULL`을 이용하여 "No name"으로 표시

**정답**
```
SELECT ANIMAL_TYPE, 
CASE WHEN NAME IS NULL THEN 'No name' ELSE NAME END AS NAME, SEX_UPON_INTAKE 
FROM ANIMAL_INS 
ORDER BY ANIMAL_ID ASC
```
