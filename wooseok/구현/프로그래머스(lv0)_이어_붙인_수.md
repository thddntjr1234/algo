```java
import java.util.*;

class Solution {
    public int solution(int[] num_list) {
        int answer = 0;
        String odd = "";
        String even = "";        
        for (int i=0; i<num_list.length; i++) {
            if (num_list[i] % 2 == 1) {
                odd += String.valueOf(num_list[i]);
            }  else if (num_list[i] % 2 == 0) {
                even += String.valueOf(num_list[i]);
            }
        }
        answer = Integer.parseInt(odd) + Integer.parseInt(even);
        return answer;
    }
}
```

### 문제 링크
https://school.programmers.co.kr/learn/courses/30/lessons/181928
### 문제 유형
구현
### 요구사항

### 후기
