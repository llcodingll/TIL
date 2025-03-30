## Forward
- request 발생 시, 요청 받은 JSP 또는 Servlet이 직접 응답을 작성하지 않고
- 요청을 `서버내부에서 전달해` 해당 요청을 처리
```java
RequestDispatcher dispatcher = request.getRequestDispatcher("이동할 페이지");
dispatcher.forward(request, response);
```
- requst, response 객체가 전달되어 

### 특징
- 사용자 브라우저 상 URL 변함 X
- 서버 상에서 forward 방식으로 페이지 이동 처리 시, 기존에 있던 servlet 또는 JSP에서의 출력 buffer 소멸
  - 출력 buffer의 소멸?
    - response 객체를 통해 기존에 출력(write, print, println, ...)했던 데이터 소멸
    - forward 방식을 통해 request, response 객체를 넘기에 되면 모든 기존 출력들 소멸
  - 유지하는 방법?
    - `include` 메서드 사용
      - 기존의 servlet 내 출력 결과 포함해 화면에 보여줄 수 O
      - 이 경우, 기존 buffer가 지워지는 것이 아니기 때문에 기존의 페이지 내에 2번째 페이지가 혼재되어 출력될 수 있음에 유의

---
## Redirect
- request 발생 시 `내부로직 실행 후`, 브라우저의 `URL을 변경`하도록 해 새로운 요청 생성함으로써 페이지 이동
```java
response.sendRedirect("location");
```