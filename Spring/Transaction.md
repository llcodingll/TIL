### @Transactional


: 클래스나 메서드에 부여해 트랜잭션 범위 지정
- 성공 시 커밋, 예외 발생 시 롤백
```java
@Transactional
@Transactional(readOnly=true)
```