## Forward
- request 발생 시, 요청 받은 JSP 또는 Servlet이 직접 응답을 작성하지 않고
- 요청을 `서버내부에서 전달해` 해당 요청을 처리
```java
RequestDispatcher dispatcher = request.getRequestDispatcher("이동할 페이지");
dispatcher.forward(request, response);
```
- requst, response 객체가 전달되어 

---
## Redirect
- request 발생 시 `내부로직 실행 후`, 브라우저의 `URL을 변경`하도록 해 새로운 요청 생성함으로써 페이지 이동
```java
response.sendRedirect("location");
```