---
title: "Oracle SQL: PreparedStatement"
categories:
  - Oracle SQL
tags:
  - PreparedStatement
---

## PreparedStatement
데이터베이스 명령어가
때로는 사용자가 입력한 값으로
명령어를 만들어야 하는 경우가 있다.

String sql = "update goods set item=?,qty=?,price=? where no=?";

변수가 들어갈 자리에 ?로 대신하여 데이터베이스 명령어를 만들 수 있다.
```java
//PreparedStatement 생성시에 ?가 있는 sql을 매개변수로 보내줄것
		pstmt = conn.prepareStatement(sql);
			
		//PreparedStatement 객체에 결정되지 않은 ?에 차례대로 값을 설정
		pstmt.setString(1, item);
		pstmt.setInt(2, qty);
		pstmt.setInt(3, price);
		pstmt.setInt(4, no);
			
		//PreparedStatement 객체 생성시에 이미 sql이 전달되었고
		//그리고 위에서 각각의 ?에 값이 연결된 상태이기 때문에
		//executeUpdate할때는 sql을 전달하지 말것
		//만약 전달하게 되면 ?의 값이 정해지지 않은 상태로 실행하게 된다->에러남
			int re = pstmt.executeUpdate();
```

C:\app\a863a\product\21c\homes\OraDB21Home1\network\admin







