---
layout : post
title : Programmers[전화번호 목록]
subtitle : Programmers
gh-repo: junhong625/Algorithm
gh-badge: [star, fork, follow]
tags : [Algorithm]
comments: true
---
## 1. 문제 설명
> 전화번호부에 적힌 전화번호 중, 한 번호가 다른 번호의 접두어인 경우가 있는지 확인하려 합니다.
전화번호가 다음과 같을 경우, 구조대 전화번호는 영석이의 전화번호의 접두사입니다.
- 구조대 : 119
- 박준영 : 97 674 223
- 지영석 : 11 9552 4421

> 전화번호부에 적힌 전화번호를 담은 배열 phone_book 이 solution 함수의 매개변수로 주어질 때, 어떤 번호가 다른 번호의 접두어인 경우가 있으면 false를 그렇지 않으면 true를 return 하도록 solution 함수를 작성해주세요.

**제한 사항**
- phone_book의 길이는 1 이상 1,000,000 이하입니다.
    - 각 전화번호의 길이는 1 이상 20 이하입니다.
    - 같은 전화번호가 중복해서 들어있지 않습니다.
  
**입출력 예제**
|phone_book|return|
|:---|:---|
|["119", "97674223", "1195524421"]|false|
|["123","456","789"]|true|
|["12","123","1235","567","88"]|false|

**입출력 예 설명**

입출력 예 #1
앞에서 설명한 예와 같습니다.

입출력 예 #2
한 번호가 다른 번호의 접두사인 경우가 없으므로, 답은 ture입니다.

입출력 예 #3
첫 번째 전화번호, "12"가 두 번째 전화번호 "123"의 접두사입니다. 따라서 답은 false입니다.

## 2. 문제 해결방법
문제를 보고 떠오른 해결방법은 이중 for문을 돌려 단어1과 단어 2가 같지 않을 경우 단어1+단어2[len(단어1):]가  
단어2와 같은지 확인하여 접두어에 해당되는지 확인하는 것이었습니다.  

```
def solution(phone_book):
    for p in phone_book:
        for P in phone_book:
            if p != P:
                if p+P[len(p):] == P:
                    print(p+P[len(p):])
                    return False
    return True
```
위 코드가 제가 제시한 해결방법대로 작성한 코드입니다.
그리고 이 코드를 실행해본 결과 테스트 문제는 전부 성공했습니다.
하지만 이 문제는 효율성을 체크하는 문제로 위 코드는 효율성이 좋지 않아 효율성을 테스트 하는 문제 3, 4번에서  
시간 초과로 실패가 떴습니다.
<img height="300" alt="test1" src="https://user-images.githubusercontent.com/83000975/161500164-58c76275-d3de-41d2-9ccd-0fee699ec302.png">
  
그리고 이 문제를 해결하기 위해 다양한 시도를 하며 떠오른 sort(정렬)와 관련한 정보를 찾아보다 sort를 사용하면 
```
['c', 'a','b', 'ba', 'ab']
```
이렇게 순서가 뒤죽박주인 문자들을
```
['a', 'ab', 'b', 'ba', 'c']
```
이런 식으로 순서에 맞게 정렬을 해주는데

이것을 활용하면 이 문제에서는 하나의 for문만을 돌려 현재 인덱스의 값과 그 인덱스+1에 위치하는 값을  
비교하여 훨씬 간단하게 답을 구할 수 있다는 것을 알 수 있었습니다.

```
def solution(phone_book):
    phone_book = sorted(phone_book)
    for p in range(len(phone_book)-1):
        if phone_book[p] == phone_book[p+1][:len(phone_book[p])]:
            return False
    return True
```
그렇게 해서 작성한 코드가 바로 위 코드입니다.

1. phone_book을 sorted함수를 사용하여 정렬
2. (phone_book의 길이)-1만큼 반복
3. 만약 phone_book[p+1]의 위치하는 값에서 phone_book[p]의 길이만큼 앞에서부터 자른 부분과  
phone_book[p]의 값이 같은지 확인하여 같을 경우 False를 리턴 / 다를 경우 True를 리턴

1, 2, 3의 순서로 코드가 실행될 것이며 
코드를 작성한 결과 
<img height="300" alt="test2" src="https://user-images.githubusercontent.com/83000975/161506610-19696a28-baba-41a7-bb12-6d219d022584.png">
사진과 같이 효율성 문제 3, 4번도 문제없이 통과하는 것을 알 수 있었습니다.

## 3. 더욱 효율적인 해결방법
제가 완성한 코드를 제출한 후 다른 사람들의 코드를 보며 더 나은 해결책을 찾아보던 중 startswith함수를 발견하였습니다.
startswith함수[Link]()를 사용하면 제가 작성한 코드보다 조금 더 간결하게 코드를 작성하고 조금 더 빠르게 결과물을 가져올 수 있습니다.
```
def solution(phone_book):
    phone_book = sorted(phone_book)
    for p in range(len(phone_book)-1):
        if phone_book[p+1].startswith(phone_book[p]):
            return False
    return True
```
<img height="300" alt="test3" src="https://user-images.githubusercontent.com/83000975/161536570-cf283d50-b3df-42b2-833c-44171e046644.png">
