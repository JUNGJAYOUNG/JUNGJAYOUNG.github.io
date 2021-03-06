---
title: "Java Basic: Exception handling"
categories:
  - Java Basic
tags:
  - RuntimeException
  - Exception handling
  - try-catch
  - throws
  - throw
---

## 예외처리
프로그램 실행 중에 예기치 않는 상황이 발생하는 것을 "예외"라고 한다.
이러한 "예외"를 처리하는 것을 "예외처리"라고 한다.

자바에서는 대부분의 예기치 않은 상황에 대해서는 
이미 클래스로 만들어져 있고
**자동으로 예외 객체를 생성한다.**

```java
int a = 4/0;	->자동으로 new ArithmeticException() 생성
```
하나의 try안에 여러개의 catch절이 올 수 있다.
이때 catch절의 순서는 **범위가 작은 예외클래스 순서대로 catch해야한다.**
또, 예외 발생과 상관없이 반드시 처리해야할 명령이 있다면
finally를 사용한다.

```java
try{
	예외가 발생이 될만한 문장(들)
}catch(예외클래스명1 변수명){
	예외가 발생되었을때 처리할 문장(들)
}catch(예외클래스명2 변수명){
	예외가 발생되었을때 처리할 문장(들)
}catch(예외클래스명3 변수명){
	예외가 발생되었을때 처리할 문장(들)
}finally{
	정상적으로 동작하거나 예외가 발생하거나 반드시 처리해야할 명령어(들)
}
```
### 예외와 관련하여 알아야할 내용들
- throws
- RuntimeException
- throw
- 사용자정의 예외

---
## throws
예외를 메소드를 호출하는 쪽으로 **"던진다"**

메소드 안에서는 
메소드 처리를 위한 핵심 내용만 쓰고
예외처리는 메소드를 호출하는 쪽에다가 맡기고 싶은 경우.
```
public void 메소드이름() throws 예외클래스이름{

}
```
**throws 사용 
-> 메소드를 호출하는 쪽에서 try ~catch로 예외처리 해주어야 한다.**

---
### RunTimeException
RuntimeException의 후손클래스들은
사용자가 특별히 예외처리를 하지 않아도 자바가 예외처리를 해준다.
**그러나 RuntimeException의 후손이 아닌 예외들은
반드시 사용자가 예외처리를 해주어야 한다.**

#### RunTimeException의 후손이 아닌 것

* java.io 패키지 : 입출력 관련 클래스 모음
* java.net 패키지 : 네트워크 통신 관련 클래스 모음
* java.sql 패키지 : 데이터베이스 연결 관련 클래스 모음

위 패키지의 생성자와 메소드들은 RuntimeException의 후손이 아닌 예외를
포함하고 있다. RuntimeException의 하위 예외들은 자바가 예외처리를 해주기 때문에
컴파일이 되지만 하위예외가 아니라면 
**-> 사용자가 별도로 예외처리를 해야만 컴파일 가능**

---

## throw
사용자가 강제로 예외를 발생시킬때 사용

`throw new 예외클래스이름();`

---
## 사용자 정의 예외

자바는 대부분의 일반적인 예외상황에 대해서는 이미 
예외클래스들이 만들어져 있고
그런상황이 되면 자동으로 예외객체가 생성된다.

그러나 내가 만들고 있는 프로젝트에서만 처리되는
특수한 경우의 상황을 예외로 만들고자 한다면
(즉, 자바는 모르고 있는 어떠한 상황이 있다면)
사용자가 직접 예외를 만들 수 있다.

### 사용자 정의 예외클래스를 만드는 방법 
1. 예외클래스의 제일 조상인** Exception을 상속받아** 클래스를 만든다.
2. 생성시에 **예외메시지를 전달받아 부모생성자에게 전달**해준다.

```java
class 사용자정의예외클래스이름 extends Exception{	//Exception상속
	public 사용자정의예외클래스이름(String msg){	
		super(msg);	//생성시 msg메시지 부모생성자에게 전달
	}
}
```
```java
if( 문제의 상황인지 조건식){
	throw new 사용자정의예외클래스이름(메세지);
}
```
-> 문제의 상황을 if조건식에 물어보고 적절한 메세지를 출력하는 방식도 있지만
사용자 정의 예외 방식은 미리 이러한 상황은 "문제로 인식하자" 라는데에 의미가 있다.

## finally
예외처리에서 예외가 발생하거나 정상적으로 동작하거나 반드시 처리해야할 명령어들을 쓰기 위하여 사용하는 문장이다.
		 
- finally에는 주로 어떤 명령어들을 쓰나요?
파일처리나, 네트워크 통신이나, 데이터베이스 연결프로그램에서 작업이 끝난 다음에는 
사용한 자원을 반드시 닫아 주어야 한다.
이러한 자원을 닫아 주는 명령어 (close)는 
예외가 발생하거나 정상적으로 동작하거나 반드시 닫아 주어야 하기때문에 
finally로 작성한다.
