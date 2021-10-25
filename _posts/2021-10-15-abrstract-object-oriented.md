---
title: "Java Basic: Abrstract-ObjectOriented"
categories:
  - Java Basic
tags:
  - abstract class
  - abstract method
  - object-oriented
  - eclipse
---
상속관계에 있을때
부모클래스의 참조변수가
자식클래스형의 객체를 참조 할 수 있다. 
이때 부모클래스의 메소드를 자식클래스에서 오버라이딩했다면
오버라이딩한 자식클래스의 메소드가 동작한다.

그러나 부모클래스에는 없고 자식클래스에서 새로 추가한 메소드는
바로 호출할 수 없고, **자식클래스로 형변환 후 호출할 수 있다. **
`((SalariedEmployee)e1).setGrade(grade);`

--------------------------------------
## 추상클래스와 추상메소드
* 추상메소드: 메소드의 body가 없는 메소드

클래스에서 어떤 메소드를 구체화 할 수 없고
자식클래스들이 자신에게 알맞도록 재정의해야만 할 메소드인 경우
body가 없는 추상메소드로 정의한다.

* 추상클래스: 추상메소드를 하나라도 포함하고 있는 클래스
클래스이름 왼쪽에 abstract 키워드를 붙인다.

```
public abstract void computeSalary();
//body를 구체화 할 수 없는 메소드는 추상메소드로 만든다.
//미래에 만들어지는 자식클래스들이 자신에게 알맞도록 반드시 오버라이딩 해야한다!
```

**추상클래스를 상속받았다면 반드시 모든 추상메소드를 오버라이딩 해야한다.**

### 다형성
객체에게 동일한 메세지를 주었는데
객체마다 하는일이 다르다?

------------------------------------
상속관계에 있을때
부모의 메소드가 자식에게 알맞지 않은 경우
자식클래스에 맞도록 오버라이딩 할 수 있다.

이때 부모클래스의 객체와 자식클래스의 객체가
동일한 메세지를 받았을때에 
객체마다 하는일이 다르다.

이것을 다형성 이라고 한다.

-------------------------------------
## 객체지향 프로그래밍

* 객체지향 프로그래밍의 특징
1. 은닉성: 외부로부터 클래스의 속성(멤버변수)들을 노출하지 않고 보호하는것
2. 상속성: 이미 있는 클래스를 확장(재사용)하여 새로운 클래스를 만드는 것
3. 다형성: 메소드오버라이딩을 이용하여 객체에게 준 메세지는 동일한데
   객체마다 다른 일을 하도록 하는 것
   
## Eclipse

- 이클립스에서는 클래스를 작성하고 저장하면 자동으로 컴파일 해준다.(코드에 문제가 있으면 컴파일 실패)(.class를 자동으로 만들어준다)

- 파일하나에 하나의 클래스를 만드는 것이 일반적
	
- 클래스를 만들기 전에 서로 관련있는 클래스끼리 모아두기 위한
	패키지를 먼저 만들고 그 패키지에 클래스들을 만든다.
	
- 패키지 이름 생성 3step
  com.sist.board
  a.b.c
  a : 기관의 종류
  b : 기관명
  c : 서비스명

- 자동 완성 기능(ctrl +space)
	sout 적고 ctrl+스페이스 -> System.out.println() 
	이외에도 클래스이름, 생성자, 변수명 등 자동완성 가능.

- 코드 복사(ctrl + alt + 방향키 아래) 

-----------------------------------------------------------------
### Object 클래스

자바의 클래스계층의 최상위 클래스
	
자바가 제공하는 모든클래스의 
제일조상클래스는 Object입니다.

우리가 만드는 클래스도 
묵시적으로 Object의 후손이 됩니다.
	
따라서, 
모든 클래스에서는 
Object의 메소드를 자유롭게 사용할 수 있고
필요하다면 오버라이딩 할 수 있다. 
ex)  toString() 메소드

