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
| 코드대     | 분류명                    | 설명             | 예시 상황                                               |
|---------|------------------------|----------------|-----------------------------------------------------|
| **1xx** | 정보(Informational)      | 요청 수신 중, 계속 진행 | 거의 사용되지 않음                                          |
| **2xx** | 성공(Success)            | 요청 정상 처리       | `200 OK`, `201 Created`                             |
| **3xx** | 리다이렉션(Redirection)     | 다른 URL로 이동     | `301 Moved`, `302 Found`, `304 Not Modified`        |
| **4xx** | 클라이언트 오류(Client Error) | **클라이언트 잘못**   | `400 Bad Request`, `401 Unauthorized`, `403`, `404` |
| **5xx** | 서버 오류(Server Error)    | **서버 내부 문제**   | `500 Internal Server Error`, `502`, `503`           |

### 자주 나오는 상태 코드 요약
| 코드              | 의미       | 언제 발생?                        |
|-----------------|----------|-------------------------------|
| **200 OK**      | 정상 응답    | 요청 성공                         |
| **201 Created** | 리소스 생성됨  | POST로 새 데이터 등록                |
| **301/302**     | 리다이렉트    | URL 이동됨                       |
| **304**         | 변경 없음    | 캐시 사용                         |
| **400**         | 잘못된 요청   | 파라미터 누락, JSON 오류 등            |
| **401**         | 인증 필요    | 로그인 안 한 상태에서 인증 필요한 자원 접근     |
| **403**         | 접근 금지    | 권한 부족                         |
| **404**         | 없음       | 잘못된 경로, 리소스 없음                |
| **500**         | 서버 내부 오류 | 예외 발생, NullPointerException 등 |

---

### 오류 코드 발생 주체
| 오류 코드   | 책임 주체                              |
|---------|------------------------------------|
| **4xx** | 클라이언트(브라우저, 앱) 실수                  |
| **5xx** | 서버(Spring, Servlet, DB 등)에서 발생한 오류 |