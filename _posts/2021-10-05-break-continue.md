---
title: "Java Basic: break, continue"
categories:
  - Java Basic
tags:
  - error
  - if
  - switch case
  - comment
  - comment out
---

### break와 continue

continue : 반복문에서 사용되며

가령 다음 코드에서
```java
a;
b;
for(int i=1;i<=10;i++){
	System.out.println(i);
	if(i%3==0){
		break;
	}
	System.out.println("hello");
}
c;
d;
```
실행결과
1
hello
2
hello
3
c
d

i가 3이 되었을때 조건식을 만족하여 반복문을 탈출한다.

```java
a;
b;
for(int i=1;i<=10;i++){
	System.out.println(i);
	if(i%3==0){
		continue;
	}
	System.out.println("hello");
}
c;
d;
```
실행결과
a
b
1
hello
2
hello
3
4
hello
5
hello
6
7
hello
9
10
hello

즉, i가 3의 배수일때는 반복문 속의 그 다음을 실행하지 않고
다음 증감식을 수행하러 간다.

