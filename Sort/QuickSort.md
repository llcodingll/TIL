## Quick Sort


: 평균적인 상황에서 가장 좋은 성능을 가지는 정렬 알고리즘(feat. Pivot)

---
### 기본 로직
1. Divide: 배열에서 하나의 요소를 선택해 pivot으로 설정
    - pivot을 기준으로 pivot보다 작은 요소는 왼쪽, 큰 요소는 오른쪽으로 이동
2. Conquer: pivot 기준으로 분할된 2개의 부분 배열에 대해 부분 배열 크기가 1 이하가 되어 더 정렬할 수 없을 때까지 재귀적으로 퀵 정렬 수행
3. Combine: 모든 정렬된 부분 배열 결합해 정렬된 배열 만들기

---
### Code
```java
public class Main {
    public static void main(String[] args) {
        int[] arr = {60, 10, 30, 1, 4, 3, 31, 22};
        print(arr, 0, arr.length - 1, -1);
        sort(arr);
        print(arr, 0, arr.length, -1, -1);
    }
    
    static void print(int[] arr, int left, int right, int pivot){
       for (int i = 0; i < arr.length; i++) {
          if (i == left) {
             System.out.print("[");
          }
          if (i == pivot) {
             System.out.print("*");
          }
          System.out.print(arr[i]);
          if (i == right) {
             System.out.print("]");
          } else {
             System.out.print(" ");
          }
       }
       System.out.println();
    }
    
    static void swap(int[] arr, int i, int j) {
       int tmp = arr[j];
       arr[j] = arr[i];
       arr[i] = tmp;
    }

   static int partition(int[] arr, int low, int high) {
      int left = low;
      int right = high - 1;
      
      //pivot = 배열 끝 idx
      int p = high;
      int pivot = arr[p];
      
      //left idx가 right idx를 넘어서기 전까지 루프
      while (left <= right) {
          //pivot 왼 = 작은 값, 오른 = 큰 값으로 정렬
         // 조건에 맞지 않는 원소 찾아 교환
         while (left <= high && arr[left] < pivot) {
             left++; //pivot보다 큰 값 나올 때까지 왼쪽으로 이동
         }
         while (right >= low && arr[right] > pivot) {
             right--; //pivot보다 작은 값 나올 때까지 오른쪽으로 이동
         }
         
         //left와 right가 서로를 넘어서지 않고, 교환할 원소 찾으면
         if (left <= right) {
            swap(arr, left, right);
         }
      }
      
      //left, right 위치가 서로를 넘어서면 left와 pivot 위치 교환
      //pivot 왼 = 작은 값, 오른 = 큰 값으로 정렬
      swap(arr, p, left);
      return left; //변경된 pivot 위치인 left 반환
   }

   static void quickSort(int[] arr, int low, int high) {
      if (low < high) {
         int pivot = partition(arr, low, high); //퀵 정렬 phase 통해 정렬된 pivot 위치
         print(arr, low, high, pivot);
         quickSort(arr, low, pivot - 1); //pivot의 왼쪽 다시 퀵 정렬(작은 값들)
         quickSort(arr, pivot + 1, high); //pivot의 오른쪽 다시 퀵 정렬(큰 값들)
      }
   }

   static void sort(int[] arr) {
      quickSort(arr, 0, arr.length - 1);
   }
}
```

---
### 최악의 경우


: 이미 정렬된 경우, 거의 정렬된 경우, pivot 고정되어 있으니 최악일 수 있음
- 중간값을 피벗으로 선택하면 최악의 경우까지 가지 않을 수 있도록 보장

```java
static void quickSort(int[] arr, int low, int high) {
    if (low < high) {
       int mid = low + (high - low) / 2;
       threeSort(arr, low, mid, high);

       if (high - low + 1 > 3) {
          swap(arr, mid, high);
          int pivot = partition(arr, low, high);
       }
    }
}

static void threeSort(int[] arr, int front, int mid, int rear){
   if (arr[front] > arr[mid]) {
      swap(arr, front, mid);
   }
   if (arr[mid] < arr[rear]) {
      swap(arr, mid, rear);
   }
   if (arr[front] > arr[mid]) {
      swap(arr, front, mid);
   }
}
```
**[기존과 다른 부분]**
1. 부분 배열이 3개 이하 값
   - 위의 과정으로 이미 정렬 완료 = partition() 수행 X
2. 부분 배열이 4개 이상 값
   - 중간값에 해당하는 정렬된 mid가 pivot이 되어 partition() 수행

---
### 시간 복잡도
평균: O(NlogN)
최악의 경우: O(N^2)