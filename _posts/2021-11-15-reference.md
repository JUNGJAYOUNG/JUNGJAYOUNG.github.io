---
title: "Java Basic: join"
categories:
  - Java Basic
tags:
  - Inner Class
  - JDBC
---
* 테이블에서 주식별자 설정
create table dept(
	dno number primary key,
	dname varchar2(20),
	dloc varchar2(30)
);

---

* 두개 이상의 속성이 합쳐져서 주식별자로 설정할 수 있다.

create table dept(
	dname varchar2(20),
	dloc varchar2(30),
	tel varchar2(30),
	manager varchar2(20),
	primary key(dname,dloc)
);
insert into dept values('영업팀','인천','032-1111-1111','홍길동');
insert into dept values('영업팀','서울','02-1111-1111','이순신');
insert into dept values('개발팀','서울','02-2222-2222','김유신');
insert into dept values('영업팀','인천','032-3333-3333','유관순');


create table dept(
	dno number primary key,
	dname varchar2(20),
	dloc varchar2(10)
);

//컬럼레벨에서 주식별자와 참조키 설정
create table emp(
	eno number primary key,
	ename varchar2(20),
	salary number,
	dno number references dept(dno)
);

//테이블레벨에서 주식별자와 참조키 설정
create table emp(
	eno number,
	ename varchar2(20),
	salary number,
	dno number,
    primary key(eno),
    foreign key(dno) references dept(dno)
);
** 참조키를 설정하는 컬럼은 반드시 부모테이블의 "주식별자"여야 한다.**

위 처럼 테이블을 생성하게 되면
두테이블은 부모 자식 관계(주종관계)가 된다.

dept 부모테이블(부모개체)
emp 자식테이블(자식개체)

부모자식관계까 설정되어있을때
부모테이블을 함부로 삭제할 수 없다.

1행에 오류:
ORA-02449: 외래 키에 의해 참조되는 고유/기본 키가 테이블에 있습니다

**부모자식관계가 설정되어있다면
자식테이블을 먼저 삭제하고 부모테이블을 삭제 할 수 있다.**

부모테이블인 dept에 레코드가 먼저 추가되어야 하고
거기에 있는 dno를 가지고 emp에 추가할 수 있다.

---
insert into dept values(10, '기획팀','서교동');
insert into dept values(20, '영업팀','서교동');
insert into dept values(30, '개발팀','판교');

insert into emp values(1000, '홍길동',500, 10);
insert into emp values(1001, '이순신',400, 20);
insert into emp values(1002, '김유신',500, 30);
insert into emp values(1003, '유관순',400, 30);

emp 테이블에서 30부서번호를 모두 10번으로 변경한다.
update emp set dno=10 where dno=30;
delete dept where dno = 30;

부모테이블에서 레코드를 삭제할때
자식테이블에서 참조하고 있는 레코드들을 연쇄하여 삭제하고자 한다면
테이블 생성시에 on delete cascade

create table emp(
	eno number,
	ename varchar2(20),
	salary number,
	dno number,
    primary key(eno),
    foreign key(dno) references dept(dno) on delete cascade
);

---

데이터베이스 명령어
1) DCL
2) DDL
	create
	alter
	drop
3) DML

---
## alter
이미 있는 테이블에 새로운 컬럼 추가
이미 있는 테이블에 컬럼 삭제
이미 있는 테이블에 칼럼의 자료형이나 제약 변경

1) 이미 있는 테이블에 새로운 컬럼 추가
`alter table 테이블이름 add 추가할칼럼이름 자료형;`

이미 레코드가 많이 있는 상태에서
컬럼을 추가한다면 그 컬럼의 값은 null인 상태가 된다.

alter table emp add phone varchar2(20);

2) 이미 있는 테이블에 컬럼 삭제
`alter table 테이블이름 drop column 컬럼이름;`

alter table emp drop column phone;


create table emp(
	eno number,
	ename varchar2(20),
	salary number,
	dno number,
    primary key(eno),
    foreign key(dno) references dept(dno) on delete cascade
);


3) 컬럼 자료형 바꾸기
alter table 테이블이름 modify 컬럼이름 새로운자료형;
dept 테이블의 dname을 varchar2(30)으로 변경
alter table dept modify dname varchar2(30);

dept 테이블의 dloc을 varchar2(50)로 벼ㄴ경
alter table dept modify dloc varchar2(50);

create table dept(
	dno number,
	dname varchar2(30),
	dloc varchar2(50)
);

4) 이미 있는 테이블의 pk설정하기
alter table 테이블명 modify 컬럼이름 자료형 not null
alter table 테이블명 add primary key(컬럼이름)

단, pk를 설정하려는 컬럼의 값이
null이거나 중복된 데이터가 있다면
이것을 처리한 후에 pk를 설정할 수 있다.

