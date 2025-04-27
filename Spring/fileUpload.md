### MultiPartResolver
- multipart/form-data 요청을 해석해 MiltipartFile로 변환

### MultipartFile
- 업로드된 파일을 표현하는 인터페이스
- 파일 이름, 파일 내용(byte[]), 저장 메서드 등 제공

### 폼 인코딩 타입
- 파일 업로드를 하기 위해 HTML form의 `enctype="multipart/form-data`로 설정
