---
title: "[DataBase] SQL 기본 구조"
excerpt: database chapter 3
author_profile: true
categories: 
  - database
tags:
  - database
  - study
last_modified_at: 2021-03-04T00:27:30-05:00
---



## [DataBase] SQL 기본 구조



### Basic Query Structure

***

```sql
select A1, A2, ..., An
from r1, r2, ..., rm
where P
```

* A<sub>i</sub> : attribute 

* R<sub>i</sub> : relation (관계)

* P : predicate

  -> SQL query의 결과는 relation



### The Select Clause

***

* select 절은 쿼리 결과에서 원하는 속성을 나열합니다.
  * 관계형 대수의 <u>projection operation</u>에 해당합니다.
* **Π**<sub>ID, salary</sub>**(instructor)** -> **select** ID, salary **from** instructor
* SQL의 이름은 대소문자를 구분하지 않습니다.



#### Distinct

* SQL은 쿼리 결과뿐만 아니라 관계에서도 중복을 허용합니다.
* 중복 항목을 강제로 제거하려면 선택 후 distinct 키워드를 삽입합니다.
* instructor와 함께 모든 departments의 이름을 찾고 중복을 제거합니다.

```sql
select distinct dept_name
from instructor
```



#### All

* 키워드 all은 중복항목이 제거되지 않도록 지정합니다.

```sql
select all dept_name from instructor

/* == */

select dept_name from instructor
```



#### *

* select 절의 별표는 **모든 속성** 을 나타냅니다

```sql
select * from instructor
```

 

#### Arithmetic expressions

* select 절에는 연산 +,-,*,/ 와 관련된 산술 표현식과 튜플의 상수 또는 속성에 대한 연산이 포함될 수 있습니다.

* The query:

  ```sql
  select ID, name, salary/12
  from instructor
  ```

  * 속성 급여의 값을 12로 나눈다는 점을 제외하면 instructor relation 과 동일한 관계를 가집니다.



### The Where Clause

***

* where 절은 결과가 충족 해야하는 조건을 지정합니다.
  * 관계형 대수의 Selection predicate에 해당합니다.
* **σ**<sub>salary > $85,000 </sub>**(instructor)** -> **select** * **from** instructor **where** salary>85000

```sql
select name
from instructor
where dept_name == 'Comp. Sci.' and salary > 70000
```

* salary > 70000 이고 dept_name이 'Comp. Sci.'인 모든 instructor의 name을 찾습니다.
  * **and** / **or**



### The From Clause

***

* from 절은 쿼리와 관련된 관계를 나열합니다.

  * 관계형 대수의 Cartesian product operation에 해당합니다.

* instructor X teaches의 Cartesian product 찾기

  ```sql
  select * 
  from instructor, teaches
  ```

  * 두 관계로부터 모든 속성을 사용하여 가능한 모든 instructor - teaches 쌍을 생성합니다. ![CartesianImage](C:\Users\wkdgm\AppData\Roaming\Typora\typora-user-images\image-20210304000939032.png)   

* Cartesian product는 직접적으로 그다지 유용하지는 않습니다.

  * 하지만 where 절 조건 (관계형 대수의 선택 연산)과 결합하면 유용합니다.
  * 동일한 ID 값을 갖고 있는 instructor tuples과 함께 teaches tuples를 match 시킵니다.

  -> **JOIN**



### Join

***

```sql
select name, cousre_id /* attribute */
from instructor, teaches 
where instructor.ID = teaches.ID /* relation.attribute*/
```

<img src="C:\Users\wkdgm\AppData\Roaming\Typora\typora-user-images\image-20210304001331783.png" alt="Join" style="zoom: 67%;" /> 

<img src="C:\Users\wkdgm\AppData\Roaming\Typora\typora-user-images\image-20210304001821387.png" alt="Original" style="zoom:67%;" /> 

**Step 1**. **from**절에 나열되어 있는 relations의 Cartesian product를 발생시킵니다.

<img src="C:\Users\wkdgm\AppData\Roaming\Typora\typora-user-images\image-20210304002017594.png" style="zoom:67%;" /> 

**Step 2**. 1단계의 결과에 **where** 절에 지정된 clause를 적용합니다.

<img src="C:\Users\wkdgm\AppData\Roaming\Typora\typora-user-images\image-20210304001731150.png" alt="REsult" style="zoom:67%;" /> 

**Step 3**. 2단계 결과의 각 튜플에 대해 select 절에 지정된 속성을 출력합니다.

-> course를 가르친 모든 instructor의 경우 자신이 가르친 course의 이름과 course ID를 찾으십시오

 

 ### Joins

***

```sql
select section.course_id, semester, year, title
from section, course
where section.course_id = course.course_id and dept_name = 'Comp. Sci.'
```

* Comp. Sci. department에서 제공하는 각 과정의 ID, 학기, 연도 및 제목을 찾습니다.



#### Natural Join

***

* Natural Join은 모든 공통 속성에 대해 동일한 값을 가진 튜플과 일치하고 각 공통 열의 복사본을 하나만 유지합니다.

* instructor <img src="https://user-images.githubusercontent.com/60311404/108045271-a0c31480-7086-11eb-9652-592ea574434c.png" alt="자연조인" style="zoom:33%;" /> teaches

```sql
select * 
from instructor natural join teaches
```

<img src="C:\Users\wkdgm\AppData\Roaming\Typora\typora-user-images\image-20210304002544026.png" alt="naturalJoin" style="zoom:80%;" />

```sql
select name, course_id
from instructor, teaches
where instructor.ID = teaches.ID

/* == */

select name, course_id
from instructor natural join teaches
```

***

