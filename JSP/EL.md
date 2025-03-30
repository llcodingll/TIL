## EL(Expression Language)


: JSP 내에서 데이터를 다룰 때, 사용되는 scripting language
- `<% %>` 보다 속성값을 쉽게 출력 하기 위함 ⇒ `${}`
- `${}`: 변수, 속성, 메서드 호출 등 포함 O

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