```java
import java.util.*;

class Solution {
    public String[] solution(String[] players, String[] callings) {
        Map<String, Integer> rankMap = new HashMap<>();

        // 선수 이름별 현재 위치 저장
        for (int i=0; i<players.length; i++) {
            rankMap.put(players[i], i);
        }

        for (String calledPlayer : callings) {
            // 해설진이 부른 선수의 현재 위치
            int currentIndex = rankMap.get(calledPlayer);

            int frontIndex = currentIndex - 1;
            String frontPlayer = players[frontIndex];

            // 선수 위치교환
            players[frontIndex] = calledPlayer;
            players[currentIndex] = frontPlayer;

            // map 교환된 위치 갱신
            rankMap.put(calledPlayer, frontIndex);
            rankMap.put(frontPlayer, currentIndex);
        }

        return players;
    }
}
```

### 문제 링크
https://school.programmers.co.kr/learn/courses/30/lessons/178871
### 문제 유형
Map
### 요구사항&풀이
리스트를 쓰지 않고 시간복잡도 개선하기
### 후기
