```java
import java.util.*;

class Solution {
    public int solution(int[] order) {
        // 보조 컨베이어 벨트는 FIFO이므로 스택 사용
        Stack<Integer> stack = new Stack<>();
        int idx = 0;
        
        for (int box=1; box<=order.length; box++) {
            // 현재 박스가 상차해야 되면 상차로 간주하고 다음 박스 진행
            if (box == order[idx]) {
                idx++;
                
                while (!stack.isEmpty() && stack.peek() == order[idx]) {
                    stack.pop();
                    idx++;
                
                     // 모든 보조 컨베이어 벨트를 상차하게 되는 케이스 처리
                    if (idx == order.length) {
                        return idx;
                    }
                }
            } else {
                stack.push(box);
            }
        }
        return idx;
    }
}
```

### 문제 링크
https://school.programmers.co.kr/learn/courses/30/lessons/131704
### 문제 유형
스택 자료구조
### 요구사항&풀이
보조 컨베이어 벨트 -> FIFO 자료구조이므로 스택 사용
메인 벨트(box)가 order[i]에 해당하는 경우 상차하고, 여기서부터 스택에서 차례대로 꺼낸다
스택에서 모두 꺼내서 더이상 상차 가능한 박스가 없으면 다시 보조 컨베이어 벨트로 박스를 추가
### 후기
