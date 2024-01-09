---
layout : post
title : Programmers[SQL] GROUP BY
subtitle : SQL 고득점 Kit
gh-repo: junhong625/SQL
gh-badge: [star, fork, follow]
tags : [SQL]
comments: true
---
# Programmers SQL 고득점 Kit

## GROUP BY 문제
<br>

### 1. 고양이와 개는 몇 마리 있을까
**문제 풀이**
> 동물 보호소에 들어온 동물 중 `고양이와 개가 각각 몇 마리인지 조회`하는 SQL문을 작성해주세요. 이때 `고양이를 개보다 먼저 조회`해주세요.

- `고양이와 개가 각각 몇 마리인지 조회` : `COUNT()`함수와 `GROUP BY`를 이용하여 각각의 마리 수 조회 
- `고양이를 개보다 먼저 조회` : `Cat`이 `Dog`보다 먼저 나오니 `ORDER BY () ASC`를 이용하여 정렬

**정답**
```
SELECT ANIMAL_TYPE, COUNT(ANIMAL_TYPE) as count 
FROM ANIMAL_INS
GROUP BY ANIMAL_TYPE 
ORDER BY ANIMAL_TYPE ASC;
```
<br>

### 2. 동명 동물 수 찾기
**문제 풀이**
> 동물 보호소에 들어온 `동물 이름 중 두 번 이상 쓰인 이름`과 `해당 이름이 쓰인 횟수를 조회`하는 SQL문을 작성해주세요. 이때 결과는 `이름이 없는 동물은 집계에서 제외`하며, 결과는 `이름 순으로 조회`해주세요.

- `동물 이름 중 두 번 이상 쓰인 이름` : `GROUP BY () HAVING ()`에 `COUNT()`함수를 이용
- `해당 이름이 쓰인 횟수를 조회` : `COUNT()` 함수로 횟수 조회
- `이름이 없는 동물은 집계에서 제외` : `IS NOT NULL`을 이용하여 제외
- `이름 순으로 조회` : `ORDER BY`를 이용하여 정렬

**정답**
```
SELECT NAME, COUNT(NAME) as COUNT 
FROM ANIMAL_INS 
GROUP BY NAME 
HAVING COUNT(NAME) >= 2 AND NAME IS NOT NULL 
ORDER BY NAME ASC;
```
<br>

### 3. 입양 시각 구하기(1)
**문제 풀이**
> 보호소에서는 몇 시에 입양이 가장 활발하게 일어나는지 알아보려 합니다. `09:00부터 19:59까지`, `각 시간대별로 입양이 몇 건이나 발생했는지 조회`하는 SQL문을 작성해주세요. 이때 결과는 `시간대 순으로 정렬`해야 합니다.
- `09:00부터 19:59까지` : `BETWEEN 9 AND 19`을 이용
- `각 시간대별로 입양이 몇 건이나 발생했는지 조회` : `GROUP BY`로 시간대별로 묶은 후 `COUNT()`함수로 발생건수 조회  
- `시간대 순으로 정렬` : `ORDER BY`로 정렬
- DATETIME에서 HOUR만 뽑아내기 : `HOUR(DATETIME)`

**정답**
```
SELECT HOUR(DATETIME) AS HOUR, COUNT(*) AS COUNT 
FROM ANIMAL_OUTS 
GROUP BY HOUR(DATETIME)
HAVING HOUR BETWEEN 9 AND 19
ORDER BY HOUR;
```
<br>

### 4. 입양 시각 구하기(2)
**문제 풀이**
> 보호소에서는 몇 시에 입양이 가장 활발하게 일어나는지 알아보려 합니다. `0시부터 23시까지`, `각 시간대별로 입양이 몇 건이나 발생했는지 조회`하는 SQL문을 작성해주세요. 이때 결과는 `시간대 순으로 정렬`해야 합니다.

이 문제에서는 DB에 들어가 있는 시간 데이터가 7시부터 19시까지의 데이터들이 들어있기 때문에 DB에 없는 시간들도 조회되도록 하기위해서 변수를 설정하고 변수를 이용하여 `0시부터 23시까지`의 데이터들이 조회되도록 만들었다.
- `0시부터 23시까지` : `SET @HOUR := -1`변수 설정 후 SELECT문에서 `@HOUR`변수에 1을 더해준 후 `WHERE`절을 통해 시간이 `@HOUR`인 데이터를 조회(`WHERE @HOUR < 23`을 통해 23시까지)  
변수
- `각 시간대별로 입양이 몇 건이나 발생했는지 조회` : `COUNT()`함수를 이용
- `시간대 순으로 정렬` : `ORDER BY`를 이용

**정답**
```
SET @HOUR := -1;
SELECT (@HOUR := @HOUR +1) AS HOUR, 
(SELECT COUNT(*) FROM ANIMAL_OUTS WHERE HOUR(DATETIME) = @HOUR) AS COUNT
FROM ANIMAL_OUTS
WHERE @HOUR < 23;
```
