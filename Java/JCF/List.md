## List Interface


: 순서가 있는 저장공간


e.g.) ArrayList, LinkedList, Vector, Stack
- 저장 순서 유지 
- 같은 요소 중복 저장 가능
- 배열처럼 index 요소로 접근 가능
- 요소 사이 빈공간 비허용 == 삽입/삭제 시 배열 이동 발생
### List vs Array
- List: 자료형의 크기가 데이터 양에 따라 동적으로 변함(가변)

#### 주요 메서드
```java
public interface List<E> extends Collection<E> {
	//컬렉션과 중복은 제외...
	default void replaceAll(UnaryOperator<E> operator);
	default void sort(Comparator<? super E> c);
	E get(int index);
	E set(int index, E element);
	void add(int index, E element);
	int indexOf(Object o);
	int lastIndexOf(Object o);
	ListIterator<E> listIterator();
	ListIterator<E> listIterator(int index);
	List<E> subList(int fromIndex, int toIndex);
}
```
---
### ArrayList


: 내부적으로 배열의 구조를 가지고 있으며, 크기가 가변적으로 바뀌는 선형구조

*capacity (용량)을 넘는 경우에 resize가 일어나, capacity를 확보
- 배열 기반의 구현
- 인덱스를 통한 접근이 빠름
- 데이터 삽입, 삭제가 빈번한 경우 성능 저하 (많은 데이터 이동)
- 데이터의 조회가 많고, 삽입/삭제가 적은 경우 유용
- 앞의 내용을 비워둘 수 없음 (index 0 을 비우고 1을 채울 수 없음 → 앞으로 밀착됨)
- 중간(index n)에 삽입한다면 n뒤의 자료들을 한칸 뒤로 밀림
- 어느정도 데이터가 차면, 더 큰 데이터를 자체적으로 만든 뒤 바꿈
  반대로 데이터가 너무 적다면, 더 작은 데이터로 자체적으로 만들어 바꿈

#### 주요 메서드
```java
public class ArrayList<E> extends AbstractList<E>
        implements List<E>, RandomAccess, Cloneable, java.io.Serializable
{
	// transient Object[] elementData;
	// private int size;
	public ArrayList(int initialCapacity);
	public ArrayList();
	public ArrayList(Collection<? extends E> c);
	public void trimToSize();
	public void ensureCapacity(int minCapacity);
	protected void removeRange(int fromIndex, int toIndex);
	public ListIterator<E> listIterator(int index);
	/*
	*	Collection, List 인터페이스 구현 메소드는 생략 
	*/
	public ListIterator<E> listIterator();
	public Iterator<E> iterator();
	private class Itr implements Iterator<E> {};
}
```
---
### LinkedList


: Node가 데이터와 다음 노드의 참조를 포함하는 방식으로 구성된 자료구조
- 연속된 메모리 공간에 저장하는 배열과는 달리 비연속적 위치에 저장 가능
- 자료구조의 크기를 동적으로 조정할 수 있어 메모리 효율적
- 처음 노드의 위치를 저장하는 Head 필요

#### 주요 메서드
```java
public class LinkedList<E>
    extends AbstractSequentialList<E>
    implements List<E>, Deque<E>, Cloneable, java.io.Serializable {
    // transient int size = 0;
    // transient Node<E> first;
    // transient Node<E> last;

    /** 생성자 */
    public LinkedList();

    public LinkedList(Collection<? extends E> c);

    /** get, add & remove, peek & poll, offer, push & pop */
    public E getFirst();

    public E getLast();

    public E removeFirst();

    public E removeLast();

    public void addFirst(E e);

    public void addLast(E e);

    public E peek();

    public E peekFirst();

    public E peekLast();

    public E poll();

    public E pollFirst();

    public E pollLast();

    public boolean offer(E e);

    public boolean offerFirst(E e);

    public boolean offerLast(E e);

    public void push(E e);

    public E pop();

    /** iterator */
    public ListIterator<E> listIterator(int index);

    private class ListItr implements ListIterator<E> {}
}
```
| **메서드** | **내용** |
| --- | --- |
| add(E e) | 데이터 추가 (마지막 위치) |
| add(int index,E e | 데이터 추가 (index 위치) |
| get(int index) | 데이터 변환 (index 위치) |
| set(int index, E e) | 데이터 수정 (index 위치) |
| remove(int index) | 데이터 삭제 (index 위치) |
| remove(Object o) | 데이터 삭제 (index 위치) |
| size() | 컬렉션의 크기를 반환 |
| isEmpty() | 컬렉션이 비어 있는지 확인 |
| contains(Object o) | 특정 데이터가 포함되어 있는지 확인 |
| indexOf(Object o) | 특정 데이터의 첫 번째 위치 반환 |
| clear() | 컬렉션의 모든 요소 삭제 |
#### Node


:자료구조에서 데이터를 저장하는 기본 단위
- 구성 요소
    - 데이터 필드: 노드가 저장하는 값(숫자, 문자열, 객체, …)
    - 링크 필드: 다음 노드를 가리키는 참조(:다음 노드를 가리키는 주소)

*사용하는 자료구조에 따라 링크 필드가 여러 개 존재할 수  O
#### LinkedList vs Array
| 비연속적 | 연속적 메모리 공간 |
| --- | --- |
| 동적 | 정적 할당 |
| O(n): 처음부터 탐색 | O(1): index 접근 |
| 링크 필드 수정 | 앞으로/뒤로 밀착 |
| 데이터+링크 저장 | 데이터만 저장 |
| 크기가 자주 변하는 경우 | 빠른 접근이 필요한 경우 |
---
### Singly Linked List


: 각 노드가 하나의 링크 필드에 의해 다음 노드와 연결되는 구조
- Head는 가장 앞의 노드를 가리키고, 각 노드는 다음 노드를 가리킴
- 마지막 노드의 링크 필드는 NULL → 다음이 없음을 알 수 있음

= 단순 연결 리스트