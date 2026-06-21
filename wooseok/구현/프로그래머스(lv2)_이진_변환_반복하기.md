```java
import java.util.*;

class Solution {
    public int[] solution(String s) {
        int binaryCount = 0;
        int zeroCount = 0;
        
        // 문자열 s가 0제거 -> 이진변환 반복후 "1"이 될때까지 무한 루프
        while (!s.equals("1")) {
            int loopZeroCount = countZero(s);
            binaryCount++;
            zeroCount += loopZeroCount;
            
            int binary = s.length() - loopZeroCount;
            s = Integer.toString(binary, 2);
        }
        
        int[] answer = new int[]{binaryCount, zeroCount};
        return answer;
    }
    
    private int countZero(String s) {
        int result = 0;
        for (char c: s.toCharArray()) {
            if (c == '0') {
                result++;
            }
        }
        
        return result;
    }
}
```

### 문제 링크
https://school.programmers.co.kr/learn/courses/30/lessons/70129?language=java
### 문제 유형
문자열, 구현
### 요구사항&풀이

### 후기
