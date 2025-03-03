## Set Collections

- 중복 데이터 허용하지 않음
- 순서 보장하지 않음
- null 값 허용 (한 개 저장)
- 데이터의 고유성을 보장하기 위해 사용
- 구현 클래스
    - HashSet
    - LinkedHashSet
    - TreeSet
---
### HashSet

- 데이터의 저장 순서를 유지하지 않음
- HashMap 기반으로 동작 → 빠른 추가, 삭제, 검색이 가능
- null 값 하나 저장할 수 있음


💡 Hash : 데이터를 빠르게 저장하고 검색하기 위해 사용하는 특별한 값 또는 기법

→ 데이터를 고유한 숫자 값으로 변환하는 과정

```java
		Set<String> names = new HashSet<>();
		
		names.add("유아름");
		names.add("강건"); 
		names.add("박승연");
		names.add("강건"); 
		names.add("왕성민");
		names.add("강건");
		
		System.out.println(names);
```

```java
<결과>
[왕성민, 유아름, 박승연, 강건]
```
---
### LinkedHashSet

- 데이터의 저장 순서 유지
- LinkedHashMap 기반으로 동작 → 빠른 추가, 삭제, 검색 가능
    - 메모리를 더 많이 차지함
- 이중 연결 리스트를 이용하여 관리 (약간 더 느림)
- null값 하나 저장할 수 있음

---
### TreeSet

- 데이터가 정렬된 상태로 유지 (기본 오름차순)
- 사용자 정의 정렬이 필요한 경우 Comparator 사용 가능
- 내부적으로 이진 탐색 트리(레드 - 블랙 트리 [균형 유지]) 구조 사용
- null 값 저장 불가

### Set 주요 메서드
| **메서드** | **내용** |
| --- | --- |
| add(E e) | 데이터 추가 (중복인 경우 추가 X) |
| remove(Object o) | 데이터 삭제 (특정 데이터) |
| size() | Set의 크기를 반환 (요소 수) |
| isEmpty() | Set이 비어 있는지 확인 |
| contains(Object o) | 특정 데이터가 포함되어 있는지 확인 |
| clear() | 컬렉션의 모든 요소 삭제 |
| iterator() | Set을 순회할 수 있는 Iterator를 반환 |