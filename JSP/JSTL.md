## JSTL(JSP Standard Tag Library)


: JavaEE 기반 웹 어플리케이션 개발을 위한 컴포넌트 모음
- JSP 스트립트와 HTML 코드가 혼재되어 복잡한 구조 -> 이를 간결하게 작성하기 위해 자바 코드를 태그 형태로 작성해둔 것
- 유용한 custom tag들을 모아 표준화 한 것
### JSTL 기능
- 간단한 프로그램 로직 구현 O -> e.g.) 변수 선언, if문, for문, ...
- 데이터 출력 포맷 설정
- DB 입력/수정/삭제/조회
- 문자열 처리 함수
- XML 문서 처리
### JSTL 사용
- `taglib` 지시자를 사용한 태그 사용 선언
```java
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
```
- 사용할 태그 구분을 위한 `prefix` 작성
#### Core
#### 변수 지원
| 태그     | 설명                           |
|--------|------------------------------|
| set    | JSP에서 사용할 변수를 지정된 범위 속성으로 설정 |
| remove | 설정한 변수 제거                    |
#### 흐름 제어
| 태그        | 설명                 |
|-----------|--------------------|
| if        | 조건에 따라 내부 코드 수행    |
| choose    | 다중 조건 처리           |
| forEach   | 컬렉션 각 항목에 대한 반복 처리 |
| forTokens | 구분자로 분리된 각각의 토큰 처리 |
#### 기타 태그
| 태그    | 설명                        |
|-------|---------------------------|
| catch | 예외 처리에 사용                 |
| out   | 변수나 표현식의 결과를 HTML 출력에 쓸 때 |

```java
<%@ page language="java" contentType="text/html; charset=UTF-8"
	pageEncoding="UTF-8"%>
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>JSTL</title>
</head>
<body>
	<c:out value="hello main"></c:out>	<br>
	<c:out value="hello main"/>	<br>
	
	<!-- c:set 써보기 var/value/scope[옵션] -->
	<c:set var="msg" value="Hell main"/>
	<c:set var="msg2">hell main2</c:set>
	
	${msg}<br>
	${msg2}<br>
	
	<c:set var="p" value="<% new dto.Person() %>"/>
	<c:set target="${p}" property="name" value="메인"/>
</body>
</html>
```
```java
<c:if test="${param.fruit == 1}">
		<div style="color: yellow">파인애플</div>
	</c:if>
	<c:if test="${param.fruit == 2}">
		<div style="color: pink">망고스틴</div>
	</c:if>
	<c:if test="${param.fruit == 3}">
		<div style="color: green">멜론</div>
	</c:if>
	<c:if test="${param.fruit == 4}">
		<div style="color: red">사과</div>
	</c:if>
	
	<hr>
	<!-- 다중조건을 처리할 때 -->
	<c:choose>
		<!-- if의 느낌 -->
		<c:when test="${param.fruit == 1}"></c:when>
			<div style="color: yellow">파인애플</div>
		<c:when test="${param.fruit == 2}"></c:when>
			<div style="color: pink">망고스틴</div>
		<c:when test="${param.fruit == 3}"></c:when>
			<div style="color: green">멜론</div>
		<!-- else 느낌 -->
		<c:otherwise>
			<div>그 외 기타 과일입니다.</div>
		</c:otherwise>
	</c:choose>
```
```java
<!--
		크게 2가지
		1. 내가 반복할 친구
		2. 어떤 변수로 활용할 건지
		-->
	<c:forEach var="drama" items="${dramaList}">
		${drama}<br>
	</c:forEach>
	
	<hr>
	<c:forEach var="drama" items="${dramaList}" varStatus="status" begin="1" end="4" step="2">
		${status.index} : ${drama} |
		${status.count} : ${drama}<br>
	</c:forEach>
	
```
```java
<c:forEach var="item" items="${paramValues.dish}" varStatus="status">
		${item} <c:if test="${not status.last}">, </c:if>
	</c:forEach>
```
```java
<c:forTokens var="campus" items="서울, 대전, 광주. 구미. 부울경" delims=",">
		${campus}<br>
	</c:forTokens>
	<c:forTokens var="campus" items="서울, 대전, 광주. 구미. 부울경" delims=",.">
		${campus}<br>
	</c:forTokens>
```
```java
<c:catch var="errmsg">
		<div>예외 발생 전</div>
		<div><%= 2/0 %></div>
		<div>예외 발생 후</div>
	</c:catch>
	${errmsg}
```

---
## EL + JSTL 사용 이유
1. 코드 간결화
2. HTML(XML) 문법 친화적
3. Java와 함께 혼용된 상태의 가독성 부족 문제 개선
4. JSP 내의 모든 비즈니스 로직 제거
   - 순수하게 화면에 출력될 코드만 관리 가능
   - JSP 역할: View
5. 보안
   - 제약사항에 의해 스크립트 삽입, 사용자 입력 X = 일부 안정성 확보 O
   - e.g.) null값인 경우 "null"로 출력되던 부분을 아예 보이지 않게 하기, ...
---
#### 동작 방식
- 내부적으로 p.getName()이라는 getter 호출
- p.name 직접 호출
- 없으면 에러 반환
---
#### Scope 객체
page -> request -> session -> application 내에 있는 속성 호출