```java
import java.util.*;
import java.io.*;

class Solution {
    public int solution(String s) {
        String[] word = {"zero", "one", "two", "three", "four", "five", "six", "seven", "eight", "nine"};
        
        for (int i=0; i<word.length; i++) {
            s = s.replace(word[i], String.valueOf(i));
        }
        
        return Integer.parseInt(s);
    }
}
```

### 문제 링크
https://school.programmers.co.kr/learn/courses/30/lessons/81301

### 요구사항
영단어를 매칭 목록에 맞게 숫자로 단순 변환

### 후기
영단어가 중복되게 나올 수 있으니 replace로 일괄 처리
replace() 안 쓰고 빡구현으로도 풀어볼 예정