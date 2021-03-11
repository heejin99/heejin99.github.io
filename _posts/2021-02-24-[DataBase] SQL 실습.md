---
title: "[DataBase] SQL 실습"
excerpt: database chapter 3 - 예제
author_profile: true
toc: true
toc_sticky: true
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

<img src="https://user-images.githubusercontent.com/60311404/109960943-b4c87080-7d2c-11eb-9d16-447e70be0edf.png" alt="image-20210224131132964" style="zoom:67%;" /> 

<img src="https://user-images.githubusercontent.com/60311404/109961041-d0337b80-7d2c-11eb-91b7-efa79c042445.png" alt="image-20210224131233580" style="zoom:67%;" /> 

 <img src="https://user-images.githubusercontent.com/60311404/109961087-dcb7d400-7d2c-11eb-8a03-76958f9d3446.png" alt="image-20210224131330134" style="zoom:67%;" />





### 서점 데이터 (Select)

***

1. 모든 도서의 이름과 가격을 검색하시오

```sql
select bookname, price from Book;
```

<img src="https://user-images.githubusercontent.com/60311404/109961119-e8a39600-7d2c-11eb-8181-07806dc11299.png" alt="image-20210224131547111" style="zoom:67%;" /> 

2. 모든 도서의 도서번호, 도서이름, 출판사, 가격을 검색하시오

```sql
select * from Book;
```

<img src="https://user-images.githubusercontent.com/60311404/109961132-eb9e8680-7d2c-11eb-98bd-d382d3904219.png" alt="image-20210224131640076" style="zoom:67%;" /> 

3. 도서 테이블에 있는 모든 출판사를 검색하시오

```sql
select publisher from Book;
```

<img src="https://user-images.githubusercontent.com/60311404/109961196-0113b080-7d2d-11eb-8f01-b9b5eb8001ae.png" alt="image-20210224131717096" style="zoom:67%;" /> 

4. 가격이 20,000원 미만인 도서를 검색하시오

```sql
select * from Book where price < 20000;
```

<img src="https://user-images.githubusercontent.com/60311404/109961211-05d86480-7d2d-11eb-98ee-7619ae40862b.png" alt="image-20210224131753406" style="zoom: 67%;" /> 

5. 가격이 10,000원 이상 20,000 이하인 도서를 검색하시오

```sql
select * from Book where price >= 10000 and price <= 20000;
```

<img src="https://user-images.githubusercontent.com/60311404/109961281-1b4d8e80-7d2d-11eb-9a35-c7bf92e973a5.png" alt="image-20210224131844043" style="zoom:67%;" /> 



### 서점 데이터 (Join)

***

6. 고객과 고객의 주문에 관한 데이터를 모두 보이시오.

```sql
select * from customer, orders where customer.custid = orders.custid;
```

