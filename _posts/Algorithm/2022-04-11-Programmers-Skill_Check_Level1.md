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
<img width="900" src="https://user-images.githubusercontent.com/83000975/162741994-5d63b894-8f96-402b-bb53-722bc8ae50b3.png">

1번 문제는 무리없이 한 번에 풀고 2번 문제에서 잠깐 멈칫했지만 무리없이 통과할 수 있었습니다.

문제와 풀이를 설명하여 다시 한 번 복습해보는 시간을 가져보겠습니다.

<br>

## 문제 1
> 문제를 본인의 패턴으로만 찍는 세 학생들이 있다. `answers`배열에 답이 주어졌을 때 가장 많은 문제를 맞추는 학생을 return 해라. 단, 정답 수가 같다면 오름차 순으로 정렬하라.

<br>

**풀이**
1. 학생들의 패턴을 배열로 각각 `first`, `second`, `third`에 지정하여 `stuendts`변수에 저장
2. 각 학생의 정답 수가 들어갈 리스트 `cnt`와 가장 많은 정답을 기록한 학생이 들어갈 리스트 `answer` 생성
3. `students`와 `len(answers)`를 활용한 이중 for문 을 통해 `cnt`에 각 학생의 정답 수 저장 **(각 학생의 패턴을 index와 상관없이 계속 반복될 수 있도록 answers의 index를 현재 반복중인 학생의 패턴 길이만큼 나눈 나머지로 index설정)**
4. `cnt`길이만큼 즉, 3번 반복하는 for문을 통해 `max(cnt)`(= 최다 정답 수)와 같은 `cnt`의 index+1을 `answer`리스트에 에 추가 (`cnt`에 정답 수를 집어넣을 때 학생의 순번을 오름차 순으로 집어넣었기에 정답은 `answer`에 오름차순으로 추가됨)
<br>

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
<br>

## 문제 2
> 마라톤에 참여한 사람들의 리스트 `participant`와 마라톤을 완주한 사람들의 리스트 `completion`이 주어진다. 완주자가 참여자보다 1명 적을 때 완주하지 못한 사람의 이름을 return해라. (이름은 모두 소문자이며 동명이인이 존재할 수 있다.)

<br>

**풀이**
1. 본 문제는 효율성을 체크하는 문제로 효율성을 높이기 위해 `dictionary`를 사용하여 문제 풀이
2. 정답이 들어갈 변수 `answer`와 참여자 명단과 완주자 명단을 dictionary타입으로 변환하여 집어넣을 변수 `p`와 `c` 생성
3. `enumerate`함수와 `sorted`함수를 이용한 for문을 통해 `idx: 이름` 형식으로 `p`와 `c`에 저장
4. 완주자 수만큼 반복하는 for문을 통해 같은 index에 위치한 `c`와 `p`의 값이 다를 때 `answer`는 `p`의 index에 위치한 값으로 저장 **(`sorted`함수를 통해 정렬하였기에 같은 index에 서로 다른 이름이 있다면 참여자 리스트에서 해당 index에 위치한 사람이 마라톤을 완주하지 못한 사람이다.)** 
5. `4`번의 예외인 경우의 수로 정렬한 참여자 명단의 맨 마지막에 위치한 사람이 마라톤을 완주하지 못한 사람일 경우의 조건문 설정

<br>

**정답**
```
def solution(participant, completion):
    answer = ''
    p = {}
    c = {}
    for idx, value in enumerate(sorted(participant)):
        p[idx] = value
    for idx, value in enumerate(sorted(completion)):
        c[idx] = value
    for i in range(len(completion)):
        if c[i] != p[i]:
            answer = p[i]
            break
    if len(answer) == 0:
        answer = p[len(p)-1]
    return answer
```

<br>

아직 갈길이 멀지만 Level 1을 통과했다니 조금 뿌듯한 마음이 듭니다. 
**이에 만족하지 않고 계속 공부하여 Level 2, 3, 4까지 얼른 나아가자!!!**
