```java
import java.util.*;

class Solution {
    public int solution(String[] want, int[] number, String[] discount) {
        // 회원가입시 10일동안 매일 한가지 제품만 할인가로 구매 가능
        // 10일 범위로 배열을 끊어서 모든 want의 number를 해당 범위의 배열이 충족하는지 검사해야 됨
        // 완전탐색으로 구현하지만 슬라이딩 윈도우 예제문제도 될 듯
        int answer = 0;
        
        // want-number key-value 저장
        Map<String, Integer> wantMap = new HashMap<>();
        for (int i=0; i<want.length; i++) {
            wantMap.put(want[i], number[i]);
        }
        
        // 10개 범위로 배열을 잘라야 하니 start 길이 조정
        for(int i=0; i<=discount.length-10; i++) {
            // 10 범위로 discount 배열 순회해서 상품별 개수 저장
            Map<String, Integer> itemMap = new HashMap<>();
            for (int j=i; j<i+10; j++) {
                String item = discount[j];
                Integer itemCount = itemMap.getOrDefault(item, 0) + 1;
                itemMap.put(item, itemCount);
                
            }
            
            // itemMap이 wantMap이랑 동일한지 검증
            if (isSameToWant(wantMap, itemMap)) {
                answer++;
            }
        }
        
        
        return answer;
    }
    
    private boolean isSameToWant(Map<String, Integer> want, Map<String, Integer> target) {            
        for (String key: want.keySet()) {
            if (!want.get(key).equals(target.getOrDefault(key, 0))) {
                return false;
            }
        }
        return true;
    }
}
```

### 문제 링크
https://school.programmers.co.kr/learn/courses/30/lessons/131127
### 문제 유형
Map(HashMap), 슬라이딩 윈도우, 완전탐색
### 요구사항
전체 arr을 10개 범위로 자르면서 want-number대로 상품을 구매할 수 있는지 검사
### 후기
완전탐색으로 구현했고
슬라이딩 윈도우로 구현하려면 이전 결과를 저장할 수 있어야 함
슬라이딩 윈도우 연습문제로 풀어봐도 좋을듯
