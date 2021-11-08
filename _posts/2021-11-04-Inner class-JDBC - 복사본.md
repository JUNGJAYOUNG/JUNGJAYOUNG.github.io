---
title: "Java Basic: Inner Class - JDBC"
categories:
  - Java Basic
tags:
  - Inner Class
  - JDBC
---

sql>
SQL> ed ff

SQL> @ff
SQL> select * from goods;

   NO ITEM         QTY    PRICE
----- ---------- ----- --------
    1 색종이        10    1,500


---
### 자료의 수정
update 테이블이름 set 컬럼이름 =값, 컬럼이름=값, .. where 컬럼이름=값

update goods set qty= 20, price=2000, item='공책' where no=7;

### 자료의 삭제
delete 테이블명 where 컬럼이름=값;
delete goods where no=7;

1. 상품번호를 매개변수로 전달받아 데이터베이스에서 삭제를 하는 메소드를 ㅏㄴ든다.
2. 삭제 버튼을 누르면 텍스트필드의 상품번호를 갖고와서 삭제하는 메소드를 호출

--

CRUD
