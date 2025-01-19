## JPQL vs Querydsl


: 동적쿼리

---
### JPQL: JPA의 일부


: Query를 Table이 아닌 Entity 기준으로 작성 = 객체 지향 쿼리 언어
- table에 매핑되는 객체 존재할 것
- 검색 시, table이 아닌 entity를 대상으로 검색할 것

---
### JPQL의 문제점
- String 형태로 쿼리문을 작성하기 때문에 컴파일 시 오류 발견 불편
- 복잡한 코드를 작성할 때, 당연히 더 찾기 힘듦

---
위의 문제를 해결하기 위해 Querydsl이 등장하면서부터 이를 사용하는 곳이 많아짐.
### Querydsl


: HQL, Hibernate Query Language = 정적 타입을 이용해 SQL 같은 쿼리 생성 도움
- JAVA 코드로 SQL문을 작성할 수 있어 컴파일 시에 오류 발생해 이전보다 잘못된 쿼리를 빠르게 잡아낼 수 O

---
### 차이
#### JPQL
```java
String name = "Java";
String jpql = "select u from User u where u.name = :name";

List<User> result = eu.createQuery(query, User.class).getResultList();
```
이런 식으로 String 타입이기 때문에 오타도 관리하기 힘듦 + 컴파일 단계에서 당연히 오류 발생 X = 오류 찾아내기 힘들어 개발 시간 더 소요

#### Querydsl
```java
String name = "Java";

List<User> result = queryFactory
        .select(user)
        .from(user)
        .where(nameEq(name))
        .fetch();
```
`.select`, `.from`, `.where`, `.fetch`와 같은 코드를 사용하기 때문에 오타 발생 확률 감소 + 컴파일 단계에서 오류 빠르게 발견 가능

---
### 차이 더 알아보기(`동적쿼리`)
데이터의 양이 방대해졌을 때, 페이징, 최신순/오래된순, 추천순, 생성일자순, 가나다순 등등 다양한 조건을 포함하는 조회를 해야 할 필요가 있다.

이때, JPQL로 작성하게 된다면 코드 자체의 가독성도 좋지 않고, 결국 사람이 코드를 작성하는 것이기 때문에 실수해 오류를 잡는 데에 많은 시간을 쏟을 가능성이 있다.

따라서 이런 경우를 대비해 가독성이 높고 컴파일 오류를 발견할 수 있도록 Querydsl을 사용한다.

---
#### 덧붙이기
Repick 프로젝트에서 Querydsl을 사용한 것도, 사용자가 더 많은 조건을 포함하는 검색을 하기에 용이한 환경을 만들고 싶었고, 이후 추가 개발이 이루어졌을 때 검색 조건에 좋아요순, 조회순, 댓글순, 최신순, 사용자순 등등 많은 조건이 추가될 것이라는 회의가 있었기 때문에 추후 개발에서 보수하기 용이한 형태를 만들고자 Querydsl을 사용했다.