![image-20210304181355364](https://user-images.githubusercontent.com/60311404/109961818-ca8a6580-7d2d-11eb-962a-f00bd8a35588.png)

7. 고객의 이름과 고객이 주문한 도서의 가격을 검색하시오.

   <img src="https://user-images.githubusercontent.com/60311404/109961827-ccecbf80-7d2d-11eb-9019-ce8562fe1bf2.png" alt="image-20210304181525427" style="zoom: 80%;" /> 

8. 고객의 이름과 고객이 주문한 도서의 이름을 구하시오.

```sql
select customer.name, book.bookname 
from customer, book, orders
where customer.custid = orders.custid and orders.bookid = book.bookid;
```

<img src="https://user-images.githubusercontent.com/60311404/109961835-ceb68300-7d2d-11eb-9df1-7d8662ade9b7.png" alt="image-20210304181717572" style="zoom:80%;" />  

9. 가격이 20,000원인 도서를 주문한 고객의 이름과 도서의 이름을 구하시오.

```sql
select customer.name, book.bookname
from customer, book, orders
where customer.custid = orders.custid 
	and orders.bookid = book.bookid 
	and book.saleprice = 20000;
```

<img src="https://user-images.githubusercontent.com/60311404/109961843-d0804680-7d2d-11eb-8f60-956140ad4c35.png" alt="image-20210304181916680" style="zoom:80%;" /> 



### 서점 데이터(Orderby)

***

10. 고객과 고객의 주문에 관한 데이터를 고객별로 정렬하여 보이시오.

```sql
select * from customer, orders
where customer.custid = orders.custid
order by customer.custid;
```

![image-20210304203643558](https://user-images.githubusercontent.com/60311404/109962157-3371dd80-7d2e-11eb-9bce-8b8100dfc4ac.png)  

11. 도서이름에 '축구'가 포함된 출판사를 검색하시오.

```sql
select bookname, publisher from book
where bookname like '%축구%';
```

<img src="https://user-images.githubusercontent.com/60311404/109962165-35d43780-7d2e-11eb-9eba-6cd1d6eeba19.png" alt="image-20210304204153137" style="zoom:80%;" /> 

12. 도서이름 왼쪽 두 번째 위치에 ‘구’라는 문자열을 갖는 도서를 모두 검색하시오.

```sql
select * from book
where bookname like '_구%';
```

<img src="https://user-images.githubusercontent.com/60311404/109962172-379dfb00-7d2e-11eb-9be9-8339ab624b19.png" alt="image-20210304204418257" style="zoom:80%;" /> 

13. 출판사가 '굿스포츠' 혹은 '대한미디어'인 도서를 검색하시오.

```sql
select * from book
where publisher='굿스포츠' or publisher = '대한미디어';
```

<img src="https://user-images.githubusercontent.com/60311404/109962175-38cf2800-7d2e-11eb-95eb-6b560cf89e4f.png" alt="image-20210304204816579" style="zoom:80%;" />  

14. 도서를 이름순으로 검색하시오.

```sql
select * from book
order by bookname;
```

<img src="https://user-images.githubusercontent.com/60311404/109962180-3a98eb80-7d2e-11eb-949f-edc9d4be3e36.png" alt="image-20210304205114702" style="zoom:80%;" />  

15. 도서를 가격의 내림차순으로 검색하시오. 만약 가격이 같다면 출판사의 오름차순으로 검색한다.

```sql
select * from book
order by price desc, publisher asc;
```

<img src="https://user-images.githubusercontent.com/60311404/109962186-3bca1880-7d2e-11eb-9d68-f06c96607d16.png" alt="image-20210304205319121" style="zoom:80%;" /> 



### 서점 데이터(As)

***

16. 고객이 주문한 도서의 총 판매액을 구하시오.

```sql
select sum(saleprice) as '총 판매액'
from orders;
```

<img src="https://user-images.githubusercontent.com/60311404/110235010-1b3dd080-7f71-11eb-867c-443944aaf7f5.png" alt="image" style="zoom:80%;" /> 

17. 2번 김연아 고객이 주문한 도서의 총 판매액을 구하시오

```sql
select sum(saleprice) as '총 매출'
from orders where custid = 2;
```

<img src="https://user-images.githubusercontent.com/60311404/110235079-78398680-7f71-11eb-89a9-78602ceed2f2.png" alt="image" style="zoom:80%;" /> 

18. 고객이 주문한 도서의 총 판매액, 평균값, 최저가, 최고가를 구하시오.

```sql
select sum(saleprice) as Total,
avg(saleprice) as Average,
min(saleprice) as Minimum,
max(saleprice) as Maximum
from orders;
```

<img src="https://user-images.githubusercontent.com/60311404/110235176-fdbd3680-7f71-11eb-92da-acc6639a1d81.png" alt="image" style="zoom:80%;" /> 

19. 마당서점의 도서 판매 건수를 구하시오.

```sql
select count(*) as '판매 건수' from orders;
```

<img src="https://user-images.githubusercontent.com/60311404/110235244-4d9bfd80-7f72-11eb-957e-361afabaf122.png" alt="image" style="zoom:80%;" /> 

20. 고객별로 주문한 도서의 총 슈량과 총 판매액을 구하시오.

```sql
select custid, count(*) as '도서 수량', sum(saleprice) as '총 액'
from orders
group by custid;
```

<img src="https://user-images.githubusercontent.com/60311404/110235279-889e3100-7f72-11eb-881a-1f548390a057.png" alt="image" style="zoom:80%;" /> 

21. 가격이 8000원 이상인 도서를 구매한 고객에 대하여 고객별 주문 도서의 총 수량을 구하시오. 단, 2권 이상 구매한 고객만 구한다.

```sql
select custid, count(*) as '도서 수량'
from orders where saleprice >= 8000
group by custid having count(*) >= 2;
```

<img src="https://user-images.githubusercontent.com/60311404/110235388-1548ef00-7f73-11eb-858a-c7be3218650d.png" alt="image" style="zoom:80%;" /> 

***

