---
title: "[Python] 자료구조 - 사전(Dictionary)"
excerpt: Inflearn Study
author_profile: true
categories: 
  - python
tags:
  - coding
  - inflearn
  - python
last_modified_at: 2021-02-05T23:24:30-05:00
---



## [Python] 자료구조 - 사전(Dictionary)



### Inflearn Study

링크: <https://www.inflearn.com/>

* 인프런에서 "파이썬 무료 강의 (기본편) - 6시간 뒤면 나도 개발자" 강의를 들으며 혼자 공부한 내용입니다.

***

#### 사전(dictionary)

```python
cabinet = {3:"유재석", 100:"김태호"} #딕셔너리 = {key: value}
print(cabinet[3]) # 유재석
print(cabinet[100]) # 김태호
```

- immutable한 키(key)와 mutable한 값(value)로 맵핑되어있는 순서가 없는 집합

***

#### 사전(dictionary) 관련 함수(1)

```python
cabinet = {3:"유재석", 100:"김태호"}

# in
print(3 in cabinet) # True
print(5 in cabinet) # False

# keys
print(cabinet.keys())

# values
print(cabinet.values())

# items
print(cabinet.items())
```

* in : Dictionary에 해당 키가 있는지 검사
* keys : Dictionary의 키를 한 번에 볼 수 있음
* values : Dictionary의 값들을 한 번에 볼 수 있음
* items : Dictionary의 키, 값 쌍을 한 번에 볼 수 있습니다.

***

#### 사전(dictionary) 관련 함수(2)

```python
cabinet = {3:"유재석", 100:"김태호"}

# get
print(cabinet.get(3))
print(cabinet[5]) # 값이 없으면 프로그램 종료
print(cabinet.get(5)) # 값이 없으면 none

# 추가
cabinet[7] = "김종국"

# del
del cabinet[3]
del cabinet[5] # error

# clear
cabinet.clear()
```

- get : value에 접근
- 추가 : cabinet[key] = value
- del : 한쌍의 키, 값을 지울 수 있습니다.
- clear : 딕셔너리 내부 데이터를 지울 수 있습니다.

***

