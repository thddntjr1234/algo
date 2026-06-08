# 캐시
 - 정답률 : 66% (25,165명)
 - 난이도 : Lv.2
 - 유형 : 구현 (LRU)
 - [문제 링크](https://school.programmers.co.kr/learn/courses/30/lessons/17680 "프로그래머스 캐시")
   
### 제출 코드
```java
import java.util.LinkedList;

class Solution {
    public int solution(int cacheSize, String[] cities) {
        int answer = 0;
        LinkedList<String> cache = new LinkedList<>();
        
        if(cacheSize == 0) return cities.length * 5;
        
        for(String city : cities){
            city = city.toLowerCase();
            if(cache.contains(city)){ // hit
                cache.remove(city);
                cache.addLast(city);
                answer += 1;
            } else { // miss
                if(cache.size() >= cacheSize){
                    cache.removeFirst();
                }
                cache.addLast(city);
                answer += 5;
            }
        }
        return answer;
    }
}


```
### 풀이 방향
- `LinkedList` 활용해 LRU 캐시 교체 알고리즘 구현
  
### 후기
- `LinkedHashMap`을 사용하는 방식도 있지만, 입력 크기가 작으므로 `LinkedList` 사용해서 직접 구현했음
