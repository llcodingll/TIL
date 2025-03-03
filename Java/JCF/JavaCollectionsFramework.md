## Java Collections Framework


: Data Structure -> 자바 클래스로 구현한 모음


: 크게 `Collection` 인터페이스와 `Map` 인터페이스로 나뉨

---
### 장점
- 인터페이스, 다형성을 이용한 `객체지향적` 설계로 표준화되어 사용법 숙지 용이 + 재사용성 up
- 데이터 구조, 알고리즘의 고성능 구현 제공으로 프로그램 `성능/품질 향상`
- 관련없는 API 간의 상호 운용성 제공(상위 인터페이스 타입으로 업캐스팅해 사용)
- 이미 구현되어 있는 API 사용해 새 API 설계 시간 down
- 소프르웨어 재사용성 up, 컬렉션 활용해 새 알고리즘 생성 가능
---
# Collection

→ `순서나 집합이 있는` 저장 공간 (List, Set의 조상인 인터페이스)

List와 Set의 조상 인터페이스인 Collection은 배열과 같이 개체에 대한
참조와 그룹으로 관리할 수 있다는 점에서 동일하지만,

- 특정 용량을 할당할 필요가 없음 (요소 추가 & 제거 시에도 자동으로 처리 가능)
- primitive type(기본 타입)을 요소로 사용할 수 없음
   → 래퍼 클래스를 이용하여 사용

```java
    import java.util.ArrayList;
    import java.util.List;
    
    public class Test{
        public static void main(String[] args) {
            
            List<Integer> lst = new ArrayList<>();
    
            lst.add(10);
            lst.add(20);
            lst.add(30);
    
            for (int i = 0; i < lst.size(); i++) {
                int temp = lst.get(i);
                System.out.println(temp);
            }
            for (int temp : lst) {
                System.out.println(temp);
            }
        }
    }
```

#### 핵심 메서드

```java
public interface Collection<E> extends Iterable<E> {
	int size();
	boolean isEmpty();
	boolean contains(Object o);
	Iterator<E> iterator();
	Object[] toArray();
	<T> T[] toArray(T[] a);
	boolean add(E e);
	boolean remove(Object o);
	boolean containsAll(Collection<?> c);
	boolean addAll(Collection<? extends E> c);
	boolean removeAll(Collection<?> c);
	default boolean removeIf(Predicate<? super E> filter);
	boolean retainAll(Collection<?> c);
	void clear();
	boolean equals(Object o);
	int hashCode();
	default Spliterator<E> spliterator();
	default Stream<E> stream();
	default Stream<E> parallelStream();
}
```
