## Insertion Sort


: 현재 위치에서 그 이하의 배열들을 비교해 현재 위치에 있는 값이 들어갈 위치를 찾아서 해당 위치에 삽입하는 알고리즘

---
### 기본 로직
1. 2번째 인덱스부터 시작해 현재 인덱스에 별도의 변수 저장 후, 비교 인덱스 = 현재 인덱스 -1로 설정
2. 저장해둔 삽입을 위한 변수 vs 비교 인덱스의 값
3. `삽입 변수의 값 < 현재 인덱스의 값`이면, 현재 인덱스로 비교 인덱스의 값 저장
4. 비교 인덱스 - 1로 비교 반복
5. `삽입 변수의 값 > 현재 인덱스의 값`이면, 비교 인덱스 + 1에 삽입 변수 저장

---
### 시간 복잡도
- 최악의 경우 : O(n^2)
- 이미 정렬되어 있는 경우 : O(n)
### 공간 복잡도
O(n)

---
### Code
```java
class Main {
    public static int[] arr = new int[5];

    public static void main(String[] args) {
        arr = new int[]{5, 4, 2, 1, 3};

        insertionSort(arr);
        for (int i = 0; i < 5; i++) {
            System.out.print(arr[i] + " ");
        }
    }
    public static insertionSort(int[] arr){
        for (int i = 0; i < 5; i++) {
            int select = arr[i];
            int vs = i - 1;
            while (vs >= 0 && arr[vs] > select) {
                arr[vs + 1] = arr[vs];
                vs--;
            }
            arr[vs + 1] = select;
        }
    }
}
```