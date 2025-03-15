## Bubble Sort


: 연속된 2개의 인덱스를 비교해, 기준 값을 뒤로 넘겨 정렬하는 방법
- 오름차순: 큰 값을 뒤로 이동시켜 가장 큰 값을 가장 뒤에 저장
---
### 기본 로직
1. 현재 인덱스 값 vs 바로 이전 인덱스 값
2. 이전 인덱스의 값이 더 크면, 현재 인덱스의 값과 swap
3. 현재 인덱스의 값이 더 크면, 교환하지 않고 다음 두 연속된 배열의 값 비교
4. (전체 배열 크기 - 현재까지 순환한 바퀴 수) 만큼 반복

### 시간 복잡도
O(n^2)
### 공간 복잡도
O(n)

---
### Code
```java
class Main {
    public static int[] arr = new int[5];

    public static void main(String[] args) {
        arr = new int[]{5, 4, 2, 1, 3};
        
        bubbleSort(arr);

        for (int i = 0; i < 5; i++) {
            System.out.print(arr[i] +" ");
        }
    }
    static void bubbleSort(int[] arr){
        int tmp = 0;
        for (int i = 0; i < 5; i++) {
            for (int j = 1; j < 5-i; j++) {
                if(arr[j] < arr[j-1]) {
                    tmp = arr[j - 1];
                    arr[j - 1] = arr[j];
                    arr[j] = tmp;
                }
            }
        }
    }
}
```
