---
layout : post
title : 프로젝트 오일러 27번 문제 풀이
subtitle : Project euler
gh-repo: junhong625/Algorithm
gh-badge: [star, fork, follow]
tags : [Algorithm]
comments: true
---

# 프로젝트 오일러 27번 문제 풀이

==============================

## 27번 문제
> 연속되는 n에 대해 가장 많은 소수를 만들어내는 이차식

이 문제는 n^2 +an + b (|a|<1000, |b|<1000)의 모양을 가진 이차식으로  
연속되는 n에 대해 가장 많은 소수를 만드는 이차식을 찾아 그 이차식의 계수 a와 b의 곱을 구하는 것이다. 

문제를 확인하고 머리 속으로 구상한 형태는 소수를 구하는 함수를 만들고 for문을 통해 계수 a와 b의 값을 구하는 것이다.  
그리고 이 두 가지를 코드로 나타내면 아래와 같다.  
1. 제곱근으로 빠르게 소수를 판단할 수 있는 함수

```
def prime_num(num):
    if num<2: 
        return False
    for i in range(2, int(num**0.5)+1):
        if num%i == 0:
            return False
    return True
```

2. -999~999의 수를 가진 a와 b의 이중 for문을 통해 가장 많은 소수를 가진 이차식의 계수 a와 b구하기

```
# 연속되는 n에 대해 가장 많은 소수 횟수 
max_prime_number_count = 0

# 계수 a의 값이 들어갈 A
A = 0
# 계수 b의 값이 들어갈 B
B = 0

for a in range(-999, 1000):
    for b in range(-999, 1000):
        n = 0
        while True:
            if prime_num(n*n+a*n+b):
                n += 1
            else:
                break
            if max_prime_number_count < n:
                max_prime_number_count = n
                A, B = a, b
```

저 두 코드를 합쳐서 작동시켜본 결과 대략 2초 정도 걸려 답을 구해낼 수 있었다.
정답을 구한 후 더 빠르게 답을 구해내기 위한 방법을 생각하다보니  
n^2 +an + b 식에서 a에 짝수가 들어간다면 답이 소수가 나올 수 없을 것이고 b에 소수가 아닌 다른 수가 들어간다면 연속된 소수를 구할 수 없다는 생각이 들었다.
그리하여 a에는 홀수라는 조건을 b에는 소수라는 조건을 걸어 코드를 보완했다.
```
from time import time as t
start = t()

def prime_num(num):
    if num < 2:
        return False

    # 제곱근 통해 소수 확인
    for i in range(2, int(num**0.5)+1):
        if num % i == 0:
            return False
    return True

max_prime_number_count = 0
A = 0
# 소수
B = 0
for a in range(-999, 1000):
    # a는 홀수
    if a % 2 == 0:
        continue
    for b in range(-999, 1000):
        # b는 소수여야함
        if prime_num(b):
            x = 0
            while True:
                if prime_num(x*x+a*x+b):
                    x += 1
                else:
                    break
                if max_prime_number_count < x:
                    max_prime_number_count = x
                    A, B = a, b
end = t()
print("소수의 최대 연속 횟수 :", max_prime_number_count)
print("a = %d, b = %d" % (A, B))
print("계수 a와 b의 곱 :", A*B)
print('소요시간:{}'.format(end-start))
```

최종적으로 완성된 코드는 위와 같다.  
단지 a에 홀수라는 조건과 b에 소수라는 조건을 걸었을 뿐이지만 소요시간을 2초에 1초로 절반으로 줄일 수 있었다. 

### 역시 개발자는 계속 효율적으로 코드를 작성하고 더 나은 코드를 작성하기 위해 노력해야 한다는 생각이 들었다.
