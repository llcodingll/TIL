## Stack

- 후입선출 (LIFO : Last-In First-Out) 구조
- Vector 기반으로 동작

| **메서드** | **내용** |
| --- | --- |
| push(E item) | 스택의 맨 위에 데이터를 추가 |
| pop() | 스택의 맨 위에 있는 데이터를 제거하고 반환 |
| peek() | 스택의 맨 위에 있는 데이터를 제거하지 않고 반환 |
| isEmpty() | 스택이 비어 있는지 확인 |
| size() | 스택에 저장된 요소의 개수를 반환 |


```java
		Stack<Integer> stack = new Stack<>();
		
		stack.add(1);
		stack.add(2);
		
//		System.out.println(stack.pop()); //가장 위에 있는거 빼기
//		System.out.println(stack.pop());
//		System.out.println(stack.pop()); //에러 -> 공백이니까

		System.out.println(stack.peek()); //가장 위에 있는거 읽기
```
---
## Queue

- 선입선출(FIFO : First-In First-Out) 구조
- 다양한 구현체 (LinkedList, ArrayDeque)가 있음

| **메서드** | **내용** |
| --- | --- |
| offer(E e) | 큐의 맨 뒤에 요소를 추가 ( 공간 부족 시 실패 반환 ) |
| add(E e) | 큐의 맨 뒤에 요소를 추가 ( 공간 부족 시 예외 발생 ) |
| poll() | 큐의 맨 앞 요소 제거 후 반환 ( 비어 있으면 null ) |
| remove() | 큐의 맨 앞 요소 제거 후 반환 ( 비어 있으면 예외 발생) |
| peek() | 큐의 맨 앞 요소 반환 ( 비어 있으면 null 반환 ) |
| element() | 큐의 맨 앞 요소 반환 ( 비어 있으면 예외 발생 ) |
| isEmpty() | 큐가 비어 있는지 확인 |
| size() | 큐에 저장된 요소의 개수를 반환 |


```java
		//FIFO
		Queue<Integer> queue = new LinkedList<>();
		
		//추가
		queue.add(1); //특정 상황에서 실패 반환
		queue.offer(2); //특정 상황에서 예외 반환
		
		//삭제
		System.out.println(queue.poll());
		System.out.println(queue.remove());
		
		System.out.println(queue.poll());//null
		System.out.println(queue.remove());//예외 발생
```
---
## Deque

- 양방향 큐 ( 양쪽에서 삽입과 삭제 가능)
- ArrayDeque (배열 기반), LinkedList (연결리스트 기반) 사용 가능

| **메서드** | **내용** |
| --- | --- |
| addFirst(E e) | 덱 맨 앞에 요소를 추가 ( 공간 부족 시 예외 발생 ) |
| addLast(E e) | 덱 맨 뒤에 요소를 추가 ( 공간 부족 시 예외 발생 ) |
| removeFirst() | 덱 맨 앞 요소 제거 후 반환 ( 비어 있으면 예외 발생 ) |
| removeLast() | 덱 맨 뒤 요소 제거 후 반환 ( 비어 있으면 예외 발생 ) |
| getFIrst() | 덱 맨 앞 요소 반환 ( 비어 있으면 예외 발생) |
| getLast() | 덱 맨 뒤 요소 반환 ( 비어 있으면 예외 발생 ) |
| isEmpty() | 덱이 비어 있는지 확인 |
| size() | 덱에 저장된 요소의 개수를 반환 |

```java
		//양방향 큐
		
		Deque<String> deque = new ArrayDeque<>();
		
		deque.addFirst("유아름");
		deque.addLast("박승연");
		deque.addFirst("이정은");
		
		System.out.println(deque);

```

```java
<결과>
[이정은, 유아름, 박승연]
```