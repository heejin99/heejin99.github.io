---
title: "[DataBase] SQL Set Operations, Null Values"
excerpt: database chapter 3
author_profile: true
categories: 
  - database
tags:
  - database
  - study
last_modified_at: 2021-03-05T19:37:30-05:00
---



## [DataBase] SQL Set Operations, Null Values



### Set Operations

***

* Set Operations
  * union (합집합)
  * intersect (교집합)
  * except (차집합)
* 위의 각 작업은 자동으로 중복을 제거합니다.



#### Section Relation

* section(<u>course_id</u>, <u>sec_id</u>, <u>semester</u>, <u>year</u>, building, room_number, time_slot_id)

<img src="https://user-images.githubusercontent.com/60311404/110095659-7be9d380-7de0-11eb-9170-1abeea6a8f05.png" alt="image" style="zoom:80%;" /> 



#### Union (합집합)

* 2009년 가을이나 2010년 봄에 열린 courses를 찾아라

```sql
(select cousre_id from section
where semester = 'Fall' and year = 2009)
union
(select course_id from section
 where semester = 'Spring' and year = 2010)
```

* 모든 중복 유지

```sql
(select cousre_id from section
where semester = 'Fall' and year = 2009)
union all
(select course_id from section
 where semester = 'Spring' and year = 2010)
```



#### Intersect (교집합)

* 2009년 가을과 2010년 봄에 열린 courses를 찾아라

```sql
(select cousre_id from section
where semester = 'Fall' and year = 2009)
intersect
(select course_id from section
 where semester = 'Spring' and year = 2010)
```



#### Except (차집합)

* 2009년 가을에 열렸지만 2010년 봄에 열리지 않은 courses를 찾아라

```sql
(select cousre_id from section
where semester = 'Fall' and year = 2009)
except
(select course_id from section
 where semester = 'Spring' and year = 2010)
```



### Null Values

***

* 튜플은 일부 속성에 대해 null로 표시되는 null 값을 가질 수 있습니다.

* null

  * unknown (알 수 없는)
  * 존재하지 않는다.

* 널을 포함하는 산술 표현식의 결과가 널입니다.

  * 예) 5+null은 null을 반환합니다.

    ​      1 < null은 null을 반환합니다.

* insert into instructor values (90101, 'Park', 'Comp.Sci.', null);

* 예 ) 

  ```sql
  select name from instructor where salary > 0
  ```

  - salary가 null인 instructor은 출력되지 않습니다.



#### is null

* 술어가 널이면 널 값을 확인하는데 사용할 수 있습니다.

* 예) salary를 알 수 없는 (null) 모든 강사를 찾습니다.

  ```sql
  select name from instructor where salary is null
  ```

  

#### Null Values and Three Valued Logic

* null과의 비교는 알 수 없음(unknown)을 반환합니다.

  * 예 ) "5 < null" or "null <>null" or "null=null"

* 알 수 없는(unknown) 진실(truth) 값을 사용하는 Three-valued 논리 :

  * OR : (unknown **or** true) = true

    ​		 (unknown **or** false) = unknown

    ​		 (unknown **or** unknown) = unknown

  * And : (true **and** unknown) = unknown

    ​		   (false **and** unknown) = false

    ​		   (unknown **and** unknown) = unknown

  * Not : (**not** unknown) = unknown

  * 술어 P가 unknown으로 평가되면 "P **is unknown**" 은 true로 평가됩니다.

***

