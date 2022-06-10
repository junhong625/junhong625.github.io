---
layout : post
title : Programmers[SQL] String, Date
subtitle : SQL 고득점 Kit
gh-repo: junhong625/SQL
gh-badge: [star, fork, follow]
tags : [SQL]
comments: true
---
# Programmers SQL 고득점 Kit

## String, Date 문제
<br>

### 1. 루시와 엘라 찾기
**문제 풀이**
> 동물 보호소에 들어온 동물 중 `이름이 Lucy, Ella, Pickle, Rogan, Sabrina, Mitty인 동물`의 `아이디와 이름, 성별 및 중성화 여부를 조회`하는 SQL 문을 작성해주세요.

- `이름이 Lucy, Ella, Pickle, Rogan, Sabrina, Mitty인 동물` : `WHERE`절을 이용하여 조건 설정
- `아이디와 이름, 성별 및 중성화 여부를 조회` : `SELECT FROM`문으로 조회할 데이터 설정

**정답**
```
SELECT ANIMAL_ID, NAME, SEX_UPON_INTAKE 
FROM ANIMAL_INS
WHERE NAME IN ('Lucy', 'Ella', 'Pickle', 'Rogan', 'Sabrina', 'Mitty') 
ORDER BY ANIMAL_ID;
```
<br>

### 2. 이름에 el이 들어가는 동물 찾기
**문제 풀이**
> 동물 보호소에 들어온 동물 이름 중, `이름에 "EL"이 들어가는 개의 아이디와 이름을 조회`하는 SQL문을 작성해주세요. 이때 결과는 `이름 순으로 조회`해주세요. 단, `이름의 대소문자는 구분하지 않습니다.`

- `이름에 "EL"이 들어가는 개의 아이디와 이름을 조회` : `WHERE`절에 `LIKE`와 비교문을 사용하여 조회 
- `이름 순으로 조회` : `ORDER BY`절로 정렬
- `이름의 대소문자는 구분하지 않습니다.` : `UPPER`를 사용하여 모든 문자 대문자로 통일

**정답**
```
SELECT ANIMAL_ID, NAME 
FROM ANIMAL_INS 
WHERE UPPER(NAME) LIKE '%EL%' AND ANIMAL_TYPE = 'Dog'
ORDER BY NAME;
```
<br>

### 3. 중성화 여부 파악하기
**문제 풀이**
> `동물의 아이디와 이름, 중성화 여부를 아이디 순으로 조회`하는 SQL문을 작성해주세요. 이때 `중성화가 되어있다면 'O', 아니라면 'X'라고 표시`해주세요.

- `동물의 아이디와 이름, 중성화 여부를 아이디 순으로 조회` : `SELECT FROM`문과 `ORDER BY`로 정렬 및 조회
- `중성화가 되어있다면 'O', 아니라면 'X'라고 표시` : `CASE`절을 이용하여 O, X 구분

**정답**
```
SELECT ANIMAL_ID, NAME, 
CASE WHEN SEX_UPON_INTAKE LIKE 'Neutered %' or SEX_UPON_INTAKE LIKE 'Spayed %' 
THEN 'O' Else 'X' End AS '중성화'
FROM ANIMAL_INS
ORDER BY ANIMAL_ID;
```
<br>

### 4. 오랜 기간 보호한 동물(2)
**문제 풀이**
> `입양을 간 동물 중, 보호 기간이 가장 길었던 동물 두 마리의 아이디와 이름을 조회`하는 SQL문을 작성해주세요. 이때 결과는 `보호 기간이 긴 순으로 조회`해야 합니다.

- `입양을 간 동물 중, 보호 기간이 가장 길었던 동물 두 마리의 아이디와 이름을 조회` : `JOIN`과 `WHERE`을 이용하여 입양을 간 동물들을 찾아낸 후 `ORDER BY`절에서 OUTS와 INS의 `DATETIME`을 이용해 보호 기간이 길었던 순으로 정렬 후 `LIMIT`으로 2 RAW만 출력
- `보호 기간이 긴 순으로 조회` : `ORDER BY () DESC`로 역순 정렬

**정답**
```
SELECT INS.ANIMAL_ID, INS.NAME 
FROM ANIMAL_INS AS INS
LEFT OUTER JOIN ANIMAL_OUTS AS OUTS
ON INS.ANIMAL_ID = OUTS.ANIMAL_ID
WHERE OUTS.DATETIME IS NOT NULL
ORDER BY OUTS.DATETIME - INS.DATETIME DESC
LIMIT 2;
```
<br>

### 5. DATETIME에서 DATE로 형 변환
**문제 풀이**
> ANIMAL_INS 테이블에 등록된 모든 레코드에 대해, `각 동물의 아이디와 이름, 들어온 날짜를 조회`하는 SQL문을 작성해주세요. 이때 결과는 `아이디 순으로 조회`해야 합니다.

- `각 동물의 아이디와 이름, 들어온 날짜를 조회` : `DATE_FORMAT`을 사용하여 `DATETIME`의 형 변환
- `아이디 순으로 조회` : `ORDER BY`로  정렬

**정답**
```
SELECT ANIMAL_ID, NAME, DATE_FORMAT(DATETIME, '%Y-%m-%d') AS '날짜' 
FROM ANIMAL_INS 
ORDER BY ANIMAL_ID
```
