## HTTP


: Hyper Text Transfer Protocol
- 웹 서버-브라우저 간의 통신
- HTML, IMAGE, VIDEO, JSON 등 데이터 전송 가능
- 기본 포트: 80


: 보안 버전: Https(Hyper Text Transfer Protocol Secure)
- 기본 포트: 443
- 클라이언트-서버 구조

### 인터넷 프로토콜


: 인터넷에서 데이터 통신을 위한 표준화된 규약/규칙
- TCP(Transmission Control Protocol)
- UDP(User Datagram Protocol)
  - 컴퓨터 동작 유무 상관 없이 전송 = TCP보다 빠름
---
### HTTP 특징
#### Connectionless
- 지속적 연결 유지로 자원낭비 방지를 위해 연결 해제
- 서버 자원 효울적 사용
#### Stateless
- 서버가 클라이언트 상태 저장 X
- 클라이언트 상태를 알 수 없기 때문에 추가적 데이터 전송 필요
- 응답 서버 변경 용이
  - e.g.) A점원, B점원, 결제 상황
  - A점원에게 계산 요청 -> 카드/현금 선택 -> A점원이 없는 경우 -> B점원에게 카드를 건네면 바로 결제하기에는 상황 설명 필요 -> B점원에게 카드로 결제하겠다는 의사표현(추가적 데이터 전송)
- 브라우저 쿠키/서버 세션 등 이용해 상태 유지
---
### HTTP 상태 코드
#### 1xx : Informational responses
#### 2xx: Successful responses
#### 3xx: Redirection messages
#### 4xx: Client error responses
#### 5xx: Server error responses