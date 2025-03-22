## GET


: 저장된 리소스에서 데이터 `요청`하는 데에 사용
- Query String(name/value 쌍)이 URL에 포함되어 전송
  - POST와 비교해 보안 취약
- URL 길이 제한이 있으므로, 전송 가능한 데이터 길이 제한적(URL maximum charaters: 2048)
- Only ASCII 문자
---
## POST


: 리소스 생성/업데이터 하기 위해 서버에 데이터를 `보내는` 데에 사용
- HTTP header의 body에 파라미터 포함해 전송
- 데이터 길이 제한 X
- 매개변수가 브라우저나 웹 서버에 저장되지 않음
- 제한 없음, 바이너리 데이터도 허용