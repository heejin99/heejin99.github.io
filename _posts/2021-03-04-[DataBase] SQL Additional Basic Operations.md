---
title: "[DataBase] SQL Additional Basic Operations"
excerpt: database chapter 3
author_profile: true
categories: 
  - database
tags:
  - database
  - study
last_modified_at: 2021-03-04T17:56:30-05:00
---



## [DataBase] SQL Additional Basic Operations



### The Rename Operation

***

* SQL절은 **as** 절을 사용하여 관계 및 속성의 이름을 바꿀 수 있습니다.
* *old-name* **as** *new-name*

```sql
select ID as instructor_id, name as instructor_name, salary/12 as monthly_salary
from instructor
```

* 긴 관계 이름을 사용하기 더 편리한 단축 버전으로 교체합니다.

```sql
select instructor.name, teaches.course_id
from instructor, teaches
where instructor.ID = teaches.ID
/* = */
select T.name, S.course_id
from instructor as T, teaches as S
where T.ID = S.ID
```

* 같은 관계에서 튜플을 비교해야할 때 



#### Self Join 

* "Finance 부서에서 최소 한명의 instructor보다 salary가 높은 모든 instructor의 이름을 찾으시오"

<img src="C:\Users\wkdgm\AppData\Roaming\Typora\typora-user-images\image-20210304182600805.png" alt="renameoperaion" style="zoom:80%;" />  <img src="C:\Users\wkdgm\AppData\Roaming\Typora\typora-user-images\image-20210304182600805.png" alt="renameoperaion" style="zoom:80%;" /> 

​						**instructor as T**															**instructor as S**

```sql
select distinct name
from instructor as T, instructor as S
where T.salary > S.salary and S.dept_name = 'Finance'
```

* "Finance 부서에서 최소 한명의 instructor보다 salary가 높은 Comp. Sci. 부서의 모든 instructor의 이름을 찾으시오

```sql
select distinct name
from instructor as T, instructor as S
where T.salary > S.salary 
		and S.dept_name = 'Finance' 
		and T.dept_name = 'Comp.Sci.'
```



### String Operations

***

* SQL에는 문자열 비교를 위한 문자열 일치 연산자가 포함되어 있습니다.
* **"like"** 연산자는 두 개의 특수 문자를 사용하여 설명되는 패턴을 사용합니다.
* % 문자 : 모든 하위 문자열과 일치합니다.
* _ 문자 : 모든 문자와 일치합니다.
  * 예) 'Intro %' : "Intro"로 시작하는 모든 문자열과 일치합니다.
    * Introduction to SQL (o)
    * An Introduction to SQL (X)
  * '%Comp%'
    * Intro. To Computer Science (O)
    * Computational Biology (O)
* 예) select name from instructor where name like '%김%';



### Ordering the Display of Tuples - order by

***

* 모든 instructors의 이름을 알파벳 순으로 나열합니다.

```sql
select distinct name
from instructor
order by name
/* default : ascending order (오름차순) */
```

* 각 속성에 대해 내림차순으로 **desc**를 지정하거나 오름차순으로 **asc**를 지정할 수 있습니다.
* 오름차순이 기본값입니다.

```sql
select *
from instructor
order by salary desc
```



### Where Clause Predicates

***

* SQL 에는 **Between** 비교 연산자가 포함됩니다.
* 예) 급여가 $90,000~$100,000 인 모든 instructor의 이름을 찾습니다.
  * salary >= 90,000 and salary <= 100,000

```sql
select name
from instructor
where salary between 90000 and 100000
```

***

