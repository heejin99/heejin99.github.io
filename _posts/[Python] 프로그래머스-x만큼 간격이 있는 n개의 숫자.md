---
title: "[Python] 프로그래머스 - x만큼 간격이 있는 n개의 숫자"
excerpt: 프로그래머스 연습문제 Level 1
author_profile: true
toc: true
toc_sticky: true
categories: 
  - programmers
tags:
  - coding
  - programmers
  - python
last_modified_at: 2021-08-26-T11:36:30-05:00
---



## 프로그래머스 - x만큼 간격이 있는 n개의 숫자

***

링크: <https://programmers.co.kr/learn/courses/30/lessons/12954>



#### 문제 설명

***

함수 solution은 정수 x와 자연수 n을 입력 받아, x부터 시작해 x씩 증가하는 숫자를 n개 지니는 리스트를 리턴해야 합니다. 다음 제한 조건을 보고, 조건을 만족하는 함수, solution을 완성해주세요.



#### 제한 사항

***

- x는 -10000000 이상, 10000000 이하인 정수입니다.
- n은 1000 이하인 자연수입니다.



#### 입출력 예제

***

- | x    | n    | answer       |
  | ---- | ---- | ------------ |
  | 2    | 5    | [2,4,6,8,10] |
  | 4    | 3    | [4,8,12]     |
  | -4   | 2    | [-4, -8]     |

#### 코드

***

```python
def solution(x, n): 
    answer = []
    for i in range(n):
        answer.append(x*(i+1))
    return answer
```



#### 다른 사람 코드

```python
def number_generator(x, n):
    # 함수를 완성하세요
    return [i * x + x for i in range(n)]
print(number_generator(2, 5))
```



#### 코드 설명

***

- 내 코드
  - 리스트에 x의 배수를 n만큼 넣는다.
  - i+1을 해준 이유는 for문은 i가 0부터 시작하기 때문에 1부터 시작하기 위해 1을 더했습니다.