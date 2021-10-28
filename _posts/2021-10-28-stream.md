---
title: "Java Basic: JFrame-Jpanel"
categories:
  - Java Basic
tags:
  - ObjectInputStream
  - ObjectOutputStream
  - Serializable
  - JFrame
  - JPanel
---
## 객체단위 입출력 클래스

- ObjectInputStream
	Object readObject()를 이용하여 객체단위로 파일 내용을 읽어들인다.  
- ObjectOutputStream
	writeObject(Object obj)를 이용하여 객체단위로 출력한다.    
	
	> 객체단위로 출력하고자 하는 그 객체는 반드시 직렬화 되어야 한다.    
	
* 직렬화 : 데이터가 순서있게 파일로 나가고 파일로부터 들어오도록 하는 것

직렬화를 구현하고자하는  클래스에 Serializable 인터페이스를 implements해야한다.
```java
class Student implements Serializable{	//직렬화

}
```
---

## 그림판 만들기 

- JFrame
창을 만들기 위해 상속받는 클래스

- Jpanel 
	그래픽을 표현하기 위해 상속받는 클래스

	- void paintComponent(Graphics g)을 오버라이딩하여
	그 안에 표현하고자 하는 그래픽 명령어(들)을 써준다.  	 
	 repaint()를 호출하여 요청할 수 있다.(직접 호출x)

- MouseListener
마우스이벤트와 관련한 인터페이스 (java.awt.event 패키지)

---
### 선그리기(ArrayList 활용)

창 크기를 조절할때마다
화면에 보이는 내용이 달라져야 하기 대문에
다시 그려주기 위한 paintComponent메소드가 자동으로 동작한다

그래서 내가 이전에 그린 "선"들이 모두 사라지고
맨마지막에 그린 "선"만 나타난다.

이전에 그린 "선"들을 모두 출력하기 위해서는
ArrayList를 이용하여 그 정보들을 담아 두도록 한다.

선 하나의 정보는
x1,y1,x2,y2
이것을 하나의 자료형(클래스) 만들어 관리한다.
=>GraphicObject

---
### 메뉴 만들기
프레임에 메뉴를 만들고
메뉴를 누르면 파일로 저장하도록 한다.

메뉴를 위한 클래스들
- JMenuBar	          ==>"주메뉴"를 담을 수 있는 컨테이너  
- JMenu		   	    ==>"주메뉴"를 위한 클래스이며 "부메뉴"를 담을 수 있는 컨테이너  
- JMenuItem             ==>"부메뉴"를 위한 클래스   
  

"부메뉴"인 JMenuItem들을 생성하여 "주메뉴"인 JMenu에 담고
"주메뉴"인 JMenu들은 JMenuBar에 담는다.

이 JMenuBar를 "프레임"에 설정한다.

- ActionListener 인터페이스
메뉴에 "이벤트 처리"를 위한 인터페이스

---
### 파일 선택하기(JFileChooser 이용)

어떤 파일이름을 저장할지
어떤 파일을 열어올지 선택하기 위한
JFileChooser를 이용해보자
```
jfc = new JFileChooser("c:/myData");	//JFileChooser 객체를 생성
```
.showOpenDialog()
.showSaveDialog() 등의 메소드를 이용해서 
파일을 불러오거나 저장할 때 필요한 다이어로그 창을 띄울 수 있다. 

