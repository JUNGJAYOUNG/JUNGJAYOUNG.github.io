---
title: "Java Basic: DCL-DDL-DML"
categories:
  - Java Basic
tags:
  - Inner Class
  - JDBC
---

### 테이블 삭제
drop table 테이블이름;

### 부서 테이블 생성
create table dept(dno number, dname varchar2(20), dloc varchar2(30));

---
## 데이터베이스 명령어
1) DCL (DataBase Control Language) : 데이터 제어어
사용자계정을 생성, 권한 부여,  권한 제거
create user ~
grant ~
revoke ~

2) DDL(Database Definition Language) : 데이터 정의어
리소스(Table, View, Index...) 생성, 제거, 변경
create table ~ 
alter table ~
drop table ~

3) DML(Database Manuflation Language) : 데이터 조작어
레코드를 추가, 수정, 검색, 삭제
insert ~
select ~
update ~
delete ~

### 사용자 계정 생성하고 권한 부여하기
create user 유저이름 identified by 암호
grant 권한이름1,권한이름2,... to 유저이름

* 데이터를 추가, 수정, 삭제 한 후에는 **반드시 commit해야한다.**

# customer 테이블에 자료 추가하기
insert into customer values(1,'박지성','영국 맨체스타','010-5000-0001');
insert into customer values(2,'김연아','대한민국 서울','010-6000-0001');
insert into customer values(3,'장미란','대한민국 강원도','010-7000-0001');
insert into customer values(4,'추신수','미국 클리블랜드','010-8000-0001');
insert into customer values(5,'박세리','대한민국 대전',null);


# orders테이블에 자료 추가
insert into orders values(1,1,1,6000,'2021/11/01');

insert into orders values(3,2,5,8000,'2021/11/03');
insert into orders values(4,3,5,6000,'2021/11/03');
insert into orders values(5,4,5,20000,'2021/11/04');
insert into orders values(6,1,5,12000,'2021/11/05');
insert into orders values(7,4,5,13000,'2021/11/07');
insert into orders values(8,3,5,12000,'2021/11/07');
insert into orders values(9,2,5,7000,'2021/11/09');
insert into orders values(10,3,5,13000,'2021/11/08');

데이터베이스 명령어
(SQL - Structured Query Language)
-DCL
-DDL
-DML

## DML(데이터 조작어)
insert
select
update
delete

데이터 조작어 -> 검색(select)
==> 데이터를 조회하는 명령어를 특별히 query라고 부른다.

## select 명령어의 기본 구조

select 컬럼명1, 컬럼명2, ....
from 테이블이름
where 조건식;

## 중복을 제거하고 한번만 출력하고자 할때
distinct 키워드 사용

`select distinct publisher from book;`

### where 조건식에 사용되는 연산자들
```
비교: = > <= < <= <>
범위: between 값1 and 값2
집합: in (값2,값2,...) 	not in(값1, 값2...)
패턴: like
논리: and, or, not
null: is null, is not null
```

select * from book where price between 10000 and 20000;

출판사가 굿스포츠 혹은 대한미디어인 도서를 검색
select * from book where publisher in('굿스포츠','대한미디어');
select * from book where publisher not in('굿스포츠','대한미디어');

### like 연산자

==> 문자열 데이터에 있어 어떠한 패턴을 따르는지 검사할 때 사용
==> 예를들어 이름이 '김'으로 시작하는 데이터를 검색
혹은 도서명에 '축구'가 들어가는 데이터를 검색

like연산자와 같이 사용하는 기호
_ 모르는 하나의 글자를 대신함
% 모르는 아무글자를 대신함

select bookname, price from book where bookname like '%구%';
select * from book where bookname like '_구%';
select * from book where price>=20000 and bookname like '%축구%';
select * from book where publisher in('굿스포츠','대한미디어')
and bookname like '%축구%';

### 오름차순 정렬/내림차순 정렬
asc/desc

select 명령어 끝에 order by를 사용한다.

오름차순 정렬 order by 칼럼 [asc] <- 생략시 기본이 asc
내림차순 정렬 order by 칼럼 desc

select bookname, publisher, price 
from book 
where price between
6000 and 30000 and publisher in('이상미디어','대한미디어','굿스포츠') and
bookname like '%축구%'
order by publisher, price;
