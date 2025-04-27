###  DispatcherServlet과 요청 처리 흐름
- 모든 요청을 받아 컨트롤러에 전달하는 Front Controller 역할

> 흐름 <hr/>
> client request -> DispatcherServlet 수신
> -> HandlerMapping으로 controller 탐색
> -> Controller의 요청 처리
> -> ViewResolver를 통해 View 선택
> -> response 생성 -> client 반환
- HandlerMapping: 요청 URL과 컨트롤러 메서드 매핑 정보 관리하는 컴포넌트
#### Annotation
| Annotation                   | 설명                                    |
|------------------------------|---------------------------------------|
| @RequestMapping              | URL과 모든 메서드(GET/POST/PUT/...) mapping |
| @GetMapping<br/>@PostMapping | 간편한 GET/POST mapping                  |
| @PathVariable                | URL 경로의 변수 추출(/users/{id})            |
| @RequestParam                | 쿼리 스트링 또는 폼 데이터 추출(/search?query=abc) |
| @ResponseBody                | 객체를 JSON/XML로 변환해 HTTP 응답             |