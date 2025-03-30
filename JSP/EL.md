## EL(Expression Language)


: JSP 내에서 데이터를 다룰 때, 사용되는 scripting language
- `<% %>` 보다 속성값을 쉽게 출력 하기 위함 ⇒ `${}`
- `${}`: 변수, 속성, 메서드 호출 등 포함 O
---
## JavaBeans


: Java로 작성된 재사용 가능한 SW Component
### 특징
- 클래스 직렬화
- 기본 생성자 필수
- 속성: getter, setter를 사용해 접근 가능해야 함
- 필요한 이벤트 처리 메서드들을 포함해야 함
- EL 표현식을 통해 접근 가능
  - .(dot) / ["속성명"] 사용
  - instance만을 작성하면 .toString() 메서드 동작
```java
//javaBeans
public class Person implements Serializable {
    //객체 직렬화
    private static final long serialVersionUID = 1L; //임시로 1L로 설정
    //작성하는 이유: UID -> 변하지 않는 id를 부여해 person이라는 걸 내가 가지고 있는지 확인
    //따라서 기존 거에서 조금 달라지면 다른 버전이 되니 거기에 맞는 번호를 부여함
    //캡슐화를 위한 private 설정
}

---

<%@ page language="java" contentType="text/html; charset=UTF-8"
pageEncoding="UTF-8"%>
<%@ page import="dto.Person" %>
	<%
Person p = new Person();
		p.setName("user1");
		p.setAge(20);
		p.setHobbies(new String[]{"영화보기", "전시관람"});
        out.print(p);
		
		pageContext.setAttribute("p", p);
	%>

---

<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>JavaBean</title>
</head>
<body>
	<h2>JavaBeans</h2>
<div>전체 정보 : ${p}</div>
	<div>이름 : ${p.name}</div>
	<div>나이 : ${p["age"]}</div>
	<div>취미 : ${p["hobbies"][0]}</div>
</body>
</html>
```
---

```java
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>EL</title>
</head>
<body>
	<!-- 스크립트릿 -->
	<% out.print("Hello"); %>
	<!-- 표현식 -->
	<%= "Hello" %>
	<!-- EL ${변수/함수 호출/계산식} -->
	${"Hello" }
</body>
</html>
```
```java
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>EL</title>
</head>
<body>
	문자열 : ${"Hello"}<br>
	정수형 : ${10}<br>
	실수형 : ${10.1} <br>
	논리형 : ${true} <br>
	null : ${null} <br> <!-- null은 공백 반환 -->
</body>
</html>
```
### Operator
- (괄호) 안은 동일 의미의 연산자를 의미

| 종류   | 사용 가능 연산자                                    | 
|------|----------------------------------------------|
| 산술   | +, -, *, /(div), %(mod)                      |
| 관계   | ==(eq), !=(nq), <(lt), >(gt), <=(le), >=(ge) |
| 조건   | expr?val1:val2                               |
| 논리   | &&(and),                                     ||(or), !(not)|
| null | empty                                        |

```java
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>EL</title>
</head>
<body>
	\${5+2}: ${5+2}<br>
	\${5 div 2}: ${5 div 2}<br>
	\${5>2}: ${5>2}<br>
	\${5 gt 2}: ${5 gt 2}<br>
	\${5 lt 2}: ${5 lt 2}<br>
</body>
</html>
```
```java
<%@ page language="java" contentType="text/html; charset=UTF-8"
	pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>EL</title>
</head>
<body>
	<!-- 리퀘스트 영역에서 id 를 꺼내보자 -->
	<!-- == -->
	<%= request.getParameter("id") == "main" %><br/>
	<!-- .equals -->
	<%= request.getParameter("id").equals("main") %><br/>


	<!-- ==연산자는 .equals 처럼 동작한다 -->
	<!-- EL == -->
	== (EL) : ${param.id == "main"} <br/>
	<!-- EL .equals -->
	eq (EL) : ${param.id eq "main"} <br/>
</body>
</html>
```
### 내장 객체
#### JSP
| 객체          | 타입        | 설명                            |
|-------------|-----------|-------------------------------|
| pageContext | Java Bean | 현재 페이지의 page context instance |
#### Scope
| 객체               | 타입  | 설명                                 |
|------------------|-----|------------------------------------|
| pageScope        | Map | page 기본 객체에 저장된 속성을 저장하는 객체        |
| requestScope     | Map | request 기본 객체에 저장된 속성을 저장하는 객체     |
| sessionScope     | Map | session 기본 객체에 저장된 속성을 저장하는 객체     |
| applicationScope | Map | application 기본 객체에 저장된 속성을 저장하는 객체 |
#### Request Parameter
| 객체          | 타입  | 설명                                                                                      |
|-------------|-----|-----------------------------------------------------------------------------------------|
| param       | Map | JSP 내장 객체 request의 getParameter(name) 메서드와 동일한 역할<br/> ${param.name} / ${param["name"]} |
| paramValues | Map | JSP 내장 객체 request의 getParameterValues(name) 메서드와 동일한 역할                                 |

#### Cookie
| 객체     | 타입  | 설명                             |
|--------|-----|--------------------------------|
| cookie | Map | request 안에 있는 cookie를 가져올 수 있음 |
#### Request Header
| 객체           | 타입  | 설명                                    |
|--------------|-----|---------------------------------------|
| header       | Map | request의 getHeader(name) 메서드와 동일한 역할  |
| headerValues | Map | request의 getHeaders(name) 메서드와 동일한 역할 |

```java
<%@ page language="java" contentType="text/html; charset=UTF-8"
	pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>EL</title>
</head>
<body>
    <%pageContext.setAttribute("name", "page main");
    request.setAttribute("name", "request main");
    session.setAttribute("name", "session main");
    application.setAttribute("name", "application main");
    %>

    <%= pageContext.getAttribute("name") %><br>
    ${pageScope.name}<br>
    ${requestScope.name}<br>
    ${sessionScope.name}<br>
    ${applicationScope.name}<br>
    ${cookie.JSESSIONID.value}<br>
	
    <h3>나는 누구?</h3>
    <!-- 가장 작은 단위에서부터 찾아서 올라가 값을 반환한다-->
    ${name}
</body>
</html>
```