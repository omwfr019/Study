Hash Tables: Ice Cream Parlor
================================

<br/>

## 문제
In an array, arr, the elements at indies i and j (where i < j) form an inversion if arr[i] > arr[j]. <br/>
In other words, inverted elements arr[i] and arr[j] are considered to be "out of order". <br/>
To correct an invrsion, we can swap adjacent elements. <br/>

(https://www.hackerrank.com/challenges/ctci-merge-sort/problem?h_l=interview&playlist_slugs%5B%5D%5B%5D=interview-preparation-kit&playlist_slugs%5B%5D%5B%5D=sorting)

<br/>

## 설계

### 구상 1
1. 배열의 첫 번째 요소부터 인접한 두 개의 요소를 비교
2. 더 큰 숫자가 전에 있으면 후의 요소와 swap 후 횟수 카운트
3. 다시 처음으로 돌아가 비교를 수행 (1~2 반복)
4. 마지막 요소까지 swap이 없으면 배열이 정렬된 것으로 판단 (3번을 수행하지 않으므로)
5. swap 횟수 반환

#### 구현
```java
static long countInversions(int[] arr) {
    long result = 0;
    int i = 1;

    while(i < arr.length) {
        if(arr[i-1] > arr[i]) {
            int temp = arr[i];
            arr[i] = arr[i-1];
            arr[i-1] = temp;
            
            result++;
            i = 1;
            continue;
        }
        i++;
    }
    
    return result;
}
```

=> 테스트 케이스 일부만 통과. <br/>
입력된 배열 요소의 수가 많으면 시간 초과로 test case 실패. (Timeout) <br/>
속도 개선 필요

<br/>



<br/>

### 구상 2


#### 구현
```java

```
