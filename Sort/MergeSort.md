## Merge Sort


: Divide and conquer 방식으로 설계된 알고리즘
- 분할 정복: 문제를 반으로 쪼개 해결하는 방식
- 분할: 배열의 크기가 1보다 작거나 같을 때까지 반복
---
### 기본 로직
1. Divide: 배열을 반으로 나누어 더 이상 분할할 수 없을 때까지 분할
2. Conquer: 분할된 각 부분에 대해 재귀적으로 합병 정렬을 통해 배열 정렬
3. Combine: 정렬된 2개의 부분 배열을 병합해 하나의 정렬된 배열로 만들기

---
### Code
```java
public class Main{
    public static void main(String[] args) {
        int[] arr = {60, 10, 30, 1, 4, 3, 31, 22};
        print(arr, -1, -1);
        sort(arr);
    }
    
    static void print(int[] arr, int left, int right){
        for (int i = 0; i < arr.length; i++) {
            if(i == left){
                System.out.print("[");
            }
            System.out.print(arr[i]);
            if(i == right){
                System.out.print("]");
            } else {
                System.out.print(" ");
            }
        }
        System.out.println();
    }
    
    static void merge(int[] arr, int left, int mid, int right){
        int[] leftArr = Arrays.copyOfRange(arr, left, mid+1);
        int[] rightArr = Arrays.copyOfRange(arr, mid+1, right+1);
        
        int i = 0; //왼쪽 배열 검사 idx
        int j = 0; //오른쪽 배열 검사 idx
        int k = left; //합병 중인 배열 현재 idx
        
        while(i < leftArr.length && j < rightArr.length){
            if(leftArr[i] <= rightArr[j]){
                arr[k++] = leftArr[i++];
            } else {
                arr[k++] = rightArr[j++];
            }
        }
        
        while(i < leftArr.length){
            arr[k++] = leftArr[i++];
        }
        
        while (j < rightArr.length){
            arr[k++] = rightArr[j++];
        }
        
        print(arr, left, right);
    }
    
    static void mergeSort(int[] arr, int left, int right){
        //left와 right로 분할 가능하면
        if(left < right){
            int mid = (right + left) / 2;
            //mid 기준으로 2개로 분할
            mergeSort(arr, left, mid);
            mergeSort(arr, mid + 1, right);
            merge(arr, left, mid, right); //분할한 결과 합병(분할 정복)
        }
    }
    
    static void sort(int[] arr){
        mergeSort(arr, 0, arr.length - 1);
    }
}
```

---
### 시간 복잡도
평균/최악의 경우: O(NlogN)