---
title: "Java Basic: Inner Class"
categories:
  - Java Basic
tags:
  - Inner Class
  - JDBC
---

## inner클래스
- 클래스안에 포함되는 또다른 클래스를 말한다.
- 클래스가 다른곳에서는 필요하지 않고 특정 클래스안에서만 필요한 경우 
편리하게 만들어 사용할 수 있다.

- inner클래스를 포함하고 있는 클래스를 outter 클래스라고 한다.
- inner클래스는 마치 자신이 outter클래스의 멤버 인 것처럼 동작한다.
- 즉,** outter클래스의 멤버에 자유롭게 접근할 수 있다.**

- 그러나 outter 클래스는 inner에 직접 접근할 수 없고
- 접근하려면 객체를 생성하고 객체를 통해서 접근해야 한다.

### inner 클래스는 언제 사용될까?

쓰레드프로그래밍을 할때
그 기능이 다른 곳에서는 필요치 않고
특정 클래스안에서만 동작해야 될 쓰레드인 경우 
inner클래스로 만든다.

예를들어, 채팅프로그램의 클라이언트를 위한 ChatClient 클래스에서
사용자가 입력한 대화내용을 서버로 보내는 것은 버튼을 눌렀을때에
보내도록 한다. 이 일처리와 상관없이 서버가 보내오는 메세지를 계속 
수신하는 쓰레드가 필요하다. 이 쓰레드는 ChatClient 클래스에서만 필요
하기 떄문에 이 부분을 inner클래스로 만들어 표현한다.
