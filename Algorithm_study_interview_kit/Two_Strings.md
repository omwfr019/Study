Day 2 : Two Strings
=====================

<br/>

## 문제
2개의 string이 공통 부분 문자열sub string을 공유하는지 확인하여 YES와 NO를 출력.

#### Input Format
* 2개의 string이 주어짐

#### Output Format
* 공통 부분 문자열을 공유하면 YES를, 아니면 NO를 출력

<br/>

## 설계

### 구상 1
1. 주어진 string 중 1개 string의 각 알파벳을 HashSet에 저장
2. 또 다른 1개 string의 각 알파벳(부분 문자열)이 HashSet에 저장한 알파벳(부분 문자열)과 동일한 것이 있는지 확인 <br/>
   동일한 요소가 하나라도 존재하면 YES 출력 후 리턴하고, 동일 요소 없이 비교가 끝나면 NO 출력

``` java
static String twoStrings(String s1, String s2) {
    HashSet<Character> s1Conv = new HashSet<Character>();
    
    for(int i=0; i<s1.length(); i++) {
        s1Conv.add(s1.charAt(i));
    }
    
    for(int j=0; j<s2.length(); j++) {
        if(s1Conv.contains(s2.charAt(j))) {
            return "YES";
        }
    }
    return "NO";
}
```
* 시간복잡도 : O(N+M)

