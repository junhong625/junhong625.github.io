---
layout : post
title : Programmers[Skill Check] Level 1
subtitle : Programmers Skill Check
gh-repo: junhong625/Algorithm
gh-badge: [star, fork, follow]
tags : [Algorithm]
comments: true
---
# Programmers [Skill Check] Level 1
`Programmers` 알고리즘 문제를 여럿 풀어보면서 어느정도 자신감이 쌓여 `Level 1`에 도전해봐도 되겠다는 생각이 들어 스킬체크 `Level 1`에 도전해봤습니다.

결과는.... **합격**!
<img width="300" src="https://user-images.githubusercontent.com/83000975/162741994-5d63b894-8f96-402b-bb53-722bc8ae50b3.png">

1번 문제는 무리없이 한 번에 풀고 2번 문제에서 잠깐 멈칫했지만 무리없이 통과할 수 있었습니다.

문제와 풀이를 설명하여 다시 한 번 복습해보는 시간을 가져보겠습니다.

<br>

## 문제 1
> 문제를 본인의 패턴으로만 찍는 세 학생들이 있다. `answers`배열에 답이 주어졌을 때 가장 많은 문제를 맞추는 학생을 return 해라. 단, 정답 수가 같다면 오름차 순으로 정렬하라.

<br>

**풀이**
1. 학생들의 패턴을 배열로 각각 `first`, `second`, `third`에 지정하여 `stuendts`변수에 저장
2. 
**정답**
```
def solution(answers):
    first =  [1, 2, 3, 4, 5]
    second = [2,1,2,3,2,4,2,5]
    third = [3,3,1,1,2,2,4,4,5,5]
    students = [first, second, third]
    cnt = []
    answer = []

    for i in students:
        count = 0
        for j in range(len(answers)):
            if answers[j] == i[j % len(i)] :
                count += 1
        cnt.append(count)
    for i in range(len(cnt)):
        if max(cnt) == cnt[i]:
            answer.append(i+1)

    return answer
```



