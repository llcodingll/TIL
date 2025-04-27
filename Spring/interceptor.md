### 인터셉터 생명주기
| 메서드             | 호출 시점              | 주요 역할           |
|-----------------|--------------------|-----------------|
| preHandle       | 컨트롤러 실행 전          | 인증, 권한 확인 등     |
| postHandle      | 컨트롤러 실행 후, 뷰 렌더링 전 | 추가 모델 데이터 처리    |
| afterCompletion | 뷰 렌더링 완료 후         | 리소스 해제, 예외 로깅 등 |
### 인터셉터 체이닝
- 여러 인터셉터를 순서대로 등록해 연결 실행
- 등록 순서대로 preHandle 순방향 -> afterCompletion 역방향 호출
### 인터셉터 등록 방법
`WebMvcConfigurer` 인터페이스 구현해 `addInterceptors(InterceptorRegistry registry)` 메서드에서 등록