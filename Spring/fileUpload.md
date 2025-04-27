### MultiPartResolver
- multipart/form-data 요청을 해석해 MiltipartFile로 변환

### MultipartFile
- 업로드된 파일을 표현하는 인터페이스
- 파일 이름, 파일 내용(byte[]), 저장 메서드 등 제공

### 폼 인코딩 타입
- 파일 업로드를 하기 위해 HTML form의 `enctype="multipart/form-data`로 설정

---
### 필터 vs 인터셉터 vs AOP
| 구분   | 실행 시점                            | 적용 범위       | 구현방식                 | 목적              |
|------|----------------------------------|-------------|----------------------|-----------------|
| 필터   | DispatcherServlet 실행 전           | HTTP 요청/응답  | javax.servlet.Filter | 인증, 인코딩, 보안     |
| 인터셉터 | DispatcherServlet과 Controller 사이 | 스프링 MVC 요청  | HandlerInterceptor   | 인증, 권한 검사, 로깅   |
| AOP  | 메서드 호출 전후                        | 비즈니스 로직 메서드 | Aspect+Proxy         | 트랜잭션, 로깅, 성능 측정 |
