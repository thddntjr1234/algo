```java
import java.util.*;
class Solution {
    boolean solution(String s) {
        boolean answer = false;
        int length = s.length();
        Stack<Integer> stack = new Stack<>();
        
        for(int i=0; i<length; i++) {
            if(s.charAt(i) == '(') {
                stack.push(1);
            }
            else {
                if(stack.isEmpty()) {
                    return false;
                }
                else {
                    stack.pop();
                }
            }
        }
        answer = (stack.isEmpty()) ? true : false;
        return answer;
    }
}
```

### 문제 링크
https://school.programmers.co.kr/learn/courses/30/lessons/12909
### 문제 유형
스택/큐
### 요구사항
올바른 괄호쌍을 검증하기 위해 스택 자료구조 특성을 이용
'(' -> stack.push, ')' -> stack.pop 을 사용하고 올바른 괄호쌍이 아닌 경우 pop시 stack.isEmpty() == true
### 후기
