---
title: "SQL: sql exercise"
categories:
  - Java Basic
tags:
  - Inner Class
  - JDBC
---

- 극장별 상영관 수를 출력
극장별이니까 극장 이름 출력 필요 ->극장 테이블 조인 필요

select 극장이름, count(*) 상영관수
from 상영관, 극장
where 상영관.극장번호 = 극장.극장번호
group by 극장이름;

- '잠실'에 있는 극장의 상영관를 출력

1) 잠실에 있는 극장의 극장번호
select 극장번호
from 극장
where 위치='잠실';
2) 잠실에 있는 극장의 상영관 정보 출력
select *
from 상영관
where 극장번호 in (select 극장번호
from 극장
where 위치 ='잠실');

**- 2014년 9월 1일의 극장별 평균 관람 고객 수를 출력**
극장별 평균 관람 고객수
: '대한'극장에서 상영하는 영화가 A,B,C 상영된다고 가정하자.
A 10
B 10
C 10
만약 대한극장에서 상영하는 영화의 수가 3개이고 각 영화별 관람고객수가 위와 같다면
이 극장의 9월 1일날 평균 관람고객수는 10이 된다.

1) 2014년 9월 1일 날짜에 대한극장에서 상영하는 상영관의 수 cnt
2) 2014년 9월 1일의 대한극장의 총 관람수				sum
-> 2014년 9월 1일의 대한극장의 평균관람 고객수 sum/cnt

select count(distinct 상영관.상영관번호) cnt
from 극장, 상영관, 예약
where 극장.극장번호 = 상영관.극장번호 and
상영관.극장번호 = 예약.극장번호 and
상영관.상영관번호 = 예약.상영관번호 and
날짜 = '2014/09/01' and
극장이름='대한';	=> A

select count(*) sum
from 극장, 상영관, 예약
where 극장.극장번호 = 상영관.극장번호 and
상영관.극장번호 = 예약.극장번호 and
상영관.상영관번호 = 예약.상영관번호 and
날짜 = '2014/09/01' and
극장이름='대한'; => B

select B.sum/A.cnt
from () A, () B

select count(*)/count(distinct 상영관.상영관번호)
from 극장, 상영관, 예약
where 극장.극장번호 = 상영관.극장번호 and
상영관.극장번호 = 예약.극장번호 and
상영관.상영관번호 = 예약.상영관번호 and
날짜 = '2014/09/01' and
극장이름='대한';

insert into 예약 values(3,2,9,17,'2014/09/01');
insert into 고객 values(1,'윤태인','운정');
insert into 고객 values(2,'임상진','잠실');
insert into 예약 values(3,2,1,18,'2014/09/01');
insert into 예약 values(3,2,2,19,'2014/09/01');


**- 2014년 9월 1일에 가장 많은 고객이 관람한 영화를 출력**

1)2014년9월1일 날짜에 영화별로 관람수를 출력
select 영화제목, count(*)
from 극장, 상영관, 예약
where 극장.극장번호 = 상영관.극장번호 and
상영관.극장번호 = 예약.극장번호 and
상영관.상영관번호 = 예약.상영관번호 and
날짜 = '2014/09/01'
group by 영화제목;


select max(count(*))
from 극장, 상영관, 예약
where 극장.극장번호 = 상영관.극장번호 and
상영관.극장번호 = 예약.극장번호 and
상영관.상영관번호 = 예약.상영관번호 and
날짜 = '2014/09/01'
group by 영화제목;

select 영화제목, count(*)
from 극장, 상영관, 예약
where 극장.극장번호 = 상영관.극장번호 and
상영관.극장번호 = 예약.극장번호 and
상영관.상영관번호 = 예약.상영관번호 and
날짜 = '2014/09/01'
group by 영화제목
having count(*)  = (select max(count(*))
from 극장, 상영관, 예약
where 극장.극장번호 = 상영관.극장번호 and
상영관.극장번호 = 예약.극장번호 and
상영관.상영관번호 = 예약.상영관번호 and
날짜 = '2014/09/01'
group by 영화제목);

- 각테이블에 데이터를 삽입하는 insert문을 하나씩 

insert into 극장 values(4,'쌍용','홍대');
insert into 상영관 values(4,2,'재미있는 오라클',10000,14);
insert into 고객 values(5,'박성미','홍대');
insert into 예약 values(4,2,5,2,sysdate);
insert into 예약 values(3,2,5,1,'2021/11/16');

select 영화제목, 극장이름, 좌석번호
from 극장,상영관,예약, 고객
where 극장.극장번호 = 상영관.극장번호 and
상영관.극장번호 = 예약.극장번호 and
상영관.상영관번호 = 예약.상영관번호 and
예약.고객번호 = 고객.고객번호 and
이름='박성미' and
날짜='2021/11/16';

