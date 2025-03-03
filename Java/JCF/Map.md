## Map Collections


: 키와 값의 쌍으로 데이터를 저장하는 구조
- 키를 기준으로 값에 접근하여 키는 중복을 허용하지 않음 (값은 허용)
- 키를 활용하여 빠른 검색 가능
- 키 또는 값에 null 허용 (일부 TreeMap 에서는 허용하지 않음)
- 구현 클래스
    - HashMap
    - LinkedHashMap
    - TreeMap
---
### HashMap

- 데이터의 저장 순서를 유지하지 않음
- 내부적으로 Hash Table을 사용하여 데이터 저장 및 검색
    - 순서대로 Hash Table에 저장되는게 아니라, 해쉬값에 따라 저장되는 것
    - 만약 동일한 Hash값을 갖게 된다면, 다시 부여해주던가, 체이닝을 사용하여 연결리스트로 관리
- null 키를 하나 허용하며, 여러 개의 null 값을 허용
- 빠른 검색, 삽입, 삭제를 지원

---
### LinkedHashMap

- 데이터의 저장 순서를 유지
- 내부적으로 Hash Table + 이중 연결 리스트를 사용하여 데이터 저장 및 검색
- null 키를 하나 허용하며, 여러 개의 null 값을 허용
- 빠른 검색, 삽입, 삭제를 지원
- 해시 충돌 시 HashMap과 동일하기 처리

---
### TreeMap

- 키를 기준으로 정렬된 상태로 데이터를 유지 (기본 오름차순)
- 사용자 정의 정렬이 필요한 경우 Comparator를 사용
- 내부적으로 레드 - 블랙 트리 기반으로 구현
- null 키는 허용하지 않음

---
### Map 주요 메서드
| **메서드** | **내용** |
| --- | --- |
| put(K key, V value) | 키 - 값 쌍을 추가 ( **이미 키가 존재하면 덮어씀**) |
| get(Object key) | 키에 해당하는 값을 반환 |
| remove(Ovject key) | 키의 값을 지우고 반환 |
| containsKey(Object key) | 특정 키가 있는지 확인 |
| containsValue(Object value) | 특정 값이 있는지 확인 |
| keySet() | 모든 키를 반환 (Set 형태) |
| values() | 모든 값을 반환 (Collection 형태) |
| isEmpty() | Map이 비어 있는지 확인 |
| size() | Map에 저장된 키 - 값 쌍의 개수를 반환 |

```java
//Map : 사전 같은 K-V 키-값의 쌍으로 이루어져 있음
//키는 중복 X / 값 중복 O / 순서 X(일부 있는 것들도 
		
		Map<String,String> map = new HashMap<>();
		
		map.put("김희망", "Java");
		map.put("강건", "Java");
		map.put("전해지", "Python");
		map.put("전해지", "한글"); //덮어씀

		
		System.out.println(map);
		
		System.out.println(map.keySet());
		//키들을 이용하여 전체 데이터를 가져올 수도 있다.
		for(String key:map.keySet()) {
			System.out.println(map.get(key));
		}
		//키값이 존재하는지
		System.out.println(map.containsKey("김희망"));
		
		//벨류값이 존재하는지
		System.out.println(map.containsValue("Python"));
```
