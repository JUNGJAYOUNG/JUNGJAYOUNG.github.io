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

* break : switch문이나 반복문에서 사용하여 break문이 있는 중괄호를 탈출하는 용도로 사용한다.  **완전히 반복문을 벗어나게 된다.**

* continue : 반복문에서만 사용되며 반복문을 벗어나는 것이 아니라  **반복문의 다음 조건식 혹은  다음 증감식을 수행**하라는 의미이다.

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
> 실행결과
1  
hello  
2  
hello  
3  		                     //i가 3이 되었을때 조건식을 만족하여 반복문을 탈출한다.
c  
d  


```java
a;
b;
for(int i=1;i<=5;i++){
	System.out.println(i);
	if(i%3==0){
		continue;
	}
	System.out.println("hello");
}
c;
d;
```
> 실행결과
a  
b  
1  
hello  
2  
hello  
3  			                       // i가 3의 배수일때는 반복문 속의 그 다음을 실행하지 않고 다음 증감식을 수행
4  
hello  
5  
hello  



