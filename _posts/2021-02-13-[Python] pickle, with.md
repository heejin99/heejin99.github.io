---
title: "[Python] pickle, with"
excerpt: Inflearn Study
author_profile: true
categories: 
  - python
tags:
  - coding
  - inflearn
  - python
last_modified_at: 2021-02-13T00:11:30-05:00
---



## [Python] pickle, with



### Inflearn Study

링크: <https://www.inflearn.com/>

* 인프런에서 "파이썬 무료 강의 (기본편) - 6시간 뒤면 나도 개발자" 강의를 들으며 혼자 공부한 내용입니다.

***

#### pickle

```python
import pickle
```

* 텍스트 상태의 데이터가 아닌 파이썬 객체 자체를 파일로 저장하는 것입니다.
* 파이썬의 모든 객체를 다 저장할 수 있습니다.

***

#### pickle 파일 입출력

```python
profile_file = open("profile.pickle", "wb")  # wb를 이용해 파일에 써야합니다.
profile = {"이름":"박명수", "나이":30, "취미":["축구", "골프", "코딩"]}
print(profile)
pickle.dump(profile, profile_file) # profile에 있는 정보를 file에 저장
profile_file.close()
```

* dump: pickle로 저장하기

```python
profile_file = open("profile.pickle","rb")
profile = pickle.load(profile_file)
print(profile)
profile_file.close()
```

* load: pickle 불러오기

***

#### with

```python
import pickle

with open("profile.pickle", "rb") as profile_file:
    print(pickle.load(profile_file))

with open("study.txt", "w", encoding="utf8") as study_file:
    study_file.write("파이썬 공부 즁")

with open("study.txt","r",encoding="utf8") as study_file:
    print(study_file.read())
```

* with : 명시적으로 파일을 닫지 않아도 됩니다.
  * with 블록이 끝나는 시점에 파일 닫는 동작이 수행됩니다.

***

