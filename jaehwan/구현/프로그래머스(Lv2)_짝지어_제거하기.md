# 짝지어 제거하기
 - 정답률 : 75% (38,969명)
 - 난이도 : Lv.2
 - 유형 : 구현
 - [문제 링크](https://school.programmers.co.kr/learn/courses/30/lessons/12973 "프로그래머스 짝지어 제거하기")
   
### 제출 코드
```java
import java.util.Stack;

class Solution {
    public int solution(String s){
        
        Stack<Character> stack = new Stack<>();
        
        for(int i=0; i < s.length(); i++){
            char c = s.charAt(i);
            if(stack.empty()){
                stack.push(c);
            } else if(stack.peek() == c){
                stack.pop();
            } else {
                stack.push(c);
            }
        }
        
        return stack.isEmpty() ? 1 : 0;
    }
}
```
### 풀이 방향
- Stack 활용
- Stack의 Top과 현재 알파벳(c)를 비교하여 같을경우 pop(), 다를경우 push(c)
- Stack이 비어있는지 여부로 결과값 반환

### 후기
- 없음.
