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
## JOIN 문제
<br>


### 1. 없어진 기록 찾기
**문제 풀이**
> 천재지변으로 인해 일부 데이터가 유실되었습니다. `입양을 간 기록은 있는데, 보호소에 들어온 기록이 없는 동물의 ID와 이름`을 `ID 순으로 조회`하는 SQL문을 작성해주세요.

- `입양을 간 기록은 있는데, 보호소에 들어온 기록이 없는 동물의 ID와 이름` : `LEFT OUTER JOIN`절과 `WHERE`절, `IS NULL`을 이용하여 조회
- `ID 순으로 조회` : `ORDER BY`절을 이용하여 정렬

**정답**
```
SELECT OUTS.ANIMAL_ID, OUTS.NAME 
FROM ANIMAL_OUTS AS OUTS 
LEFT OUTER JOIN ANIMAL_INS AS INS 
ON OUTS.ANIMAL_ID = INS.ANIMAL_ID
WHERE INS.ANIMAL_ID is NULL 
ORDER BY OUTS.ANIMAL_ID
```
<br>

### 2. 있었는데요 없었습니다
**문제 풀이**
> 관리자의 실수로 일부 동물의 입양일이 잘못 입력되었습니다. `보호 시작일보다 입양일이 더 빠른 동물의 아이디와 이름을 조회`하는 SQL문을 작성해주세요. 이때 결과는 `보호 시작일이 빠른 순으로 조회`해야합니다.

- `보호 시작일보다 입양일이 더 빠른 동물의 아이디와 이름을 조회` : `LEFT OUTER JOIN`절을 이용하여 데이터를 합친 후 `WHERE`절에서 비교문을 통해 조회 
- `보호 시작일이 빠른 순으로 조회` : `ORDER BY`절을 이용하여 정렬

**정답**
```
SELECT INS.ANIMAL_ID, INS.NAME 
FROM ANIMAL_INS AS INS 
LEFT OUTER JOIN ANIMAL_OUTS AS OUTS 
ON OUTS.ANIMAL_ID = INS.ANIMAL_ID 
WHERE OUTS.DATETIME < INS.DATETIME 
ORDER BY INS.DATETIME;
```
<br>

### 3. 오랜 기간 보호한 동물(1)
**문제 풀이**
> `아직 입양을 못 간 동물 중, 가장 오래 보호소에 있었던 동물 3마리의 이름과 보호 시작일을 조회`하는 SQL문을 작성해주세요. 이때 결과는 `보호 시작일 순으로 조회`해야 합니다.

- `아직 입양을 못 간 동물 중, 가장 오래 보호소에 있었던 동물 3마리의 이름과 보호 시작일을 조회` : `JOIN`절로 `INS`와 `OUTS`테이블을 병합 후  `WHERE`절에 입양일 데이터가 `IS NULL`인 데이터를 `LIMIT`을 이용하여 3마리의 데이터만 조회 
- `보호 시작일 순으로 조회` : `ORDER BY`절을 이용하여 정렬

**정답**
```
SELECT INS.NAME, INS.DATETIME 
FROM ANIMAL_INS AS INS 
LEFT OUTER JOIN ANIMAL_OUTS AS OUTS 
ON INS.ANIMAL_ID = OUTS.ANIMAL_ID 
WHERE OUTS.DATETIME IS NULL 
ORDER BY INS.DATETIME LIMIT 3;
```
<br>

### 4. 보호소에서 중성화한 동물
**문제 풀이**
> 보호소에서 중성화 수술을 거친 동물 정보를 알아보려 합니다. `보호소에 들어올 당시에는 중성화되지 않았지만, 보호소를 나갈 당시에는 중성화된 동물의 아이디와 생물 종, 이름을 조회`하는 `아이디 순으로 조회`하는 SQL 문을 작성해주세요.

- `보호소에 들어올 당시에는 중성화되지 않았지만, 보호소를 나갈 당시에는 중성화된 동물의 아이디와 생물 종, 이름을 조회` : `JOIN`절을 이용하여 두 테이블을 병합하는데 서브 쿼리를 사용하여 보호에 들어올 당시 중성화 되지 않은 동물들의 데이터들과 보호소를 나갈 당시에는 중성화된 동물의 데이터를 병합 하여 `WHERE`절을 통해 `NULL`값의 데이터가 포합되지 않은 데이터들을 조회
- `아이디 순으로 조회` : `ORDER BY`절을 이용하여 정렬

**정답**
```
SELECT INS.ANIMAL_ID, INS.ANIMAL_TYPE, INS.NAME
FROM (SELECT * FROM ANIMAL_INS WHERE SEX_UPON_INTAKE = 'Intact Male' or SEX_UPON_INTAKE = 'Intact Female') AS INS
LEFT OUTER JOIN (SELECT * FROM ANIMAL_OUTS WHERE SEX_UPON_OUTCOME = 'Neutered Male' or SEX_UPON_OUTCOME = 'Spayed Female') AS OUTS
ON INS.ANIMAL_ID = OUTS.ANIMAL_ID
WHERE OUTS.SEX_UPON_OUTCOME is not NULL;
```
