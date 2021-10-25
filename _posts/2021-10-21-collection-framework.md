---
title: "Java Basic: collection-framework"
categories:
  - Java Basic
tags:
  - List
  - Set
  - Map
---

#### 배열의 단점
1) 자료형이 동일한 데이터만 담을 수 있다.
2) 크기를 변경할 수 없다. -> 메모리낭비

이러한 배열의 단점을 해결하기 위해
자바에서는 "컬렉션프레임워크"를 제공한다.

## 컬렉션 프레임워크
"컬렉션프레임워크"란 동적배열의 개념으로써 
많은 양의 자료를 처리하기 위한 자료구조이며
자료형이 다른것을 담을 수도 있고
동적으로 데이터를 추가하거나, 삭제하는 작업이 편리하다.

---

컬렉션프레임워크의 종류는
Set,List,Map이 있다.

Set,List,Map 모두 많은 자료를 처리하기 위한 자료구조이며
동적으로 데이터를 추가하거나 삭제하거나 서로 다른 자료형을 담을 수 있다.

---

### Set
데이터의 중복 허용 x

- HashSet
->데이터의 중복을 허용하지 않고, 데이터의 순서를 유지 하지 않는다. 
- LinkedHashSet
데이터의 중복을 허용하지 않고, 데이터의 순서를 유지한다.
- TreeSet
데이터의 중복을 허용하지 않고, 데이터를 정렬해준다.
---
#### Random 클래스
임의의 값(정수,boolean,double...)을 생성하기 위한 클래스

- nextInt()			int가 표현할 수 있는 최소값~최대값 범위안에 있는 난수 발생
- nextInt(int bound)   0~bound-1사이의 난수를 발생
---
### List

- ArrayList
- LinkedList
- Vector


ArrayList와 LinkedList는 사용하기 위한 메소드는 동일하지만
내부적으로 동작하는 방식이 다르다.

- ArrayList
	중간에 데이터를 추가하거나 삭제하거나 할 때에 마치 배열처럼 동작.
	중간에 데이터를 추가하는 경우라면 내부적으로 다시 메모리를 할당하고
	자료을 일일이 다 옮겨주는 작업을 수행합니다.
	
- LinkedList
	추가하는 자료의 앞뒤의 참조하는 주소값만 변경이 됩니다.
	

그러므로 데이터의 중간에 추가, 삭제가 빈번한 경우라면
ArrayList보다는 LinkedList를 사용하는 것이 효율적.

```java
ArrayList list = new ArrayList();
		list.add(true);
		list.add(new Person("홍길동", 20));
		list.add(new Person("이순신", 40));
		list.add(26.7);
		list.add(new Person("유관순", 30));
		list.add("안녕 자바");
		list.add(2021);
		
		// list에 데이터가 있는 만큼 반복실행하면서
		// 데이터를 하나씩 꺼집어내어 sayHello메소드를 호출한다.
		for(int i=0; i< list.size()  ;i++ ) {
			Object obj = list.get(i);
			System.out.println(obj);
			if(obj instanceof Person) {
				((Person)obj).sayHello();
			}
			//Person p = (Person)list.get(i);
			//p.sayHello();
		}	

```
## 제네릭

**자바 컬렉션 프레임워크에는 자료형이 다른것들을 담을 수 있다.
자료를 추가할때마다 크기가 동적으로 늘어난다.

자바초기에는 자료형이 다른것을 담을 수 있는 것이
좋은 줄 알았지만

사용하다보니 이것저것 다 담고보니 꺼내와서 사용하기가 불편했다. 

그래서 자바 5.0이후부터
가급적이면 컬렉션 프레임워크에 담을 데이터를 한정하여사용하기를 권장한다.
-> 제네릭

ArrayList list = new ArrayList();
라고 하면 list에는 온갖 자료형을 담을 수 있다.

현재에는 이것보다는 다음과 같이 제네릭을 사용한다.

ArrayList<String> list = new ArrayList<String>();
-> list에는 String만 담을 수 있다. 

---
### Wrapper 클래스
기본자료형을 객체로 만들어주는 클래스들 
boolean Boolean
char	Character
byte	Byte
short	Short
int		Integer
long	Long
float	Float
double	Double

---

ArrayList<String> list = new ArrayList<String>();
list안에는 String을 담을 수 있다.

ArrayList<ArrayList> list = new ArrayList<ArrayList>();
->list안에 담는 자료형이 ArrayList

---

### 컬렉션프레임워크의 종류

Set		자료의 중복을 허용하지 않는다.

List	자료의 중복을 허용한다.

Map		key와 value가 한쌍으로 이루어진 자료구조

```java
ArrayList data = new ArrayList();
data.add("홍길동");
data.add("서울");
data.add("010");
```
list의 데이터에 접근하기 위해서는 인덱스로 접근
이름을 갖고오려면 인덱스가 0이다.
data.get(0);

```java
HashMap map = new HashMap();
map.put("이름","홍길동");
map.put("주소","서울");
map.put("전화","010-1234-1111");

map.get("이름");
```
map은 인덱스가 아니라 key에 의해서 데이터에 접근하는 방식
key 자체가 무슨 데이터인지 설명하는 역할을 한다.

map에서는
key는 중복될 수 없다.
그러나 value는 중복 가능 

