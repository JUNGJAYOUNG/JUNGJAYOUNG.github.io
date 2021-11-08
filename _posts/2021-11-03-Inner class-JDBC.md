---
title: "Java Basic: Inner Class - JDBC"
categories:
  - Java Basic
tags:
  - Inner Class
  - JDBC
---

## inner클래스
- 클래스안에 포함되는 또다른 클래스를 말한다.
- 클래스가 다른곳에서는 필요하지 않고 특정 클래스안에서만 필요한 경우 
편리하게 만들어 사용할 수 있다.

- inner클래스를 포함하고 있는 클래스를 outter 클래스라고 한다.
- inner클래스는 마치 자신이 outter클래스의 멤버 인 것처럼 동작한다.
- 즉,** outter클래스의 멤버에 자유롭게 접근할 수 있다.**

- 그러나 outter 클래스는 inner에 직접 접근할 수 없고
- 접근하려면 객체를 생성하고 객체를 통해서 접근해야 한다.

### inner 클래스는 언제 사용될까?

쓰레드프로그래밍을 할때
그 기능이 다른 곳에서는 필요치 않고
특정 클래스안에서만 동작해야 될 쓰레드인 경우 
inner클래스로 만든다.

예를들어, 채팅프로그램의 클라이언트를 위한 ChatClient 클래스에서
사용자가 입력한 대화내용을 서버로 보내는 것은 버튼을 눌렀을때에
보내도록 한다. 이 일처리와 상관없이 서버가 보내오는 메세지를 계속 
수신하는 쓰레드가 필요하다. 이 쓰레드는 ChatClient 클래스에서만 필요
하기 떄문에 이 부분을 inner클래스로 만들어 표현한다.

---
## 데이터베이스 연결 프로그래밍

### "데이터베이스"는 왜 필요한가?
프로그램을 실행한 결과를 화면에 출력하면  
전원을 끄고 나면 그 결과는 날아가 버린다. ==> 휘발성  
그래서 그 결과를 영구적으로 보관하려면 파일을 이용한다.  

그러나, 파일은 이해관계에 있는 여러 사람들이  
항상 최신의 정보를 공유하기에는 어려움이 있다.

그래서 이해관계에 있는 사람들이 항상 최신의 정보를 공유하도록
자료를 한 곳에 모아둔 것이   
"데이터베이스"  

데이터베이스를 잘 사용하도록 도와주는 시스템
"데이터베이스 관리 시스템"
DataBase Management System
DBMS

DBMS 종류는
oracle, ms-sql, my-sql, mariadb 등이 있다.
우리나라에서는 oracle을 많이 사용한다.

---
속성(열, 필드)
||
|이름|국어|영어|수학|
|----|--|--|--|
|홍길동|100|80|90|	->레코드(행, row)
|이순신|80|90|100|
|유관순|70|100|100|

테이블은 행과 열로 구성된 자료의 집합
데이터베이스는 서로 관련이 있는 테이블들이 모여서 데이터베이스를 구성한다.

---
### 테이블 생성 명령어

`create tabel 테이블이름(속성이름 자료형, 속성이름 자료형,  ....)`

문자열의 자료형 	==> varchar2(100)
숫자 자료형 		   ==> number

`sql>create table student(name varchar2(20),kor number, eng number,math number);`

테이블 구조를 파악하는 명령어
`sql>desc student;`

---
### 테이블에 자료를 추가하는 데이터베이스 명령어

`insert into 테이블이름 values(값1, 값2, ......);`

이때 값의 수와 순서는 테이블의 구조와 같아야한다.
**오라클에서 문자열을 반드시 홋따옴표로 묶어야한다.**

`insert into student values('홍길동',100,80,90);`

이렇게 추가한 내용을 **DBMS에 반영하려면
반드시 commit을 해야한다.**

만약, 이렇게 추가한 내용을 취소 하려면
rollback을 한다.

---

### 테이블의 자료를 조회하기

select * from 테이블이름;
select * from student;

---
==> 자바에서 데이터베이스에 연결
==> Java DataBase Connect
==> JDBC 연결 프로그래밍

---

## JDBC 프로그래밍 순서
---->자바에서 데이터베이스 연결 프로그래밍 순서

1. JDBC드라이버를 메모리로 로드한다.
	Class.forName(oracle.jdbc.driver.OracleDriver);

2. DB서버에 연결한다.
	Connection conn =DriverManager.getConnection("서버의주소","사용자이름","암호");
	
3. 데이터베이스 명령을 실행할 Statement 객체를 생성한다.
	Statement stmt = conn.createStatement();
	
4. 데이터베이스 명령을 실행한다.
	int re = stmt.executeUpdate(명령어)
    ==> 데이터베이스에 변경이 있는 명령을 시킬때 사용
	==> 성공적으로 명령을 수행한 **레코드의 수(int형)를 반환**
	
	ResultSet rs = stmt.executeQuery(명령어)
	==> 데이터베이스의 내용을 읽어오는 명령을 시킬때 사용
	==> 읽어온 결과를 ResultSet으로 반환
	
5. 일처리를 한다.	
	
6. 사용했던 자원을 모두 닫아 준다.
	rs.close();
	stmt.close();
	conn.close();
	
---
실행했더니 다음과 같은 오류가 발생한다.
예외발생: oracle.jdbc.driver.OracleDriver
=> 드라이버가 어디있는지 몰라서 그렇다. 드라이브의 위치를 알려줄 것.
(이클립스에 포함시켜주어야 한다.)

오라클 설치된 다음의 경로에
C:\app\a863a\product\21c\dbhomeXE\jdbc\lib

해결방법

이클립스 프로젝트이름에 오른쪽 단추
->Properties
->JavaBuildPath
->Libraries
->C:\app\a863a\product\21c\dbhomeXE\jdbc\lib\ojdbc8.jar
->apply and close

