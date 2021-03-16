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

### 구상 1
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

=> 테스트 케이스 일부만 통과.
