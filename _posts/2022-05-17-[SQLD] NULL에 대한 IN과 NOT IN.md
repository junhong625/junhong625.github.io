---
layout : post
title : '[SQLD] NULL과 IN, NOT IN'
subtitle : '[SQLD]  NULL과 IN, NOT IN'
gh-repo: junhong625/Study
gh-badge: [star, fork, follow]
tags : [SQL, Study]
comments: true
---

#  NULL과 IN, NOT IN
- - - 

SQLD에 대해 공부를 하며 기출 문제를 풀다 NULL에 관해 꼭 알아둬야할 것 같은 부분을 알게되어 기록한다.

기본적으로 테이블 구성 시 속성에 대한 제약조건으로 NOT NULL을 설정할 수 있다.  
원하지 않든 원해서였든 NULL을 허용하게 되면 해당 테이블에서 데이터를 조회 시 **IN, NOT IN** 사용에 주의해야 할 것이다.

예시를 들어 보여주겠다.

**[과일 목록 TABLE]**

|과일|구매여부|
|:--|:--|
|바나나|Y|
|사과|N|
|딸기||

### IN으로 조회하는 경우

```SQL
SELECT 과일
FROM 과일 목록
WHERE 구매여부 IN ('Y', NULL)
```

<결과값>

|과일|
|:--|
|바나나|

위와 같은 조건으로 조회한 결과 **바나나**와 **딸기**가 결과값으로 출력될 것 같지만 바나나만 출력이 된다.
  
그 이유를 알기 위해 위 조건문 쿼리를 풀어보자
```SQL
WHERE 구매여부 = 'Y' OR 구매여부 = NULL
```

**NULL은 산술 연산을 할 시에는 NULL을 반환하고**  
**논리 연산을 할 시에는 FALSE를 반환한다.**
따라서 위 쿼리에서는 **구매여부 = NULL**의 결과값이 FALSE가 될 것이다.
그렇기에 구매여부 = 'Y'에 해당하는 데이터만 선택되어 출력되는 것이다.
<br>
<br>

### NOT IN으로 조회하는 경우

```SQL
SELECT 과일
FROM 과일 목록
WHERE 구매여부 NOT IN ('N', NULL)
```

<결과값>
0 row(s) returned

이번엔 N과 NULL이 들어가지 않은 결과값을 출력하려고 했기 때문에 **바나나**가 나오지 않을까? 싶었는데 아무것도 출력이 되지 않았다.  

이유를 알아보기 위해 이번에도 위 조건문 쿼리를 풀어보겠다.
```SQL
WHERE 구매여부 <> 'N' AND 구매여부 <> NULL
```

여기서도 NULL은 논리 연산을 할 시에 FALSE를 반환하기에 **구매여부 <> NULL**에 해당하는 데이터는 아무것도 없게 된다. 
그런데 NOT IN에서는 IN과 다르게 AND 연산자로 연결이 된다.  
따라서 **구매여부 <> 'N'**이 어떠한 결과값을 가지든 **구매여부 <> NULL**에 해당하는 데이터는 아무것도 없기에  
'0 row(s) returned' 즉, 아무것도 출력이 되지 않게 된다.