```java
import java.util.*;
import java.math.*;

class Solution {
    public int[] solution(String[] keymap, String[] targets) {
        // 최소 키 누름 횟수 저장용 map
        Map<Character, Integer> minKeyMap = new HashMap<>();
    
        for (String keys: keymap) {
            // 각 key를 순회하면서 key 만날때마다 map에서 최소값 비교
            for (int i=0; i<keys.length(); i++) {
                char key = keys.charAt(i);
                int pressCount = i+1;
                // math min 비교후 더 작은 값을 추가
                minKeyMap.put(key, Math.min(minKeyMap.getOrDefault(key, Integer.MAX_VALUE), pressCount));
            }
        }
        
        // targets 문자 단위로 순회하면서 문자를 key로 사용해 최소 입력 회수 value를 조회하여 count
        int[] answer = new int[targets.length];
        
        for (int i=0; i<targets.length; i++) {
            int sum = 0;
            for (char c: targets[i].toCharArray()) {
                if (!minKeyMap.containsKey(c)) {
                    sum = -1;
                    break;
                }
                sum += minKeyMap.get(c);
            }
            answer[i] = sum;
        }
        
        return answer;
    }
}
```

### 문제 링크
https://school.programmers.co.kr/learn/courses/30/lessons/160586
### 요구사항
targets의 각 대상 알파벨별로 keymap에서 가장 적은 횟수로 키를 눌러서 도달할 수 있는 횟수를 찾는 것
map에 각 알파벳별로 최소 입력 회수를 저장하고, target 순회하면서 O(1)로 조회해서 추가하는 문제
시간복잡도는 O(N)
### 후기
약간 그리디 성격도 있는 거 같은데 일단은 자료구조+문자열 구현 문제였음
