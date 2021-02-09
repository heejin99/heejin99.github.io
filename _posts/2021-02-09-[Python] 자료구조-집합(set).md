---
title: "[Python] 자료구조 - 집합(set)"
excerpt: Inflearn Study
author_profile: true
categories: 
  - python
tags:
  - coding
  - inflearn
  - python
last_modified_at: 2021-02-09T23:33:30-05:00
---



## [Python] 자료구조 - 집합(set)



### Inflearn Study

링크: <https://www.inflearn.com/>

* 인프런에서 "파이썬 무료 강의 (기본편) - 6시간 뒤면 나도 개발자" 강의를 들으며 혼자 공부한 내용입니다.

***

#### 집합(set)

```python
my_set = {1, 2, 3}
java = {"유재석", "김태호", "양세형"}
python = set(["유재석", "박명수"])
```

- 중복된 데이터를 가질 수 없습니다.
- 순서가 없습니다.

***

#### 집합 예제 (1)

```python
# 교집합
print(java & python)
print(java.intersection(python))
```

* 교집합: 두 개의 집합에서 공통된 원소

```python
# 합집합
print(java | python)
print(java.union(python))
```

* 합집합: 두 개의 집합에 있는 모든 원소

```python
# 차집합
print(java - python)
print(java.difference(python))
```

* 차집합: java 집합에는 있지만 python 집합에는 없는 원소 

***

#### 집합 예제 (2)

```python
# 집합 길이 구하기
len(my_set)
```

- 집합 길이 구하기: len 사용

```python
# 값 존재 여부 확인
print(2 in my_set)
print(5 in my_set)

print(1 not in my_set)
print(7 not in my_set)
```

* 값의 존재 여부 확인: in/not in

```python
# 원소 추가
my_set = {1, 2, 3, 5}
my_set.add(4)

# 원소 여러개 추가
my_set = {1, 2, 3, 5}
my_set.update([4,6,7])
```

* 원소 추가 : add
* 원소 여러 개를 한 번에 추가: update

```python
# 원소 제거
my_set = {1, 2, 3, 5}
my_set.remove(5)

my_set.remove(7) # 에러 메시지 나면서 프로그램 종료

my_set.discard(7) # 에러가 나지 않음

my_set.pop() # 임의의 원소를 하나 가져온 후 삭제

my_set.clear() # 모든 원소 제거 -> 공집합
```

* 원소 제거: remove
  * 없는 원소를 제거했을 시 에러가 발생하면서 프로그램이 종료됩니다.
* discard: 없는 원소 제거 시 에러가 발생하지 않습니다.
* pop: 임의의 원소를 하나 가져온 후 삭제합니다.
* clear: 모든 원소를 제거해 공집합을 만듭니다.

***

