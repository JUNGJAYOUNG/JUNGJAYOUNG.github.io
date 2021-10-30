---
title: "Java Basic: NotePad예제-JTextArea"
categories:
  - Java Basic
tags:
  - JTextArea
  - java notepad
toc: true
toc_sticky: true
---
## 메모장 만들기
com.sist.draw
-> 주메뉴(그리기색상)에 대한 처리를 위하여
LinePanel 과 GraphicInfo 클래스에
Color drawColor (새로운)멤버변수를 추가한다.

### 메모장 만들기에 필요한 인터페이스, 클래스들
- JFrame, ActionListener
창을 띄우기 위함, 메뉴에 액션을 넣기 위함 

- Reader, Writer
메모장은 문자단위의 입출력 이용

- FileWriter(Writer의 후손)
JTextArea의 내용을 파일로 출력

- JFileChooser
저장할 파일위치와 파일명을 선택할 수 있는 다이얼로그 생성

- JOptionPane
사용자에게 알릴 내용을 메세지창으로 띄움
ex) .showMessageDialog()

---
메모장의 제목표시줄에 
파일이름을 출력하도록 기능을 추가해본다.

파일을 저장하지 않거나, 열어오지 않은 상태에는
"제목 없음"으로 표시하고

파일을 저장하거나 열어왔을때에는
파일이름을 제목표시줄에 출력해본다.

---
- FIle 클래스의 delete 메소드
파일을 삭제할 수 있다.

---
com.sist file02
파일목록을 
JList에 출력하고
JList에서 선택한 항목의 파일 내용을
JTextArea에 출력하는 프로그램

JList에서 선택한 파일이름이 무엇인지 알기 위하여
이벤트를 등록해야 한다.

---

## 입출력

자바에서는 입출력과 관련한 클래스들을 **java.io 패키지**에 모아두었다.
또, 입출력 위해는 자료가 순서있는 흐름이 되어야 하는데 이것을 **스트림** 이라 합니다.
자바에서는 출력할 장치 상관없이 동일한 방식으로 입출력 할 수 있도록 스트림이 만들어져 있다!
	
	자바에서는 크기 두가지 종류의 입출력(스트림)이 있다.
		- 문자단위의 스트림(Reader, Writer)
		- 바이트단위의 스트림(InputStream, OutputStream)

#### 객체단위의 입출력

InputStream의 후손인 ObjectInputStream 와 
OutputStream의 후손이 ObjectOutputStream가 있습니다.

객체단위로 출력하기 위해서는 writeObejct 메소드를 이용하고
객체단위로 읽어들이기 위해서는 readObject메소드를 이용한다.

단, 이때에 객체단위로 출력을 위한 클래스는 
반드시 "직렬화"되어야 하며
이를 위하여 클래스를 만들때에 
Serializable을 implements 해줘야 한다.



