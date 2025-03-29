## Cookie


: 웹 서버가 클라이언트의 웹 브라우저에 저장하는 작은 데이터 조각
- (팔요에 따라) 요청 시, 서버로 함께 전송
- Key-Value 형태의 문자열 데이터
  - 이름(key), 값(value), 만료일(expire date), 도메인 경로(path) 등
- 웹 브라우저(client)별로 별도 Cookie 생성
  - 브라우저가 다르면 다른 사용자
- client에 최대 300개 cookie 저장 가능
- 하나의 도메인 당 20개 cookie 저장 가능
- 1 cookie 4KB 제한
---
### 사용 목적
- 세션 관리(아이디, 장바구니 등)
- 사용자가 설정한 환경 등을 기억해 페이지 제공
- 사용자 행동/패턴 분석
- 사용자의 관심에 따른 광고 targeting 등
### 동작 순서
1. Client 요청 생성
2. WAS가 cookie 생성, HTTP Header에 cookie 넣어 응답
3. Client의 cookie 저장, 해당 서버에 요청할 때 요청과 함께 cookie 전송
   - (client에 저장하기 때문에)공유 pc의 경우 보안 취약
4. cookie는 브라우저가 종료되어도 저장된 상태 -> 만료 기간 전까지 동일 사이트 재방문 해 요청 시, 필요에 따라 cookie 재전송 됨
---
### Cookie 메서드

| 메서드                             | 설명             |
  |---------------------------------|----------------|
| void setComment(String comment) | 쿠키에 대한 설명 설정   |
| void setDomain(String domain)   | 쿠키의 유효한 도메인 설정 |
| void setMaxAge(int expiry)      | 쿠키 유효 기간 설정    |
| void setPath(String path)       | 쿠키 유효 디렉토리 설정  |
| void setValue(String value)     | 쿠키 값 설정        |
| String getComment()             | 쿠키 설명 반환       |
| String getDomain()              | 쿠키 유효 도메인 반환   |
| String getMaxAge()              | 쿠키 유효 기간 반환    |
| String getPath()                | 쿠키 유효 디렉토리 반환  |
| String getValue()               | 쿠키 값 반환        |