# 가장 큰 수
 - 정답률 : 58% (62,164명)
 - 난이도 : Lv.2
 - 유형 : 정렬
 - [문제 링크](https://school.programmers.co.kr/learn/courses/30/lessons/42746 "프로그래머스 가장 큰 수")
   
### 제출 코드
```java
import java.util.Arrays;

class Solution {
    public String solution(int[] numbers) {
        // Comparator 사용을 위한 문자열[]
        String[] strNumbers = new String[numbers.length];
        
        for(int i=0; i<numbers.length; i++){
            strNumbers[i] = String.valueOf(numbers[i]);
        }
        
        // Comparator 정렬
        Arrays.sort(strNumbers, (a, b) -> {
            return (b+a).compareTo(a+b);
        });
        
        if (strNumbers[0].equals("0")) return "0";

        return String.join("", strNumbers);
    }
}
```
### 풀이 방향
- int[]을 String[]로 변환.
- Arrays.sort / compareTo()를 사용해 a+b / b+a 비교.
- 내림차순으로 String[] 정렬.

### 후기
- int 타입 그대로 사용하여 a와 b의 맨 앞자리를 비교 -> 같다면 다음 자리수 비교 하는 방법으로 구현하려고 했었다 ~~삽질~~
- compareTo 메서드가 익숙하지 않아서 고생 좀 했다.
