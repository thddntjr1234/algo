```java
import java.util.*;

class Solution {
    boolean solution(String s) {
        s = s.toLowerCase();
        
        int pCount = s.length() - s.replace("p", "").length();
        int yCount = s.length() - s.replace("y", "").length();
        
        if (pCount == yCount) {
            return true;
        } else {
            return false;
        }
    }
}
```

### 문제 링크
https://school.programmers.co.kr/learn/courses/30/lessons/12916
### 문제 유형
문자열, 구현
### 요구사항&풀이

### 후기
