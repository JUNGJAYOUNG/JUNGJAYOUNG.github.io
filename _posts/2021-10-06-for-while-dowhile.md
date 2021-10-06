---
title: "Java Basic: for each-while-do while"
categories:
  - Java Basic
tags:
  - while
  - do while
  - for
  - for each

---

### for문의 무한루프 구조

```
for(;;){
			//무한루프(항상 참)
}
```
위의 구조를 사용하여 
for문이 오기전에 초기값을 두고,
증감식을 증감식과 조건식을 for문 속에 두어 반복할 횟수를 정할 수 있다.
```java
int i=1;
for(;;){
	System.out.println("hello");
	if(i>=3){	//i가 3이면 for문 탈출
		break;
	}
	i++;
}
```
위와 같이 for문이 오기전에 초기값을 주고
for문 속에서 조건식과 증감식을 주어
반복 시킬 횟수를 정할 수 있다.

## while

### while 문의 형식
```
초기값;
while(조건식){
	반복실행시킬 명령어(들);
	증감식;
}
```
-----

### do while 문의 형식
```
초기값;
do{
	반복 수행할 명령어(들);
	증감식;
}while(조건식);
```
-----

### while과 do~while의 차이

만약에 처음부터 조건을 만족하지 않는 상황이라면 
while문은 반복문을 한번도 실행하지 않는다.
**do~while문은 어찌되었던 do문을 적어도 한번은 실행한다.(조건을 나중에 비교)**

```java
int i=100;
while(i<=3){	//조건 만족 x -> 한번도 동작하지 않음
	System.out.println("hello");
	i++;
}
```


```java
int i=100;
do{
	System.out.println("hello");	//한번 실행
	i++;
}while(i<=3);	//조건 나중에 판별
```
출력결과
hello

------------
**Q. **반복문이 세가지(for,while,do~while)나 있는데
어떨 때 어떤 것을 사용하는 것이 좋은가요?
**A.**반드시 이럴때는 이것을 써요! 라고 정해진 것은 없다.

그러나 일반적으로 반복 실행 해야할 횟수가 딱 정해진 경우는 for를 많이 사용. 
사용자의 입력값(혹은 조건이) 만족할동안 계속해서 동작해야하는
경우에는 while이나 do~while 문을 사용하는 것이 좋다.

그리고
일단 한번 동작해야 하는 경우라면
do~while문을 이용하는 것이 좋다.

### 반복문을 이용하여 제대로 된 값을 입력할때까지 입력 받기
```
System.out.print("월을 입력하세요==>");
month = sc.nextInt(); //-5
```
```java
while(true){
	System.out.print("월을 입력하세요:"")
	month=sc.nextInt();
	if(month >=1 && month<=12){	//제대로 된 값을 입력하면 for문 탈출
		break;
	}
}
```
### 배열의 요소 만큼 반복 실행하기

`int []data = {10,20,30,40,50};`

위와 같은 배열의 요소만큼 반복 실행하기 위해서는 다음과 같이 반복문을 사용한다.

```java
for(int i=0;i<data.length;i++){
	System.out.println(data[i]);
}
```

```java
int i=0;
while(i<data.length){
	System.out.println(data[i]);
	i++;
}
```

```java
int i=0;
do{
	System.out.println(data[i]);
	i++;
}while(i<data.length);
```
위와 같은 반복문(for, while, do~while)을 사용하여 배열의 인덱스만큼 증가시켜
배열의 요소에 접근할 수 있다.

또한, 자바에서는 배열의 요소만큼 반복 실행하기 위한
향상된 반복문(for-each)을 제공한다.

## for each
**배열의 요소만큼 반복 실행**시키기 위하여 사용하며  
사용하는 방법은 다음과 같다.

### for each 반복문의 형식
```
for( 자료형 변수명: 배열이름){
	반복실행시킬 명령어(들)
}
```
for each 는 배열의 요소를 차례로 꺼내와서 변수에 담는다.
하나씩 꺼집어 내어와서 담을 변수의 자료형은 배열의 자료형과 일치해야한다.

```java
for( int v : kor){
	System.out.print();		//kor의 요소들을 하나씩 끄집어 내와서 v에 차례로 담는다
}
```

