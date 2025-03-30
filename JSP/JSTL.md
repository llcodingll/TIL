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
---
### 1. `<c:forEach>` – 반복문
리스트, 배열, 범위 등 반복 출력할 때 사용
```
<c:forEach var="item" items="${list}" varStatus="status">
   ${status.index} : ${item}
</c:forEach>
```
### 주요 속성
| 속성                     | 설명                       |
|------------------------|--------------------------|
| `var`                  | 각 반복 요소를 저장할 변수          |
| `items`                | 반복할 컬렉션 (List, 배열 등)     |
| `varStatus`            | 루프 상태 정보를 담는 객체          |
| `begin`, `end`, `step` | 정수 범위 지정 시 사용 (0부터 시작 등) |

`varStatus` 속성 사용 예

| 속성      | 설명             |
|---------|----------------|
| `index` | 0부터 시작하는 인덱스   |
| `count` | 1부터 시작하는 반복 횟수 |
| `first` | 첫 번째 반복이면 true |
| `last`  | 마지막 반복이면 true  |

---

### 2. `<c:if>` – 단일 조건 분기
- `test` 속성에 조건식을 넣고, true일 때만 실행됩니다.
- `else` 없음 → 다중 조건은 `<c:choose>` 사용
```
<c:if test="${user.age >= 20}">
   성인입니다.
</c:if>
```
---
### 3. `<c:choose>`, `<c:when>`, `<c:otherwise>` – 다중 조건 (if-else if-else)
```
<c:choose>
   <c:when test="${user.grade == 'A'}">우수</c:when>
   <c:when test="${user.grade == 'B'}">보통</c:when>
   <c:otherwise>재시험</c:otherwise>
</c:choose>
```
- `<c:when>`은 여러 개 가능
- `<c:otherwise>`는 마지막 기본값
---
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