이미 있는 데이터에 중복된 값이 있으면 pk로 설정할 수 없다.
alter table dept add primary key(dno);

pk로 설정하려면 칼럼의 값들을 중복되지 않도록 처리한 후에
pk가 설정이 된다!!!!111


create table emp(
	eno varchar2(20),
	ename varchar2(20),
	dno number
);

1) eno의 자료형을 number로 수정
alter table emp **modify** eno number;

2) salary 칼럼을 추가
alter table emp **add** salary number;

3) eno에 pk를 설정
alter table emp **modify** eno number **not null**;
alter table emp **add** primary key(eno);

4) dno에 fk를 설정
alter table emp **add** foreign key(dno) references dept(dno); 


## 테이블의 구조 변경하기

- 새로운 컬럼 추가
alter table 테이블이름 add 컬럼이름 자료형 옵션
-  컬럼의 자료형 변경
alter table 테이블이름 modify 컬럼이름 새로운 자료형
- 컬럼 삭제
alter table 테이블이름 drop column 컬럼이름
- pk추가
alter table 테이블이름 add primary key(컬럼이름)
(단, 컬럼은 not null이어야 한다.)
- fk추가
alter table 테이블이름 add foreign key(컬럼이름) references 부모테이블이름(컬럼이름)

---
## 테이블 삭제하기
drop table 테이블명;
** 자식 테이블이 있으면 먼저 자식테이블을 삭제한 후에 테이블 삭제 가능

DDL 데이터 정의어
create
alter
drop

create table dept(
	dno number primary key,
	dname varchar2(20) not null,
	dloc varchar2(30) default '서교동',
	tel varchar2(30) null
);

insert into dept values(10,'기획팀','판교','031-111-1111');
insert into dept(dname,dno) values('개발팀',20);
insert into dept(dno,dloc,tel) values(30,'판교','031-2222-2222');

dname속성에는 not null로 되어있는데
이것을 생략하고 레코드를 추가할 수 없다

----
## 테이블 복사
create table 테이블이름 as select~~

create table dept100 as select * from dept;

테이블의 컬럼이름과 레코드는 복사가 되지만 제약은 복사가 되지 않는다.


### 이미 있는 테이블의 구조만 복사하여 새로운 테이블 생성
create table 테이블이름 as select * from 테이블명 where 만족하지 않을 조건;

create table dept100 as select * from dept where 1=2;

### 검색한 결과를 insert하기
insert into dept100 select * from dept;

### 자료의 수정
update 테이블이름 set 컬럼1=값1, ... where 

update customer set address = '대한민국 부산' where custid=5;

conn c##madang/madang

박세리 고객의 주소를 김연아와 동일하게 수정
(서브쿼리 이용)

select address from customer where name='김연아'

update customer set address=(select address from customer where name='김연아') where name='박세리';

---
## 자료의 삭제
delete from 테이블이름 [where 조건식]

delete from customer where custid = 5;

