---
title: "[DataBase] SQL 실습"
excerpt: database chapter 3 - 예제
author_profile: true
categories: 
  - database
tags:
  - database
  - study
last_modified_at: 2021-02-24T13:19:30-05:00
---



## [DataBase] SQL 실습



### 서점 데이터 (Create Table)

***

<img src="https://user-images.githubusercontent.com/60311404/108945388-dfb52380-769f-11eb-9a7e-6e24ec80b518.png" alt="CreateTAble" style="zoom: 80%;" /> 

* Book (<u>bookid</u>, bookname, publisher, price)
* Orders (<u>orderid</u>, custid, bookid, saleprice, orderdate)
* Customer (<u>custid</u>, name, address, phone)



```sql
create table Book (
    bookid int,
    bookname varchar(20),
    publisher varchar(15),
    price numeric(8,2),
    primary key (bookid));


create table Customer (
    custid int,
    name char(5),
    address varchar(20),
    phone varchar(15),
    primary key (custid));
    
    
create table Orders (
	orderid int,
    custid int,
    bookid int,
    saleprice numeric(8,2),
    orderprice varchar(20),
    primary key (orderid),
    foreign key (bookid) references Book(bookid),
	foreign key (custid) references Customer(custid));
```



### 서점 데이터 (Insert)

***

* Book Table

| bookid |     bookname      |  publisher  | price |
| :----: | :---------------: | :---------: | :---: |
|   1    |    축구의 역사    |  굿스포츠   | 7000  |
|   2    |  축구 아는 여자   |   나무수    | 13000 |
|   3    |    축구의 이해    | 대한 미디어 | 22000 |
|   4    |    골프 바이블    | 대한 미디어 | 35000 |
|   5    |     피겨 교본     |  굿스포츠   | 8000  |
|   6    |  역도 단계별기술  |  굿스포츠   | 6000  |
|   7    |    야구의 추억    | 이상미디어  | 20000 |
|   8    |   야구를 부탁해   | 이상미디어  | 13000 |
|   9    |   올림픽 이야기   |   삼성당    | 7500  |
|   10   | Olympic Champions |   Pearson   | 13000 |

* Customer Table

| **custid** | **name** |   **address**   |   **phone**   |
| :--------: | :------: | :-------------: | :-----------: |
|     1      |  박지성  |  영국 맨체스타  | 000-5000-0001 |
|     2      |  김연아  |  대한민국 서울  | 000-6000-0001 |
|     3      |  장미란  | 대한민국 강원도 | 000-7000-0001 |
|     4      |  추신수  | 미국 클리블랜드 | 000-8000-0001 |
|     5      |  박세리  |  대한민국 대전  |     NULL      |

* Order Table

| **orderid** | **custid** | **bookid** | **saleprice** | **orderdate** |
| :---------: | :--------: | :--------: | :-----------: | :-----------: |
|      1      |     1      |     1      |     6000      |  2013-07-01   |
|      2      |     1      |     3      |     21000     |  2013-07-03   |
|      3      |     2      |     5      |     8000      |  2013-07-03   |
|      4      |     3      |     6      |     6000      |  2013-07-04   |
|      5      |     4      |     7      |     20000     |  2013-07-05   |
|      6      |     1      |     2      |     12000     |  2013-07-07   |
|      7      |     4      |     8      |     13000     |  2013-07-07   |
|      8      |     3      |     10     |     12000     |  2013-07-08   |
|      9      |     2      |     10     |     7000      |  2013-07-09   |
|     10      |     3      |     8      |     13000     |  2013-07-10   |



```sql
insert into Book (bookid, bookname, publisher, price) values
	('1', '축구의 역사', '굿스포츠', 7000),
    ('2', '축구 아는 여자', '나무수', 13000),
    ('3', '축구의 이해', '대한미디어', 22000),
    ('4', '골프 바이블', '대한미디어', 35000),
 	('5', '피겨 교본', '굿스포츠', 8000),
    ('6', '역도 단계별기술', '굿스포츠', 6000),
  	('7', '야구의 추억', '이상미디어', 20000),
    ('8', '야구를 부탁해', '이상미디어', 13000),
    ('9', '올림픽 이야기', '삼성당', 7500),
 	('10', 'Olympic Champions', 'Pearson', 13000);
 	
 	
insert into Customer (custid, name, address, phone) values
    ('1', '박지성', '영국 맨체스타', '000-5000-0001'),
    ('2', '김연아', '대한민국 서울', '000-6000-0001'),
    ('3', '장미란', '대한민국 강원도', '000-7000-0001'),
    ('4', '추신수', '미국 클리블랜드', '000-8000-0001'),
    ('5', '박세리', '대한민국 대전', NULL);
    

insert into Orders (orderid, custid, bookid, saleprice, orderdate) values
	('1', '1', '1', 6000, '2013-07-01'),
    ('2', '1', '3', 21000, '2013-07-03'),
    ('3', '2', '5', 8000, '2013-07-03'),
    ('4', '3', '6', 6000, '2013-07-04'),
    ('5', '4', '7', 20000, '2013-07-05'),
    ('6', '1', '2', 12000, '2013-07-07'),
    ('7', '4', '8', 13000, '2013-07-07'),
    ('8', '3', '10', 12000, '2013-07-08'),
    ('9', '2', '10', 7000, '2013-07-09'),
    ('10', '3', '8', 13000, '2013-07-10');
```



<img src="C:\Users\wkdgm\AppData\Roaming\Typora\typora-user-images\image-20210224131132964.png" alt="BookData" style="zoom: 67%;" /> 

<img src="C:\Users\wkdgm\AppData\Roaming\Typora\typora-user-images\image-20210224131233580.png" alt="OrdersImage" style="zoom: 67%;" /> 

<img src="C:\Users\wkdgm\AppData\Roaming\Typora\typora-user-images\image-20210224131330134.png" alt="CustomerData" style="zoom:67%;" /> 





### 서점 데이터 (Select)

***

1. 모든 도서의 이름과 가격을 검색하시오

```sql
select bookname, price from Book;
```

<img src="C:\Users\wkdgm\AppData\Roaming\Typora\typora-user-images\image-20210224131547111.png" alt="selectname,price" style="zoom:67%;" /> 

2. 모든 도서의 도서번호, 도서이름, 출판사, 가격을 검색하시오

```sql
select * from Book;
```

<img src="C:\Users\wkdgm\AppData\Roaming\Typora\typora-user-images\image-20210224131640076.png" alt="selectBook" style="zoom:67%;" /> 

3. 도서 테이블에 있는 모든 출판사를 검색하시오

```sql
select publisher from Book;
```

<img src="C:\Users\wkdgm\AppData\Roaming\Typora\typora-user-images\image-20210224131717096.png" alt="publisherSelect" style="zoom:67%;" /> 

4. 가격이 20,000원 미만인 도서를 검색하시오

```sql
select * from Book where price < 20000;
```

<img src="C:\Users\wkdgm\AppData\Roaming\Typora\typora-user-images\image-20210224131753406.png" alt="BookPrice20000" style="zoom:67%;" /> 

5. 가격이 10,000원 이상 20,000 이하인 도서를 검색하시오

```sql
select * from Book where price >= 10000 and price <= 20000;
```

![SelectPrice10,20](C:\Users\wkdgm\AppData\Roaming\Typora\typora-user-images\image-20210224131844043.png)

***

