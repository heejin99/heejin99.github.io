---
title: "[DataBase] SQL Nested SubQuries"
excerpt: database chapter 3
author_profile: true
toc: true
toc_sticky: true
categories: 
  - database
tags:
  - database
  - study
last_modified_at: 2021-03-11T16:47:30-05:00
---



## [DataBase] SQL Nested Subqueries



### Nested Subquries

***

* SQL은 서브 쿼리의 중첩을 위한 메커니즘을 제공합니다.
* **서브 쿼리(Subqueries)**는 다른 쿼리 내에 중첩된 **select-from-where** 식입니다.
  * 서브쿼리: Select문 안에 Select문
  * 반드시 괄호가 들어가야합니다.

```sql
select distinct course_id from section
where semester = 'Fall' and year = 2009 and /* Outer query */
	course_id in (select cousre_id
                 from section
                 where semester = 'Spring' and year = 2010); 
```

* 서브 쿼리의 일반적인 용도는
  * 멤버 자격 설정
  * 비교 설정 및 카디널리티 설정에 대한 테스트 수행

#### 서브 쿼리의 종류

1. 서브 쿼리 위치

   * 중첩 서브쿼리 (Nested Subquery) : where절에 subquery 위치
   * 파생 관계 (Derived Relations) : from 절에 subquery 위치
   * 스칼라 서브쿼리 (Scalar Subquery) : select절에 subquery 위치

2. 중첩 서브 쿼리 (서브쿼리 반환)

   * 단일 행 서브쿼리 (Single Row Subquery)

     : 하나의 컬럼으로 구성된 조회 결과 행 하나를 outer 쿼리에 반환

   * 다중 행 서브쿼리 (Multiple Row Subquery) 

     : in, any, all, exists 등의 연산자로 얻은 서브쿼리 결과 여러개의 행을 outer 쿼리에 반환

   * 다중 컬럼 서브 쿼리 (Multiple Column Subquery)

     : 서브쿼리 결과 여러개의 행을 outer 쿼리에 반환하는데 where 또는 having in 연산자 사이에 컬럼 리스트가 괄호로 묶여 있어야 한다.

3. 서브 쿼리가 파싱되는 관점

   * Simple Subquery

     : 각 테이블에 대해서 한 번 평가되는 쿼리

   * 상관 서브 쿼리 (Correlated Subquery)

     : 중첩 서브 쿼리의 한 종류로 테이블 단위가 아닌 각 행에 대해 한 번 평가된다.

     

#### Nested Subquries

예) section(<u>course_id</u>, <u>sec_id</u>, <u>semester</u>, <u>year</u>, building, room_number, time_slot_id)

<img src="https://user-images.githubusercontent.com/60311404/110095659-7be9d380-7de0-11eb-9170-1abeea6a8f05.png" alt="image" style="zoom:80%;" /> 



* 2009년 가을과 2010년 봄에 제공된 courses(과정)을 찾아라

```sql
select distinct course_id
from section
where semester = ’Fall’ and year= 2009 and
	course_id in (select course_id
                  from section
                  where semester = ’Spring’ and year= 2010);
```

```sql
/* == */
(select course_id from section 
 where semester = ‘Fall’ and year = 2009)
 intersect
 (select course_id from section
  where semester = ‘Spring’ and year = 2010)
```

```sql
/* ==> */
select distinct course_id
from section
where semester = ’Fall’ and year= 2009 and
course_id in ('CS-101', 'CS-315', 'CS-319', 'CS-319',
              'FIN-201', 'HIS-351', 'MU-199');
```



* 2009년 가을에는 제공되고 2010년 봄에는 제공되지 않은 courses(과정)을 찾아라

```sql
select distinct course_id
from section
where semester = ’Fall’ and year= 2009 and
	course_id not in (select course_id
                  from section
                  where semester = ’Spring’ and year= 2010);
```

```sql
/* == */
(select course_id from section 
 where semester = ‘Fall’ and year = 2009)
 except
 (select course_id from section
  where semester = ‘Spring’ and year = 2010)
```



*  ID 10101을 가진 instructor(강사)가 가르친 course(과정)을 듣는 학생들의 전체 수를 찾으세요

```sql
select count (distinct ID)
from takes
where (cousre_id, sec_id, semester, year) in
(select cousre_id, sec_id, semester, year 
 from teaches 
 where teaches.ID = 10101);
```



#### in / not in

* **in** connective

