---
title: "[DataBase] SQL"
excerpt: database chapter 3
author_profile: true
categories: 
  - database
tags:
  - database
  - study
last_modified_at: 2021-02-18T21:09:30-05:00
---



## [DataBase] SQL



### SQL Data Definition

***

#### 1. Data-definition language (DDL)

* **Defining relation schema**
* **Deleting relation**

* **Modifying relation schema**



### C++ vs. SQL

***

* C++

  ```c++
  struct department {
        char dept_name [20];      
        char building[15];
        int    budget;
  };
  ```

* SQL

  ```sql
   create table department(
       dept_name  char(20),
       building   char(20),     
       budget     int
  };
  ```



### Basic Types in SQL(1)

***

* **char(n).**
  * 사용자 지정 길이가 n인 고정 길이 문자열

* **varchar(n).**
  * 사용자 지정 최대 길이가 n인 가변 길이 문자열

* **int.**
  * 정수 (기계 종속적인 정수의 유한 서브 세트)

* **smallint.**
  * 작은 정수(정수 도메인 유형의 기계 종속 서브 세트)
* **numeric(d, p).**
  * 사용자 지정 정밀도 p 자리, d 자리의 고정 소수점 번호
    * 예) numeric (3, 1)
    * numeric(전체길이(소수점 이하 포함), 소수점 이하 길이)

* **real, double precision**
  * 기계 종속 정밀도를 갖는 부동 소수점 및 배정 밀도 부동 소수점 숫자




#### Char vs. Varchar

* char(10)

  ![char](https://user-images.githubusercontent.com/60311404/108356644-b9226300-722f-11eb-8eb0-c4578d9661f6.png) 

* vchar(10)

  ![varchar](https://user-images.githubusercontent.com/60311404/108356654-bc1d5380-722f-11eb-8a2e-6426c57e5339.png) 



### Create Table Construct

***

* SQL 관계는 **create table** 명령을 사용하여 정의됩니다.

  **create table** r (A<sub>1</sub>   D<sub>1</sub>,					-> attributes

  ​						    A<sub>2</sub>   D<sub>2</sub>,

  ​						  .  ............,

  ​						    (integrity-constraint<sub>1</sub>),		-> integrity constraints

  ​						     ...												(무결성 제약 조건)

  ​						    (integrity-constraint<sub>k</sub>));

  * r은 관계(relation)의 이름
  * 각 A<sub>i</sub> 는 관계 r의 스키마에 있는 속성 이름
  * D<sub>i</sub>는 속성 A<sub>i</sub>의 도메인에 있는 값의 데이터 유형

* 예시)

  **create table** *instructor* (

  ​						*ID*			  	char(5),

  ​						*name*	   	  varchar(20),

  ​						*dept_name*	varchar(20),

  ​						*salary*		     numeric(8,2));



### Insert Statement

***

* **insert into** *instructor* **values** ('10211', 'Smith', 'Biology', 66000);
* **insert into** *instructor* **values** ('10212', 'Kim', 'Biology', 76000);



### Alter Table

***

* **alter table** *r* **add** *A D*
  * A는 관계 r에 추가할 속성의 이름
  * D는 A의 도메인
  * 관계의 모든 튜플에는 새 속성의 값으로 null이 할당됩니다.
  * 예) **alter table** *instructor* **add** monthly_salary numeric(8,2)
* **alter table** *r* **drop** *A*
  * A는 관계 r의 속성의 이름
  * 많은 데이터베이스에서 지원하지않는 속성 삭제
  * 예) **alter table** *instructor* **drop** salary



### Drop Table

***

* **drop table** *r*
  * r의 모든 튜플 및 스키마 삭제
* **delete from** *r*
  * r의 모든 튜플을 삭제하고 관계 r을 유지합니다.



### Integrity Constraints

***

```sql
create table instructor (
     ID        char(5),
     name      varchar(20) not null,
     dept_name varchar(20),
     salary    numeric(8,2),
     primary key (ID),
     foreign key (dept_name) references department(dept_name));
```

* **not null**

  * 해당 속성에는 null 값이 허용 되지않습니다.
  * **insert into** *instructor* **values** (‘10212’, **null**, ’Biology’, 66000); -> **ERROR**

* **primary key** (*A*1, ..., *A<sub>n</sub>* )

  * 속성에 대한 기본 키 선언은 null이 아니고 고유하지않도록 합니다

  * **insert into** *instructor* **values** (**null**, ‘Smith’, ’Biology’, 66000); -> **ERROR**

    **insert into** *instructor* **values** (‘**10211**’, ‘Kim’, ’Physics’, 91000); -> **ERROR**

  * ```sql
    create table instructor (
         ID        char(5) PRIMARY KEY,
         name      varchar(20) not null,
         dept_name varchar(20),
         salary    numeric(8,2),
         foreign key (dept_name) references department(dept_name));
    ```

* **foreign key** (*A*<sub>m</sub>, ..., *A<sub>n</sub>* ) **references** *r*

  <img src="https://user-images.githubusercontent.com/60311404/108362718-72d10200-7237-11eb-8245-a31800b5e881.png" alt="foreignkey" style="zoom: 67%;" /> 

  * **insert into** *instructor* **values** (‘99999’, ’JW KIM’, ’**Industrial Engineering**’, 65000);

    -> 'Industrial Engineering'이 department relation에 존재해야합니다.

    -> department relation에 없으면 **Error**

***

