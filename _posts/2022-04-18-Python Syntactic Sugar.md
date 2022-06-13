---
layout : post
title : '[Python]Python Syntactic Sugar'
subtitle : Python Syntactic Sugar
gh-repo: junhong625/Python
gh-badge: [star, fork, follow]
tags : [Python]
comments: true
---

저번에 알고리즘 문제를 리뷰하면서 `Syntacitc Sugar`중 하나인 `for-else문`에 대해 배웠는데요. 오늘은 `Syntacitc Sugar`들에 대해 찾아서 공부하고 배운것들에 대해 정리하고자 합니다. 

## 1. 다중 할당<Multiple Assignment>
```python
a = 1
b = 1
c = 1
```
하나씩 일일이 변수에 값을 넣어줬던 코드를 `Syntacitc Sugar`를 사용해서 나타내면 아래와 같이 나타낼 수 있습니다.
```python
a = b = c = 1
```
<br>

## 2. 파이썬 변수 교환<Pythonic Swap>
```python
tmp = a
a = b
b = tmp
```
a와 b의 값을 교환하기 위해서 새로운 변수를 만들어 교환했던 코드를 `Syntacitc Sugar`를 사용하면 아래와 같이 나타낼 수 있습니다.
```python
a, b = b, a
```
<br>

## 3. 'FT'(boolean)
Python에서 문자열을 index를 사용하여 접근할 수 있는 점과 False=0, True=1에 대응하는 값을 나타내는 것을 응용한 방법입니다.
```python
'jh coder'[0] > 'j', 'jh coder'[1] > 'h'
'jh coder'[False] > 'j', 'jh coder'[True] > 'h'
```
<br>

## 4. 비교 연산자 합치기<Chaining Comparison Operators>
```python
if a < b and b <= c:
    ...
```
위와 같이 and를 사용하여 비교문을 두 번 사용했던 코드를 `Syntacitc Sugar`를 사용하면 아래와 같이 사용할 수 있습니다.
```python
if a < b <= c:
    ...
```
<br>

## 5. 삼항 연산자<Ternary Operator>
```python
if c = True:
    x = a
else:
    x = b
```
위와 같은 `if-else문`을 `Syntacitc Sugar`를 사용하면 아래와 같이 나타낼 수 있습니다.
```python
x = a if c = True else b
```
<br>

## 6. LIST/TUPLE Unpacking
```python
a = 1
b = 2
c = 3
```
위와 같이 각각 줄을 나눠 변수에 값을 입력해줬던 방식을 `Syntacitc Sugar`를 사용하면 아래와 같이 나타낼 수 있습니다.
```python
a, b, c = 1, 2, 3
```
이걸 응용하면 아래와 같이 list나 tuple을 이용해서도 나타낼 수 있습니다.
```python
nums = [1, 2, 3]
a, b, c = nums
```
<br>

## 7. Comprehension
`Comprehension`은 list, set, dictionary 형식의 자료구조들을 한줄로 간단하게 생성할 수 있도록 도와주는 아주 고마운 친구입니다.
for문을 사용하여 코드를 작성시 훨씬 코드를 간결하게 만들어주는 친구입니다.

### List Comprehension
```python
even = []
for i in range(10):
    if i % 2 == 0:
        nums.append(i)
```
기존에 for문을 사용하여 list를 생성할 때는 위와 같이 작성했던 코드를 `List Comprehension`을 사용하면 아래와 같이 간결하게 작성할 수 있습니다.
```python
even = [i for i in range(10) if i % 2 == 0]
```
`if-else문`을 사용한 예시는 아래와 같습니다.
```python
# 홀수는 제곱, 짝수는 + 1
nums = [i + 1 if i % 2 == 0 else i ** 2 for i in range(10)]
```

### Set Comprehension
100의 약수를 가져오는 set을 작성하면 아래와 같이 작성할 수 있을 것입니다. 
```python
divisor = set()
for i in range(100):
    if 100 % i == 0:
        divisor.add(i)
```
위와 같이 작성했던 set을 `Set Comprehension`을 사용하면 아래와 같이 간결하게 작성할 수 있습니다.
```python
divisor = {i for i in range(100) if 100 % i == 0}
```

### Dictionary Comprehension
1부터 10까지의 숫자들 중 홀수만 key로 가지고 각 key가 제곱된 값을 value로 지정한 dictionary를 만들면 아래와 같이 만들 수 있을 것입니다.
```python
squared = {}
for i in range(1, 11):
    if i % 2 == 1:
        squared[i] = i ** 2
```
위와 같이 작성했던 dict를 `Dictionary Comprehension`을 이용하면 아래와 같이 간결하게 작성할 수 있습니다.
```python
squared = {i: i**2 for i in range(1, 11) if i % 2 == 1}
```
  
   
이렇게 Python에서 사용하는 다양한 `Syntactic Sugar`에 대해 알아봤습니다. 오늘도 새로운 지식을 얻어가 기분 좋게 하루를 마무리 지을 수 있을 것 같습니다.

> 참고링크 [https://www.codeit.kr/community/threads/19376](https://www.codeit.kr/community/threads/19376)
