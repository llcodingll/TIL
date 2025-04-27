### mapper.xml
- SQL 작성 파일
- interface: 메서드 이름: mapper.xml의 SQL을 호출하는 Java 인터페이스
### parameterType과 resultType
- parameterType: SQL 실행 시 넘길 입력 파라미터 타입 지정
- resultType: SQL 실행 결과 매핑할 객체 타입 지정
### 동적 쿼리
```xml
<if></if>
<where></where>
<choose></choose>
```
조건에 따라 SQL문 동적 생성
### 조인 처리
- 여러 테이블 join 결과를 association(단일 관계) || collection(다대일 관계) 태그로 매핑
