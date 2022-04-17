---
layout : post
title : '[Python]lambda 함수(map, reduce, filter)'
subtitle : lambda 함수
gh-repo: junhong625/Python
gh-badge: [star, fork, follow]
tags : [Python]
comments: true
---
  
`lambda 함수`는 python에서 사용하는 함수로 '익명함수'라고도 불립니다.  
그렇다면 `lambda 함수`를 사용하는 이유는 무엇일까요??

## lambda 함수를 사용하는 목적
1. `lambda 함수`를 사용하면 `def 함수`보다 코드를 훨씬 간결하게 만들어줍니다.
2. `lambda 함수`는 익명 함수이기에 한 번 사용되면 heap메모리에서 삭제되기에 메모리 관리에 용이합니다.
3. `lambda 함수`를 사용하면 코드가 간결해져 가독성이 좋아집니다.  
(하지만 너무 남용하면 가독성이 나빠집니다.)


## lambda 함수 사용방법
기본적인 사용 방법은 `lambda 매개변수 : 표현식`으로 아래와 같이 사용할 수 있습니다.
``` 
(lambda x:x+5)(5)
```
> 10

만약 위의 `lambda 함수`를 `def 함수`로 표현을 한다면?
```
def plus(x):
    return x+5
```
> def plus(5)
> 10