```sql
select distinct course_id from section
where semester = 'Fall' and year = 2009 and
	course_id in ('BIO-101', 'CS-101', 'CS-190'); 
```

```sql
/* ---> */
select distinct course_id from section
where semester = 'Fall' and year = 2009 and
	(cousre_id = 'BIO-101' or
    course_id = 'CS-101' or
    course_id = 'CS-190');
```

* **not in** connective

```sql
select distinct course_id from section
where semester = 'Fall' and year = 2009 and
	course_id not in ('BIO-101', 'CS-101', 'CS-190'); 
```

```sql
/* ---> */
select distinct course_id from section
where semester = 'Fall' and year = 2009 and
	(cousre_id != 'BIO-101' and
    course_id != 'CS-101' and
    course_id != 'CS-190'); /* Not equal(!=) */
```



#### Definition of All Clause

* all : 값을 서브 쿼리에 의해 리턴되는 모든 값과 조건값을 비교하여 모든 값을 만족해야만 참

* 예) 부서 이름이 Physics인 강사의 급여보다 많이 받는 강사의 이름을 모두 출력하시오.

  <img src="https://user-images.githubusercontent.com/60311404/110764293-36248380-8296-11eb-852a-d2ff238bb713.png" alt="image" style="zoom:80%;" /> 

  ```sql
  select name
  from instructor
  where salary > all (select salary
                       from instructor
                       where dept_name = 'Physics');
  ```

  * 부서 이름이 'Physics'인 강사의 급여는 87000, 95000원인데 여기서 95000원보다 많은 사람들의 이름을 출력합니다.



#### Definition of Some Clause

* some : 서브 쿼리에 의해 리턴되는 각각의 값과 조건을 비교하여 하나 이상을 만족하면 참

* 예) 부서 이름이 Physics인 강사의 급여보다 많이 받는 강사의 이름을 출력하시오.

  ```sql
  select distinct T.name
  from instructor as T, instructor as S
  where T.salary > S.salary and S.dept_name = 'Physics';
  ```

  ```sql
  /* == */
  select name
  from instructor
  where salary > some (select salary
                       from instructor
                       where dept_name = 'Physics');
  ```

  * Physics 부서의 강사 급여는 87000과 95000원인데 급여가 85000보다 많거나 95000보다 많으면 출력될 수 있습니다.



#### Exists / Not Exists

* **Exists** : exists안의 조건이 **존재**할 때 전체 결과를 출력해라.

```sql
select cousre_id
from section as S
where semester = 'Fall' and year = 2009 and
	exists ( select *
             from section as T
             where semester = 'Sprint' and 
            	year = 2010 and
            	S.cousre_id = T.course_id);
```

* **Not Exists** : not exist안의 조건이 **존재 하지 않을 때**만 전체 결과를 출력해라.

```sql
select cousre_id
from section as S
where semester = 'Fall' and year = 2009 and
	not exists ( select *
                 from section as T
             	 where semester = 'Sprint' and
                 	year = 2010 and
            		S.cousre_id = T.course_id);
```



#### Correlated subquery

: 내부 subquery에서 외부 테이블의 값을 참조할 때 사용

: Outer query에서 읽어온 행을 가지고 내부 쿼리를 실행하는 것을 반복하여 결과를 출력한다.

* 예) 2009 년 가을 학기와 2010 년 봄 학기에 가르친 모든 과정을 찾아보십시오.

  

#### Derived Relations

* Derived Relations(파생 관계) : SQL을 사용하면 from 절에서 서브 쿼리 표현식을 사용할 수 있습니다.
* 예) 평균 연봉이 75000원 이상인 부서의 평균 강사 연봉을 찾으십시오.

```sql
select dept_name, avg_salary
from (select dept_name, avg (salary) as avg_salary
      from instructor
      group by dept_name) /* Derived Relation */
where avg_salary > 75000;
```

* 예) 각 부서의 평균 급여의 모든 부서에서 최대 값 찾기

```sql
select max(dept_avg.avg_salary)
from (select dept_name, avg(salary) as avg_salary
      from instructor
      group by dept_name) as dept_avg;
```



#### Scalar Subquery

* Scalar Subquery : **단일 속성을 포함하는 하나의 튜플만 반환**합니다.

```sql
select dept_name, (select count(*)
                   from instructor)
                   as num_instructors
from department; /* scalar subquery */
```

```sql
select dept_name, (select count(*)
                   from instructor
                   where department.dept_name = instructor.dept_name)
                   as num_instructors /* correlated Scalar subquery */
from department; 
```

