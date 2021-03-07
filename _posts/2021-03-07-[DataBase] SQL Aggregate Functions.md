---
title: "[DataBase] SQL Aggregate Functions"
excerpt: database chapter 3
author_profile: true
categories: 
  - database
tags:
  - database
  - study
last_modified_at: 2021-03-07T16:59:30-05:00
---



## [DataBase] SQL Aggregate Functions



### Aggregate Functions

***

* 관계 열의 다중 값 집합에 대해 작동하고 값을 반환합니다.

  * **avg** : 평균값
  * **min** : 최소값
  * **max** : 최대값
  * **sum** : 합계
  * **count** : 값의 개수

  

#### Avg

* Computer Science 부서(department)의 강사(instructors)의 평균 급여(salary) 찾기

```sql
select avg (salary) /* avg (salary) : DBMS가 주는 임의의 이름 */
from instructor
where dpet_name = 'Comp. Sci.'

select avg (salary) as avg_salary
from instructor
where dept_name = 'Comp. Sci.'
```

 

#### Count

* course 관계에 tuples의 수를 찾기

```sql
select count (*)
from course;
```

* 2010년 봄의 과정을 가르치는 instructors의 전체 수 찾기

```sql
select count(distinct ID)
from teaches 
where semester = 'Spring' and year = 2010

select count(ID)
from teaches
where semester = 'Spring' and year = 2010
```



#### Max / Min / Sum

* Max : 최대값

```sql
select name, max(salary)
from instructor;
```

* Min : 최소값

```sql
select name, min(salary)
from instructor;
```

* Sum : 합

```sql
select sum(salary)
from instructor;
```



#### Group By

* 각 부서 (department)에 강사 (instructors)의 평균 급여 (salary)를 찾아라

```sql
select dept_name, avg(salary)
from instructor
group by dept_name;
```

Step1) instructor relation -> instructor relation을 dept_name으로 그룹화

Step2) 각 그룹의 salary를 평균화해서 출력

* 예)

  ```sql
  select dept_name, count(*)
  from instructor
  group by dept_name
  ```

  * 부서를 그룹화 해서 부서 이름과 부서의 강사 수를 출력



#### Having Clause

* 튜플이 아닌 **그룹에 적용되는 조건**

* 예) **평균 급여가 42000보다 큰** 모든 부서의 이름과 평균 급여를 찾습니다.

  ```sql
  select dept_name, avg (salary)
  from instructor
  /* where dept_name != 'Physics' */
  group by dept_name
  having avg(salary) > 42000
  ```

  * 그룹을 형성하기 전에 **where** 절의 술어가 적용됩니다.
  * **having** 절의 술어는 그룹 형성 후 적용됩니다.



### Aggregation

***

* 집계 함수 외부의 select 절에 있는 속성은 목록별로 그룹화 되어야합니다.

  ```sql
  /* erroneous query */
  select dept_name, ID, avg(salary)
  from instructor
  group by dept_name;
  
  select dept_name, ID, avg(salary)
  from instructor
  group by dept_name, ID;
  ```




### Null Values and Aggregates

***

* 모든 급여 합계

  ```sql
  select sum(salary)
  from instructor
  ```

  * 위의 문은 **null 금액을 무시**합니다.
  * null이 아닌 금액이 없으면 결과는 null입니다.

* count(*)를 제외한 모든 aggregate(집계) 작업은 aggregated(집계된) 속성에서 null 값이 있는 튜플을 무시합니다.

* 컬렉션에 null 값만 있으면 어떻게 되나요?

  * count는 0을 반환합니다
  * 다른 모든 집계는 null을 반환합니다.

* 예 )

  ```sql
  create table temp (
      id varchar(8) primary key,
      salary int
  ); /* Empty relation */
  ```

  * select count (*) from temp -> 0
  * select sum(salary) from temp -> NULL

***