**sysdate으로 insert한 레코드는 출력되지 않는다.
==> sysdate에는 날짜뿐아니라 시,분,초에 대한 정보도 같이 관리되고 있어서
시,분,초가 정보가 달라서 검색이 되지 않는다.
to_char(날짜,'yyyy/mm/dd')**

select 영화제목, 극장이름, 좌석번호
from 극장,상영관,예약, 고객
where 극장.극장번호 = 상영관.극장번호 and
상영관.극장번호 = 예약.극장번호 and
상영관.상영관번호 = 예약.상영관번호 and
예약.고객번호 = 고객.고객번호 and
이름='박성미' and
**to_char(날짜,'yyyy/mm/dd')='2021/11/16';**


- 영화의 가격을 10%씩 인상
update 상영관 set 가격=가격*1.1;

새로 추가할 주문의 주문번호는
select max(orderid) +1 from orders;

jsp파일에서는 form이 있는 jsp파일에서 실행해야 한다.

- 대한 극장에서 오늘 날짜에 상영하는 상영관정보를 모두 출력

select 상영관.극장번호, 상영관.상영관번호, 영화제목, 가격, 좌석수
from 극장, 상영관, 예약
where 극장.극장번호 = 상영관.극장번호 and
상영관.극장번호 = 예약.극장번호 and
상영관.상영관번호 = 예약.상영관번호 and
극장이름='대한' and
to_char(날짜,'yyyy/mm/dd')= to_char(sysdate,'yyyy/mm/dd');

극장번호 상영관번호 영화제목            			가격     			좌석수
--------	 ---------- 	--------------- -			-------			 ----------
       3          2 재밌는 영화        8,000        110
       3          3 즐거운 자바        9,000        100
       3          3 즐거운 자바        9,000        100
       3          3 즐거운 자바        9,000        100

예약테이블에서
극장번호와 상영관번호가 합쳐져서 중복되지 않도록검색

select distinct 극장번호, 상영관번호 from 예약
where to_char(날짜,'yyyy/mm/dd')=to_char(sysdate,'yyyy/mm/dd');
  극장번호 상영관번호
	---------- ----------
         4          2
         3          2
         3          3			=>A

- 상영관 테이블로부터 극장번호와 상영관번호가 합쳐져서 A에 해당하는 레코드를 검색
select * from 상영관
where (극장번호, 상영관번호) in (select distinct 극장번호, 상영관번호 from 예약
**where to_char(날짜,'yyyy/mm/dd')=to_char(sysdate,'yyyy/mm/dd'));**

select 상영관.극장번호,상영관.상영관번호,영화제목,가격,좌석수 from 상영관, 극장
where (상영관.극장번호, 상영관번호) in (select distinct 극장번호, 상영관번호 from 예약
where to_char(날짜,'yyyy/mm/dd')=to_char(sysdate,'yyyy/mm/dd')) and
상영관.극장번호 = 극장.극장번호 and
극장이름='대한';

insert into 상영관 values(3,3,'즐거운 자바',9000,100);
insert into 예약 values(3,3,1,1,sysdate);
insert into 예약 values(3,3,2,2,sysdate);
insert into 예약 values(3,3,3,3,sysdate);
insert into 예약 values(3,2,9,1,sysdate);
insert into 예약 values(3,2,1,2,sysdate);

대한극장의 오늘날짜의 총수익 출력
1)대한극장의 상영관별 금액과 예약건수를 출력
select 극장번호, 상영관번호, count(*)
from 예약
where to_char(날짜,'yyyy/mm/dd')=to_char(sysdate,'yyyy/mm/dd') and
극장번호 = (select 극장번호 from 극장 where 극장이름 = '대한')
group by 극장번호, 상영관번호
order by 극장번호, 상영관번호;

select 극장번호, 상영관번호, count(*), (select 가격 from 상영관 where 예약.극장번호 = 상영관.극장번호 and 예약.상영관번호 = 상영관.상영관번호)
from 예약
where to_char(날짜,'yyyy/mm/dd')=to_char(sysdate,'yyyy/mm/dd') and
극장번호 = (select 극장번호 from 극장 where 극장이름 = '대한')
group by 극장번호, 상영관번호
order by 극장번호, 상영관번호;



select  sum(count(*)*
(select 가격 from 상영관 where 예약.극장번호 = 상영관.극장번호 and 예약.상영관번호 = 상영관.상영관번호)) TOTAL
from 예약
where to_char(날짜,'yyyy/mm/dd')=to_char(sysdate,'yyyy/mm/dd') and
극장번호 = (select 극장번호 from 극장 where 극장이름 = '대한')
group by 극장번호, 상영관번호
order by 극장번호, 상영관번호;

select 극장이름, 상영관.상영관번호, 영화제목, 날짜, 좌석번호, 가격
from 극장,상영관,예약,고객
where 극장.극장번호=상영관.극장번호 and
상영관.극장번호=예약.극장번호 and
상영관.상영관번호=예약.상영관번호 and
예약.고객번호 = 고객.고객번호 and
이름 = '홍길동';
