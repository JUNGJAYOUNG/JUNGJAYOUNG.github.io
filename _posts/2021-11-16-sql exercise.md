---
title: "SQL: sql exercise"
categories:
  - Java Basic
tags:
  - Inner Class
  - JDBC
---

- 극장별 상영관 수를 출력
select 극장번호, count(상영관번호) 상영관수
from 상영관
group by 극장번호;

- '잠실'에 있는 극장의 상영관를 출력
1) 잠실에 있는 극장의 극장번호
select 극장번호
from 극장
where 위치 like '%잠실%';
2) 잠실에 있는 극장의 상영관 정보 출력
select *
from 상영관
where 극장번호 in (select 극장번호
from 극장
where 위치 like '%잠실%');

**- 2014년 9월 1일의 극장별 평균 관람 고객 수를 출력**
평균관람고객수????
1) 극장별 관람 고객 수
select count(*)
from 극장, 예약
where 극장.극장번호 =예약.극장번호 
group by 극장.극장번호;

**- 2014년 9월 1일에 가장 많은 고객이 관람한 영화를 출력**
1) 영화별 관람 고객수
select 극장번호, 상영관번호, count(*)
from 예약
where 날짜='2014/09/01'
group by 극장번호, 상영관번호;


2)
- 각테이블에 데이터를 삽입하는 insert문을 하나씩 실행

- 영화의 가격을 10%씩 인상
update 상영관 set 가격=가격*1.1;

