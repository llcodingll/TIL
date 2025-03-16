## Counting Sort


: 데이터의 수를 세어 counting array에 저장하고 하나씩 꺼내어 정렬하는 알고리즘
- 특정 조건이 부합할 때만 사용할 수 있음
  - 데이터가 양의 정수
  - 데이터 크기 범위가 제한된 경우
  - 가장 큰 데이터와 가장 작은 데이터 차이가 1,000,000을 넘지 않는 경우
- 중복된 값이 많은 경우의 배열 정렬 시, 효과적

---
### 기본 로직
1. 가장 작은 데이터와 가장 큰 데이터가 모두 담길 수 있는 리스트 생성
2. 배열 순회하며 각 데이터 값과 동일한 idx의 데이터 1씩 증가 (counting array 생성)
3. 카운팅 리스트에서 0인 값 제외, 해당 idx의 데이터만큼 반복 출력

---
### Code

```java
public static List<Integer> countingSort(int[] arr){
    int max = Arrays.stream(arr).max().getAsInt();
    int[] cntArr = new int[max+1]; // 수가 1부터 시작하면 idx는 0부터 시작하기 때문에 max+1
    
    //배열 순회하며 각 데이터 값과 동일한 idx 데이터 1씩 증가
    for (int i = 0; i < arr.length; i++) {
        cntArr[arr[i]]++;
    }
    
    List<Integer> result = new ArrayList<>();
    
    //완성된 카운팅 리스트에서 0인 값 제외하고, 해당 인덱스 데이터만큼 반복 출력
    for (int i = 0; i < cntArr.length; i++) {
        if(cntArr[i] == 0){
            continue;
        }
        for (int i = 0; i < cntArr[i]; i++) {
            result.add(i);
        }
    }
    return result;
}
```

---
### 시간 복잡도
O(N+K)
K: counting array 내부 최대 숫자