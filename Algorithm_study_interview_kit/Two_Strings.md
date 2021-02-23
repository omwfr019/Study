Day 2 : Two Strings
=====================

<br/>

## 문제
2개의 string이 공통 부분 문자열sub string을 공유하는지 확인하여 YES 또는 NO를 출력.

#### Input Format
* 2개의 string이 주어짐

#### Output Format
* 공통 부분 문자열을 공유하면 YES를, 아니면 NO를 출력

<br/>

## 설계

### 구상 1
1. 주어진 string 중 1개 string의 각 알파벳을 HashSet에 저장
   + 방법 1) charAt() 메소드를 이용하여 Set에 추가
   + 방법 2) ""로 split하여 String 배열에 저장 후 Set에 추가
   + 방법 3) toCharArray로 char 배열에 저장 후 Set에 추가
3. 또 다른 1개 string의 각 알파벳(부분 문자열)이 HashSet에 저장한 알파벳(부분 문자열)과 동일한 것이 있는지 확인 <br/>
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
* 시간복잡도 : O(N) <br/>
   N+M => s1 배열 사이즈 + s2 배열 사이즈
   

Map => key-value 형태가 필요하지 않음 <br/>
List => 데이터 검색(포함되었는지 체크)에 시간이 오래 걸림, 중복을 제거하는 과정을 거쳐야 함 <br/>
문제에선 동일한 요소가 '1개'라도 있는지 확인 ~> contains 체크 과정에서 불필요하게 중복 요소를 검사하지 않도록 미리 제거. <br/>
Set의 검색(contains) 시간복잡도는 O(1)이고, 중복이 허용되지 않음. 
따라서 Set이 가장 적합. <br/>

과정 1에서 생각해본 3가지 방법들 중 charAt() 메소드를 이용하는 것, char array로 변환 후 순회하기 중 어떤 방법이 성능에 유리할까? 를 검색한 결과 <br/>
   + String 길이를 천만개로 하면 char array가, 백만개로 하면 charAt이 더 빠름.
   + char 배열을 생성하여 반환하므로 처리속도가 더 느릴 수 있음. <br/>

본 문제에선 1.1번 방법을 선택.


<br/>

#### 코드 정리
* twoStrings : 문제에서 주어진 메소드.
* initStrToSet : string의 각 부분 문자char을 HashSet으로 추가하여 반환.
* chkCommonSubString : str의 각 문자가 set에 포함되어 있으면 YES를 리턴. 포함되는 요소 없이 순회가 종료되면 NO를 리턴.

``` java
static String twoStrings(String s1, String s2) {
   String result = "";
   HashSet<Character> convS1 = new HashSet<Character>();
   
   convS1 = initStrToSet(s1);
   
   result = chkCommonSubString(convS1, s2);
   System.out.println(result);
}

static HashSet<Character> initStrToSet(String str) {
   HashSet<Character> convStr = new HashSet<Character>();
   
   for(int i=0; i<str.length(); i++) {
        char subStr = str.charAt(i);
        convStr.add(subStr);
   }
   
   return convStr;
}

static String chkCommonSubString(HashSet<Character> set, String str) {
   for(int i=0; i<str.length(); i++) {
        if(set.contains(str.charAt(i))) {
            return "YES";
        }
    }
    return "NO";
}
```
