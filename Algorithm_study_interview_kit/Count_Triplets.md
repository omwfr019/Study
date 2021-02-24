Count Triplets
===============

<br/>

## 문제
주어진 long타입 List에서 r과 3개의 Geometric progression을 이룰 수 있는 쌍의 개수를 출력

#### Input Format
* List<long> arr : r의 등비수열Geometric progression을 찾을 배열
* long r : 공비

#### Output Format
* r의 3개 Geometric progression 쌍의 개수

<br/>

### 설계

### 구상 1
1. HashMap에 List의 요소를 저장 (key에 숫자를, value에 개수를 저장)
2. 초기화(1번 과정)를 하며 최대값을 찾음
3. 연속된 3개의 제곱수의 값을 가져옴 (기준값의 이전, 이후 값 검색)
4. 가져온 3개 값을 곱해서(3개 값으로 만들 수 있는 쌍의 개수) 결과에 더함 <br/>
   하나라도 값이 없으면 0을 곱하므로 결과 변화 없음
   

``` java
static long countTriplets(List<Long> arr, long r) {
  long result = 0;
  HashMap<Long, Long> list = new HashMap<>();
  long max = 0;
  
  for(Long key : arr) {
      if(!list.containsKey(key)) {
          list.put(key, 1L);
      } else {
          list.put(key, list.get(key) + 1L);
      }
      if(key > max) {
          max = key;
      }
  }
  
  int n = 1;
  while(Math.pow(r, n+1) <= max) {
      long leftKey = (long)Math.pow(r, n-1);
      long leftValue = list.containsKey(leftKey) == false ? 0 : list.get(leftKey);
      
      long centerKey = (long)Math.pow(r, n);
      long centerValue = list.containsKey(centerKey) == false ? 0 : list.get(centerKey);
      
      long rightKey = (long)Math.pow(r, n+1);
      long rightValue = list.containsKey(rightKey) == false ? 0 : list.get(rightKey);
      
      result += leftValue * centerValue * rightValue;
      n++;
  }
  
  return result;
}
```

시간복잡도 : O(N)

=> 테스트케이스 일부만 통과