delete from customer where custid = 1
*
1행에 오류:
ORA-02292: 무결성 제약조건(C##MADANG.SYS_C008320)이 위배되었습니다- 자식
레코드가 발견되었습니다

1번고객의 구매내역이 자식테이블의 레코드에 존재하기 때문에 삭제 불가

**헷갈리지 않게 주의~!**
drop table 테이블명;
:테이블 자체 삭제
:delete from 테이블명;
레코드 삭제

insert, update, delete를 수행한 후에는

commit
rollback으로 명령어의 적용을 해줘야 한다.

commit 승인
rollback 취소

insert into dept values(30,'영업팀','서교동','010-1111-1111');

DML 작업을 수행한 후에는 반드시
COMMIT 또는
ROLLBACK을 해줘야한다.

---
DDL, DCL은 auto commit이다.
바로 적용 됨.


create table 극장(극장번호 number, 극장이름 varchar2(20), 위치 varchar2(20), primary key(극장번호));

create table 상영관(
	극장번호 number,
	상영관번호 number,
	영화제목 varchar2(50),
	가격 number,
	좌석수 number,
	primary key(극장번호,상영관번호),
	foreign key(극장번호) references 극장(극장번호)
);

create table 고객(
	고객번호 number,
	이름 varchar2(20),
	주소 varchar2(50),
	primary key(고객번호)
);

create table 예약(
	극장번호 number,
	상영관번호 number,
	고객번호 number,
	좌석번호 number,
	날짜 date,
	primary key(극장번호,상영관번호,고객번호),
	foreign key(극장번호,상영관번호) references 상영관(극장번호,상영관번호),
	foreign key(고객번호) references 고객(고객번호)
);

insert into 극장 values(1,'롯데','잠실');
insert into 극장 values(2,'메가','강남');
insert into 극장 values(3,'대한','잠실');

insert into 상영관 values(1,1,'어려운 영화',15000,48);
insert into 상영관 values(3,1,'멋진 영화',7500,120);
insert into 상영관 values(3,2,'재밌는 영화',8000,110);

insert into 고객 values(3,'홍길동','강남');
insert into 고객 values(4,'김철수','잠실');
insert into 고객 values(9,'박영희','강남');

insert into 예약 values(3,2,3,15,'2014-09-01');
insert into 예약 values(3,1,4,16,'2014-09-01');
insert into 예약 values(1,1,9,48,'2014-09-01');

column 극장번호 format 9999;
column 상영관번호 format 9999;
column 고객번호 format 9999;
column 가격 format 999,999;
column 좌석번호 format 9999;

select 극장이름, 위치 from 극장;
select 극장이름 from 극장 where 위치='잠실';
select 이름 from 고객 where 주소 like '%잠실%' order by 이름;

select 극장번호, 상영관번호, 영화제목
from 상영관
where 가격<=8000;

**어려움 **
select 이름
from 고객,극장,상영관,예약
where 고객.고객번호 = 예약.고객번호 and
극장.극장번호 = 상영관.극장번호 and
상영관.상영관번호 = 예약.상영관번호 and
상영관.극장번호 = 예약.극장번호 and
고객.주소 = 극장.위치;

select count(*) from 극장;

select avg(가격) from 상영관;

select count(*) from 예약
where 날짜 = '2014/09/01';

부속질의와 조인


select 극장번호
from 극장
where 극장이름='대한';

select 영화제목
from 상영관
where 극장번호=(select 극장번호
from 극장
where 극장이름='대한');

select 극장번호
from 극장
where 극장이름='대한';

select 고객번호
from 예약
where 극장번호=(select 극장번호
from 극장
where 극장이름='대한');

select 이름
from 고객
where 고객번호 in (select 고객번호
from 예약
where 극장번호=(select 극장번호
from 극장
where 극장이름='대한'));

- 대한 극장의 전체 수입을 출력
극장테이블과 상영관 테이블을 조인하여 '대한'극장 상영하는 영화의 가격을 검색

** 대한극장에 상영하는 영화별 가격을 출력

극장번호와 상영관번호 쌍으로 해당 영화라는걸 알 수 있으므로 
영화별이고 해서
꼭 group by가 들어가야만 하는것은 아니다.
**group by는 select 문에 그룹함수가 필요할때 쓴다.**


select 상영관.극장번호, 상영관번호, 가격
from 극장, 상영관
where 극장.극장번호 = 상영관.극장번호 and 
극장이름 = '대한';

극장번호 상영관번호     가격
-------- 	---------- -	-------
   3         	1    		7,500
   3         	2    		8,000

** 대한극장에서 상영하는 영화별 예매건수를 출력

select 상영관.극장번호, 상영관.상영관번호, count(*) n 
from 극장, 상영관, 예약
where 극장.극장번호 = 상영관.극장번호 and 
상영관.극장번호 = 예약.극장번호 and 
상영관.상영관번호 = 예약.상영관번호 and 
극장이름 = '대한' 
group by 상영관.극장번호, 상영관.상영관번호;


극장번호 상영관번호          N
-------- ---------- ----------
   3          1          1
   3          2          1

select sum(가격*n)
from (select 상영관.극장번호, 상영관번호, 가격
from 극장, 상영관
where 극장.극장번호 = 상영관.극장번호 and 
극장이름 = '대한'
) a, (select 상영관.극장번호, 상영관.상영관번호, count(*) n 
from 극장, 상영관, 예약
where 극장.극장번호 = 상영관.극장번호 and 
상영관.극장번호 = 예약.극장번호 and 
상영관.상영관번호 = 예약.상영관번호 and 
극장이름 = '대한' 
group by 상영관.극장번호, 상영관.상영관번호) b
where a.극장번호 = b.극장번호 and
a.상영관번호 = b.상영관번호; 






select sum(가격*n) 
from (select 상영관.극장번호, 상영관번호, 가격
from 극장, 상영관
where 극장.극장번호 = 상영관.극장번호 and 
극장이름 = '대한') a, (select 상영관.극장번호, 상영관.상영관번호, count(*) n 
from 극장, 상영관, 예약
where 극장.극장번호 = 상영관.극장번호 and 
상영관.극장번호 = 예약.극장번호 and 
상영관.상영관번호 = 예약.상영관번호 and 
극장이름 = '대한' 
group by 상영관.극장번호, 상영관.상영관번호) b
where a.극장번호  = b.극장번호 and 
a.상영관번호 = b.상영관번호
	
 SUM(가격*N)
 -----------
      15500