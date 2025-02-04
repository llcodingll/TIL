## JVM


: Java Virtual Machine
- 싱글 스레드
- 멀티 스레드
---
## JVM 메모리 구조
### Method Area


: 클래스 정보 저장
- 정적 변수(`static`), 상수, 메서드 등 저장
- `모든` 스레드가 공유
- Class Loader에 의해 클래스가 로드될 때, 저장되는 공간
```java
/*
* 클래스: 설계도
* 인스턴스: 설계도를 기반으로 만든 붕어빵
*/
이라고 했을 때, `설계도`가 저장되는 공간
```
- 이름이 Method인 이유: 설계도는 인스턴스 내의 필드가 가질 수도 있고, 메서드가 가질 수도 있기 때문
  - 필드는 인스턴스마다 고유
    - p1의 이름은 "yoo", p2의 이름은 "yoon"과 같이 고유
  - 메서드는 고유한가?
    - 공통으로 활용됨
    - e.g.) 잠자기, 이 닦기 등 특정 1명의 사람만 할 수 있는 행동 아님

=> `공통`이기 때문에 Method Area라고 명명

### Heap Area


: 객체 인스턴스 저장 공간
- GC가 관리하는 영역
  - 사용되지 않는 객체 자동 삭제
- 인스턴스 변수, 배열 등 저장
- 어플리케이션이 사용할 수 있는 가장 `큰` 메모리
- 모든 스레드가 공유

### Stack Area


: 지역 변수, 메서드 호출 시 사용되는 값, 연산 결과 등의 저장 공간
- 메서드 호출 시, 스택 프레임 생성
- 메서드 끝나면 스택 프레임 제거
- 스레드마다 생성
- Stack/Queue 자료구조

### PC Register


: 현재 실행 중인 메모리 주소 저장

### Native Method Area

---

### 객체 생성과 메모리 할당

```java
Person p1 = new Person();
p1.name = "Yoo";
p1.age = 24;
p1.hobby = "Coding";


Person p2 = new Person();
p2.name = "Yoon";
p2.age = 25;
p2.hobby = "Programming";
```
- Class Person은 Method Area에 클래스 로더 통해서
- Main 실행하는 건 Stack Area 가장 하단에
- Person의 name, age, hobby Heap Area에 참조(instance 변수)