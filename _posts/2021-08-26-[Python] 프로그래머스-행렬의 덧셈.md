---
title: "[Python] 프로그래머스 - 행렬의 덧셈"
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
last_modified_at: 2021-08-26-T11:50:30-05:00
---



## 프로그래머스 - 행렬의 덧셈

***

링크: <https://programmers.co.kr/learn/courses/30/lessons/12950>



#### 문제 설명

***

행렬의 덧셈은 행과 열의 크기가 같은 두 행렬의 같은 행, 같은 열의 값을 서로 더한 결과가 됩니다. 2개의 행렬 arr1과 arr2를 입력받아, 행렬 덧셈의 결과를 반환하는 함수, solution을 완성해주세요.



#### 제한 사항

***

- 행렬 arr1, arr2의 행과 열의 길이는 500을 넘지 않습니다.



#### 입출력 예제

***

- | arr1          | arr2          | return        |
  | ------------- | ------------- | ------------- |
  | [[1,2],[2,3]] | [[3,4],[5,6]] | [[4,6],[7,9]] |
  | [[1],[2]]     | [[3],[4]]     | [[4],[6]]     |

#### 코드

***

```python
def solution(arr1, arr2):
    for i in range(len(arr1)):
        for j in range(len(arr1[0])):
            arr1[i][j] += arr2[i][j]
    return arr1
```



#### 다른 사람 코드

```python
import numpy as np
def sumMatrix(A,B):
    A=np.array(A)
    B=np.array(B)
    answer=A+B
    return answer.tolist()
```



#### 코드 설명

***

- 내 코드
  - 이중 for문을 돌면서 arr1의 원소에 arr2 원소를 하나하나 더해서 리턴한다.
- 다른 사람 코드
  - np.array 함수를 이용해 배열을 생성한다.
  - tolist()함수를 이용해 같은 위치에 있는 데이터끼리 묶어준다.