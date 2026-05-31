```java
import java.util.*;

class Solution {
    public String solution(String[] participant, String[] completion) {
        Map<String, Integer> map = new HashMap<>();

        // 참가자 이름별로 저장
        for (String name : participant) {
            map.put(name, map.getOrDefault(name, 0) + 1);
        }

        // 완주자 이름별로 - 카운트
        for (String name : completion) {
            map.put(name, map.get(name) - 1);
        }

        // value > 0이면 완주 못함
        for (String name : map.keySet()) {
            if (map.get(name) > 0) {
                return name;
            }
        }

        return "";
    }
}
```

### 문제 링크
https://school.programmers.co.kr/learn/courses/30/lessons/42576
### 문제 유형
해시 자료구조 
### 요구사항
선수명을 1차 저장후, completion 목록에서 해당 선수명을 제외해가는 방식
HashSet은 사용 불가능(동명이인인 경우 Set은 중복 제거함) HashMap으로 접근
### 후기
