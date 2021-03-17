Sorting: Comparator
=====================

<br/>

## 문제
Comparators are used to compare two objects. In this challenge, you'll create a comparator and use it to sort an array. The Player class is provided in the editor below. It has two fields: <br/>
1. name : a string. <br/>
2. score : an integer. <br/>

Given an array of n Player objects, write a comparator that sorts them in order of decreasing score. <br/>
If 2 or more players have the same score, sort those players alphabetically ascending by name. <br/>
To do this, you must create a Checker class that implements the Comparator interface, then write an int compare(Player a, Player b) method implementing the Comparator.compare(T o1, T o2) method. <br/>
In short, when sorting in ascending order, a comparator function returns -1 if a < b, 0 if a = b, and 1 if a > b. <br/>
Declare a Checker class that implements the comparator method as described. <br/>
It should sort first descending by score, then ascending by name. The code stub reads the input, creates a list of Player objects, uses your method to sort the data, and prints it out properly. <br/>

<br/>

## 설계
1. a, b의 각 name, score를 저장
2. 저장된 score를 비교하여 크거나 같으면 결과 반환
3. (a, b의 score가 같으면) 각 name의 글자 비교 후 결과 반환
  ~> a, b의 name 글자수 중 더 작은 수만큼 반복
  ~> 비교 결과가 나오면 (같은 글자가 아니면) 반복 종료
4. 위 과정에서 결과 반환 없이 메소드가 끝나면 0(동일 표시) 반환

```java
public int compare(Player a, Player b) {
    String nameA = a.name;
    String nameB = b.name;
    Integer scoreA = a.score;
    Integer scoreB = b.score;
    
    if(scoreA < scoreB) return 1;
    else if(scoreA > scoreB) return -1;
    
    int cnt = 0;
    while(cnt < nameA.length() && cnt < nameB.length()) {
        if(nameA.charAt(cnt) > nameB.charAt(cnt)) return 1;
        else if(nameA.charAt(cnt) < nameB.charAt(cnt)) return -1;
        else cnt++;
    }
    
    return 0;
}
```

<br/>
=> 테스트 케이스 일부만 통과. <br/>
test case를 분석해보니 누락된 케이스가 있음. <br/>

* 현재까지 고려된 케이스
  1. score 비동일 <br/>
    ex) 입력값 : a 1, a 10
  2. score 동일, name 글자 비동일, 글자수 동일 <br/>
    ex) 입력값 : aa 5, ab 5
  3. score 동일, name 글자 비동일, 글자수 비동일 (반복문 내에서 비교 결과 반환) <br/>
    ex) 입력값 : abb 5, aab 5

* 누락 케이스
  1. score 동일, name 글자 비동일, 글자수 비동일 (반복문 내에서 비교 결과 반환되지 않음) <br/>
    ex) 입력값 : aab 5, aabc 5
  2. score 동일, name 글자 동일, 글자수 비동일 <br/>
    ex) 입력값 : a 5, aa 5

<br/>
글자수 비교하는 로직을 추가하여 글자수가 더 작은 Person을 큰 값으로 판단하여 반환 => 누락 케이스 1, 2 해결됨

<br/>
* 현재 로직 : 반복문 내에서 글자 비교 -> 두 비교대상이 동일한 것으로 판단 (0 반환) 
* 수정 로직 : 반복문 내에서 글자 비교 -> 글자수 비교 -> 두 비교대상이 동일한 것으로 판단 (0 반환) 

<br/>

```java
class Checker implements Comparator<Player> {
  	// complete this method
	public int compare(Player a, Player b) {
        String nameA = a.name;
        String nameB = b.name;
        Integer scoreA = a.score;
        Integer scoreB = b.score;
        
        if(scoreA < scoreB) return 1;
        else if(scoreA > scoreB) return -1;
        
        int cnt = 0;
        while(cnt < nameA.length() && cnt < nameB.length()) {
            if(nameA.charAt(cnt) > nameB.charAt(cnt)) return 1;
            else if(nameA.charAt(cnt) < nameB.charAt(cnt)) return -1;
            else cnt++;
        }
        
        if(nameA.length() > nameB.length()) return 1;
        else if(nameA.length() < nameB.length()) return -1;
        return 0;
    }
}
```
