## Built-in Object
- Application Area(application): 어플리케이션 시작->종료까지 유지, tomcat
- Session Area(session): 로그인 정보 등 저장, server
- Request Area(request): 응답 완료되면 소멸, forward / redirect
- Page Area(pageContext): 페이지가 바뀌면 새로운 객체 생성
---
### JSP 기본 객체 영역(Scope) method

| 메서드                                     | 반환형         | 설명                                                         |
|-----------------------------------------|-------------|------------------------------------------------------------|
| setAttribute(String name, Object value) | void        | Key-Value 형태로 각 영역에 데이터 저장<br/>name이 value를 얻어오기 위한 key 저장 |
| getAttribute(String name)               | Object      | 현재 객체에서 인자로 받은 이름으로 설정된 값 반환                               |
| getAttributeNames()                     | Enumeration | 현재 객체에서 설정된 값의 모든 속성 이름 반환                                 |
| removeAttributes(String name)           | void        | 현재 객체에서 인자로 받은 이름으로 설정된 값 삭제                               |

```java
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>JSP 기본객체</title>
</head>
<body>
	<p>페이지 속성 : <%= pageContext.getAttribute("name") %></p> <%-- 해당 페이지에서만 쓰는 거였으니까 3에서 4로 넘어왔으니 null --%>
	<p>요청 속성 : <%= request.getAttribute("name") %></p> <%-- 새롭게 요청을 날려서 5로 넘어왔으니 null --%>
	<p>세션 속성 : <%= session.getAttribute("name") %></p> <%-- 브라우저 달라지면 이거도 null 되겠지요 --%>
	<p>애플리케이션속성 속성 : <%= application.getAttribute("name") %></p> <%-- 톰캣을 한 번 껐다가 키면 이거도 null --%>
</body>
</html>
```
---
### JSP 기본 태그 종류
| 문법              | 이름                   | 용도 및 실행 위치                          | 예시                                      |
|-----------------|----------------------|-------------------------------------|-----------------------------------------|
| `<% ... %>`     | **스크립틀릿(scriptlet)** | JSP 내부에서 **자바 코드 실행**               | `<% int x = 10; %>`                     |
| `<%= ... %>`    | **표현식(expression)**  | **출력용**: 값을 화면에 출력                  | `<%= user.getName() %>` → HTML에 그대로 출력됨 |
| `<%! ... %>`    | **선언(declaration)**  | 클래스의 **멤버 변수, 메서드 정의**              | `<%! int count = 0; %>`                 |
| `<%-- ... --%>` | **주석(comment)**      | JSP 주석. **컴파일되지 않음** → 클라이언트에게 안 보임 | `<%-- 이건 주석입니다 --%>`                    |
| `<%@ ... %>`    | **지시자(directive)**   | JSP 페이지의 **메타정보 설정**                | `<%@ page import="java.util.*" %>`      |
---
### JSP 내장 객체 Scope (4가지)
| Scope | 생존 범위 | 주요 메서드 |
| --- | --- | --- |
| **page** | 해당 JSP 페이지 내 | `pageContext.setAttribute()` |
| **request** | 하나의 요청(Request Dispatcher 포함) | `request.setAttribute()` |
| **session** | 같은 사용자 브라우저 유지되는 동안 | `session.setAttribute()` |
| **application** | 서버 전체(모든 사용자 공유) | `application.setAttribute()` |

> ⚠ 각 범위는 넓은 순서대로: page < request < session < application