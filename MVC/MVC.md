## MVC


: SW 공학에서 사용되는 디자인 패턴
- Model, View, Controller
- 각 부분 간 의존성 최소화로 유연/확장 가능 구조 제공
---
### 게층형
#### Controller
- Web MVC Controller, API 생성
#### Service
- 핵심 비즈니스 로직 구현
#### Repository
- DB 접근, domain 객체를 DB에 저장/관리
- interface : 아직 DB가 확정되지 않아 우선 interface로 구현 클래스 변경할 수 있도록 설계 예정
#### Domain
- DB에 저장/관리되는 비즈니스 도메인 객체
- e.g.) 회원, 주문, 쿠폰, ...
#### DB

---
### Model


: 어플리케이션의 비즈니스 로직 && 데이터 로직 처리
- Service
  - client에 대한 서비스 기능 제공
  - repository 이용해 데이터 가져오고, 결과 가공해 client에게 반환
  - 부가적 로직 처리
  - 사용자 친화적
- repository
  - CRUD 작성
  - DB와의 통신 처리
  - DB 친화적
---
### View


: 사용자가 데이터를 볼 수 있도록, 시각적 표현
- 로직을 위한 코드 X
- 오로지 출력
---
### Controller


: View, Model 사이에 실행 흐름 제어
- client로부터 요청 받아 분석
- 비즈니스 로직 수행할 service 호출
- 로직 결과를 보여주기 위한 View 선택해 호출