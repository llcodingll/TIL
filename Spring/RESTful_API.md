### @RestController


: @Controller + @ResponseBody
- view를 반환하지 않고, JSON/XML 형태로 데이터 반환

#### HTTP 메서드 매핑
| HTTP 메서드 | 기능    |
|----------|-------|
| GET      | 조회    |
| POST     | 생성    |
| PUT      | 전체 수정 |
| PATCH    | 부분 수정 |
| DELETE   | 삭제    |

#### RESTful 설계 원칙
- 리소즈 중심 URL 사용
  - `(boards/1/comments)`
- 상태 없이 설계
- 표준 HTTP 메서드 사용