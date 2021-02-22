Day 1 : Hash Tables: Ransom Note
==================================

<br/>

## 문제

#### 조건
* 대소문자 구분
* 부분 문자열substring이나 연결concatenation을 사용할 수 없음

#### Input Format
* magazine, note가 string 배열로 주어짐

#### Output Format
* note 배열을 magazine의 배열 요소를 이용해 동일하게 만들 수 있으면 Yes, 아니면 No

<br/>


## 설계

### 구상 1
1. note의 요소(단어)가 magazine에 있는지 체크 (단어가 동일한지 비교)
2. 동일하면 result 변수에 1을 더하고, 중복 count를 방지하기 위해 magazine, note의 해당 단어를 대체
3. result가 note의 단어 개수와 동일하면 Yes 출력

``` java
static void checkMagazine(String[] magazine, String[] note) {
    int result = 0;

    for (int i = 0; i < note.length; i++) {
        for (int j = 0; j < magazine.length; j++) {
            if (note[i].equals(magazine[j])) {
                result++;
                magazine[j] = "!chk!";
                note[i] = "?chk?";
            }
        }
    }

    if (result == note.length) {
        System.out.println("Yes");
    } else {
        System.out.println("No");
    }
}
```

* 시간복잡도 : O(N*M) <br/>
note 배열 사이즈 * magazine 배열 사이즈

<br/>

### 구상 2
1. note, magazine을 HashMap에 저장. 중복 체크를 위해 key에는 각 단어, value에는 단어의 개수를 저장
2. note의 단어를 magazine에서 검색. magazine에 note의 단어가 없으면 No를 출력하고 종료. 있으면 value에서 1을 뺌
3. 모든 단어의 검색이 끝나면(magazine에 존재하면) Yes를 출력

``` java
static void checkMagazine(String[] magazine, String[] note) {
    HashMap<String, Integer> convMagazine = new HashMap<String, Integer>();
        
    for(String mWord : magazine) {
        if (!convMagazine.containsKey(mWord)) {
            convMagazine.put(mWord, 1);
        } else {
            convMagazine.put(mWord, convMagazine.get(mWord)+1);
        }
    }
    
    for(String nWord : note) {
        if(!convMagazine.containsKey(nWord)) {
            System.out.println("No");
            return;
        } else {
            if (convMagazine.get(nWord) < 1) {
                System.out.println("No");
                return;
            } else {
                convMagazine.put(nWord, convMagazine.get(nWord)-1);
            }
        }
    }
    System.out.println("Yes");
}
```

* 시간복잡도 : O(N+M) <br/>
magazine 배열 사이즈 + note 배열 사이즈

단어가 여러 개 존재할 수 있기 때문에 중복 체크 필요. 따라서 중복 저장을 허용하거나 각 단어의 개수 체크가 가능해야 함 => Set은 중복 저장 불가. <br/>
List, HashTable은 검색 속도가 오래 걸림 => Map의 입력/삭제 시간복잡도는 O(1). <br/>
따라서 HashMap이 가장 적합. <br/>
HashMap key에 note의 단어를 저장하고, value에 중복 체크를 위해 단어의 개수를 저장. <br/>
note의 단어key가 magazine의 key에 있는지 검색. key가 검색되면 value의 개수를 빼서 중복 체크.

<br/>

#### 코드 정리
* checkMagazine : 주어진 메소드. magazine의 요소로 note와 동일하게 만들 수 있는지 체크.
* initMagazine : magazine을 HashMap으로 초기화 하는 메소드.
* checkContainsAllWord : note의 모든 단어가 magazine에 포함되는지 판별. 하나라도 포함되지 않으면 No 반환.

``` java
static void checkMagazine(String[] magazine, String[] note) {
    String result = "";
    HashMap<String, Integer> convMagazine = new HashMap<String, Integer>();

    convMagazine = initMagazine(magazine);
    
    result = checkContainsAllWord(convMagazine, note);
    System.out.println(result);
}

static HashMap<String, Integer> initMagazine(String[] magazine) {
    HashMap<String, Integer> convMagazine = new HashMap<String, Integer>();

    for(String element : magazine) {
        if (!convMagazine.containsKey(element)) {
            convMagazine.put(element, 1);
        } else {
            convMagazine.put(element, convMagazine.get(element)+1);
        }
    }

    return convMagazine;
}

static String checkContainsAllWord(HashMap<String, Integer> convMagazine, String[] note) {
    for(String nWord : note) {
        if(!convMagazine.containsKey(nWord)) {
            return "No";
        } else {
            if(convMagazine.get(nWord) < 1) {
                return "No";
            } else {
                convMagazine.put(nWord, convMagazine.get(nWord)-1);
            }
        }
    }
    return "Yes";
}
```
