---
title: "Java Basic: instanceof-final-Interface"
categories:
  - Java Basic
tags:
  - instanceof
  - final
  - interface
---
## 인터페이스

자바에서는 다중상속의 효과를 기대할 목적으로 인터페이스를 이용한다.
상수, 추상메소드 만으로 구성되는 인터페이스는
final과 abstract를 굳이 붙이지 않아도
기본적으로 final, abstract이 설정되어 있다. 
final(반드시 초기값을 주어야 한다.)

인터페이스에는 body가 구체화된 메소드를 포함xxxx할수없다.
#### 추상클래스 vs 인터페이스 차이점
** 추상클래스는 body가 구체화된 메소드를 가질 수 잇으나
인터페이스는 가질 수 없다.**

### 다형성
동일한 매세지를 받아도 동작하는게 다름
(오버라이딩)

## is - a 관계

호빗 is a 게임캐릭터

-> 상속관계에 있는 것을 is a 관계라고 한다.
상속관계에 있을 때(is a 관계에 있을때)
부모클래스의 참조변수가
자식클래스의 객체를 참조할 수 있다.

## instanceof 연산자

어떤 객체가 특정 클래스의 자료형인지 판별하기 위한 연산자
상속계층을 구성하고 있을때
상위클래스의 배열에 자식클래스의 객체들을  담을 수 있다
이때 배열의 요소를
하나씩 끄집어 내어 일괄처리 할때에
자식클래스에서 추가된 메소드를 호출하기 위해서는
자식클래스로 형변환해야한다.

이때 자식의 종류마다
호출해야하는 메소드가 다르고
자식의 종류도 여러가지일때에
해당 자식클래스인지 물어보고 형변환해야한다.

이때 instanceof 연산자를 이용한다.

## has a, is a

클래스 A,B 가 있을때
A has a B는 
A클래스의 멤버변수로 B클래스의 객체를 가진다는 의미

class B{
	~
}

class A{
	private B;
}

--------
A is a B는 상속관계를 말한다.

class B{
 	~
}
class A extends B{

}
---
CUI : Character User Interface
컴퓨터하고 사람하고 글자로 의사소통
GUI: Graphic User Interface
컴퓨터하고 사람하고 그래픽화면으로 의사소통

자바가 GUI관련 클래스와 인터페이스를 모아놓은 패키지
- java.awt	: 자바초기부터 있던 것, gui 모양이 윈도우나 리눅스 
  맥이나 시스템마다 좀 다른 모양
- javax.swing	: 나중에 만들어진것, gui 모양이 모든 플랫폼에
  동일한 

---
자바가 제공하는 여러가지 클래스들

String
문자열처리를 위한 여러가지 기능을 제공
엄밀히 말하면 참조자료형
기본자료형처럼 사용할 수도 있다.
```
Person p = new Person();
String data = new String("안녕");
String data = "안녕"; 
```
자바가 제공하는 문자열 처리를 위한 클래스
- String
- StringBuffer
- StringBuilder

String 은 변하지 않는 문자열 처리에 적합하고
StringBuffer와 StringBuilder는 변하는 문자열 처리에 적합하다.

String 변수를 문자열을 만들고
문자열의 내용을 변경시키면
새로운 메모리로 이동하고
원래의 객체는 garbage가 된다. 

그러나
StringBuffer나 StringBuilder 변수로 문자열을 만들고
문자열 내용을 변경시키면
객체자신이 변경되고
새로운 메모리로 이동되지 않는다.

그렇기 때문에 변하는 문자열 처리에는
String이 적합하지 않다.

---------

equals(Object obj)
=> 참조자료형에서 
비교연산자 ==은 두개의 객체가 서로 동일한 메모리를
참조하고 있는지 판별한다.
만약, 참조자료형의 두개의 객체가 서로 동일한 값을
갖고 있는지 판별하기 위해서는
equals메소드를 이용한다.

String도 참조자료형이기 때문에
두개의 문자열이 서로 동일한 문자열인지 판별하기 위해서는
equals를 자신에게 맞도록 "재정의"할 수 있다.

---

indexOf(String data)
indexOf(char ch)
-> 문자열 안에서 특정 문자열이나 문자가 위치한 인덱스를 반환하는 메소드이다.
만약 찾고자 하는 문자나 문자열이 없으면 -1을 반환한다.

---
lastIndexOf

---
substring(beginIndex, endIndex)
문자열데이터로부터 beginIndex에서부터 endIndex-1까지의 문자열을 반환하는 메소드

substring(beginIndex)
문자열데이터로부터 beginIndex부터 끝까지 문자열을 반환하는 메소드

---
length()
==> 문자열의 길이를 정수로 반환하는 메소드

조심하기!
배열의 길이는 속성 length
문자열의 길이는 메소드 length()
