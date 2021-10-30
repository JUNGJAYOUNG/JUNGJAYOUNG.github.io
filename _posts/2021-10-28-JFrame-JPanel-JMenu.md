---
title: "Java Basic: JFrame-JPanel-JMenu"
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
	
	> 객체단위로 출력하고자 하는 그 객체는 반드시 "직렬화" 되어야 한다.    
	
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
다시 그려주기 위한 paintComponent메소드가 자동으로 동작한다.

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

```java
public class MyFrame extends JFrame implements ActionListener {
	private LinePanel lp;

	public MyFrame() {
		lp = new LinePanel();
		add(lp);
		
		//메뉴바 생성
		JMenuBar jmb = new JMenuBar();
		//주메뉴 "파일" 생성
		JMenu mn_file = new JMenu("파일");
		//주메뉴 "그리기도구" 생성
		JMenu mn_draw = new JMenu("그리기도구");
		//부메뉴 "새파일" 생성
		JMenuItem file_new = new JMenuItem("새파일");
		//부메뉴 "열기" 생성
		JMenuItem file_open = new JMenuItem("열기");
		//부메뉴 "저장" 생성
		JMenuItem file_save = new JMenuItem("저장");
		
		//주메뉴 "그리기도구"에 담길 부메뉴들을 만든다.
		JMenuItem draw_line = new JMenuItem("선"); 
		JMenuItem draw_rect = new JMenuItem("사각형"); 
		JMenuItem draw_oval = new JMenuItem("원"); 
		
		//"부메뉴"들을 "주메뉴"에 담는다.
		mn_file.add(file_new);
		mn_file.add(file_open);
		mn_file.add(file_save);
		
		//"부메뉴"들을 "주메뉴"에 담는다.
		mn_draw.add(draw_line);
		mn_draw.add(draw_rect);
		mn_draw.add(draw_oval);
		
		//"주메뉴"를 "메뉴바"에 담는다.
		jmb.add(mn_file);
		jmb.add(mn_draw);
		
		//"메뉴바"를 프레임에 등록
		setJMenuBar(jmb);
		
		//각각의 JMenuItem에 대하여 이벤트를 등록한다.
		file_new.addActionListener(this);
		file_open.addActionListener(this);
		file_save.addActionListener(this);
		
		//그리기 도구의 부메뉴들에 이벤트를 등록한다.
		draw_line.addActionListener(this);
		draw_rect.addActionListener(this);
		draw_oval.addActionListener(this);
		
		setSize(600,400);
		setVisible(true);
		setTitle("선그리기");
	}
	//각각의 JMenuItem을 누르면 actionPerformed 메소드가 동작한다.
	@Override
	public void actionPerformed(ActionEvent e) {
		//JMenuItem중에 어떤 메뉴가 눌러졌는지 파악하기 위하여 매개변수
		//ActionEvent의 getActionCommand()를 이용한다.
		
		String cmd = e.getActionCommand();
		//System.out.println(cmd +"가 눌러짐");
		
		if(cmd.equals("저장")) {
			try {
				ObjectOutputStream oos = new ObjectOutputStream(new FileOutputStream("c:/myData/data.pan"));
				//LinePanel 객체의 멤버변수인 list를 파일로 출력한다.
				oos.writeObject(lp.list);
				oos.close();
				
			}catch(Exception ex) {
				System.out.println("예외발생:"+ex.getMessage());
			}
		}else if(cmd.equals("열기")) {
			
			//"c:/myData/data.pan"파일의 내용을 읽어들여
			//LinePanel 객체인 lp의 list에 저장하도록 한다
			//화면을 다시 그리기 위하여 LinePanel의 객체인 lp의 repaint를 호출한다.
			
			try {
				ObjectInputStream ois = new ObjectInputStream(new FileInputStream("c:/myData/data.pan"));
				//파일로 데이터를 읽어들여 Linepanel 객체인 lp의 list에 담는다
				lp.list = (ArrayList<GraphicInfo>)ois.readObject();
				
				//파일의 내용을 읽어와서 list에 담긴 그래픽의 정보만큼 다시 그려주기 위해 호출
				lp.repaint();
				//파일을 닫아준다.
				ois.close();
			}catch(Exception ex) {
				System.out.println("예외발생:"+ex.getMessage());
			}
				
		}else if(cmd.equals("새파일")) {
			System.out.println("새파일의 처리입니다.");
		}else if(cmd.equals("선")) {
			lp.drawType=0;
		}else if(cmd.equals("사각형")) {
			lp.drawType=1;
		}else if(cmd.equals("원")) {
			lp.drawType=2;
		}
	}
}
```
---
### 파일 선택하기(JFileChooser 이용)

어떤 파일이름을 저장할지
어떤 파일을 열어올지 선택하기 위한
JFileChooser를 이용해보자
```java
jfc = new JFileChooser("c:/myData");	//JFileChooser 객체를 생성
```
.showOpenDialog()
.showSaveDialog() 등의 메소드를 이용해서 
파일을 불러오거나 저장할 때 필요한 다이어로그 창을 띄울 수 있다. 

