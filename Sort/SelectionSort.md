## Selection Sort


: 현재 위치에 들어갈 값을 찾아 정렬하는 알고리즘
- Min-Selection Sort : 오름차순
- Max-Selection Sort : 내림차순

---
### 기본 로직
1. 정렬되지 않은 인덱스의 맨 앞부터, 그 이후 값 중 가장 작은 값 탐색
2. 가장 작은 값을 찾으면 해당 값을 현재 인덱스의 값과 swap
3. 다음 인덱스에서 해당 과정 반복

---
### 시간 복잡도
O(n^2)
### 공간 복잡도
O(n)

---
### Code
```java
class Main{
    public static int[] arr = new int[5];

    public static void main(String[] args) {
        arr = new int[]{5, 4, 2, 1, 3};
        
        selectionSort(arr);
        for (int i = 0; i < 5; i++) {
            System.out.print(arr[i] + " ");
        }
    }
    static void selectionSort(int[] arr){
        for (int i = 0; i < 5; i++) {
            int minIdx = i;
            for (int j = i+1; j < 5; j++) {
                if(arr[j] < arr[minIdx]){
                    minIdx = j;
                }
            }
            int tmp = arr[i];
            arr[i] = arr[minIdx];
            arr[minIdx] = tmp;
        }
    }
}
```