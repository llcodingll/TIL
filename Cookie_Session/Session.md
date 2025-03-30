## Session


: 사용자가 웹 서버에 접속해 있는 상태
- 각 세션은 sessionid를 이용해 구분
- WAS의 메모리에 객체 형태로 저장
- 메모리가 허용하는 용량까지 제한 없이 저장 가능
- 서버네 저장하기 때문에 cookie에 비해 보안이 좋음
- 사용자(로그인) 정보, 장바구니 등
---
### 동작 순서
1. Client 페이지 요청
2. Server는 cookie에서 session id 존재 유무 확인
3. session id가 존재하지 않으면 session id 생성해 cookie를 사용한 다음 client로 반환
4. 생성된 session id를 이용해 서버 내 메모리 생성
5. client가 다음 요청 시, 쿠키에 session id(JSESSIONID)를 포함해 전달하면 서버 내 저장된 session id와 비교해 데이터 조회
---
### HttpSession 메서드

| 메서드                                          | 설명                                            |
  |----------------------------------------------|-----------------------------------------------|
| void setAttribute(String name, Object value) | session에 지정한 name에 해당하는 객체 추가                 |
| void setMaxInactiveInterval(int interval)    | 사용자가 다음 요청 보낼 때까지 session을 유지하는 최대 시간(초단위) 설정 |
| void invalidate()                            | 현재 session 삭제, 속성 삭제                          |
| String getId()                               | 현재 session의 고유 id 반환                          |
| long getLastAccessTime()                     | 현재 session에 client가 마지막으로 요청 보낸 시간 반환(long)   |
| `Object` getAttribute(String name)           | name에 해당하는 속성값 반환, 반환형 유의                     |
| long getCreationTime()                       | session이 만들어진 시간 반환                           |
| void removeAttribute(String name)            | session에서 지정한 이름의 객체 제거                       |
| Enumeration getAttributeNames()              | session에서 모든 객체 이름을 Enumeration형으로 반환         |

```java
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>

<%
	String id = request.getParameter("id");
	String password = request.getParameter("password");
	
	//ID, PW를 이용해 DB에서 해당 유저 있는지 검사
	//(현재) Manager로 메모리 통해 관리하고 있지 X
	if(id.equals("user1") && password.equals("1234")){
		//로그인 성공
		HttpSession session1 = request.getSession(); // 자체적으로 반환 타입 있으면 그거 가져와서 쓸 수 있게 해준다
		//session1이 아닌 session이면 컴파일에러남
		//session은 이미 jsp에 기본 객체가 있음 그러니까 쓸 수 없음
		session.setAttribute("loginUser", "유user2"); //id, nickname 저장
		
		//페이지 이동 : main.jsp로
		//1. forwarding 방식
		// request.getRequestDispatcher("08_Main.jsp").forward(request, response);
		//2. redirect(권장) => 어떤 차이가 있는지 알고 쓸 것
		response.sendRedirect("08_Main.jsp"); //새로고침 열심히 해도 문제 발생 X
	} else {
		//로그인 실패
		response.sendRedirect("07_LoginForm.jsp");
	}
	
%>
```