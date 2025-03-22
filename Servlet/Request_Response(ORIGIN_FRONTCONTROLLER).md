## Servlet 요청과 응답
### ORIGIN(기존 방식)
- Mapping 주소마다 servlet 존재
- 많은 servlet 필요
> e.g.)
> 사용자가 게시글을 작성, 수정, 조회, 삭제할 때,
> 각각 하나의 Servlet 필요 => 총 4개의 Servlet이 Server에서 돌아가는 거야
---
### FRONT CONTROLLER
- 웹에서 발생하는 모든 요청에 대해 호출되는 Servlet 생성해 처리
> e.g.)
> 사용자가 게시글을 작성, 수정, 조회, 삭제할 때,
> 하나의 게시글 Servlet이 등록(), 수정(), 조회(), 삭제()를 수행