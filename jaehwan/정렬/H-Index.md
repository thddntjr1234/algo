# H-Index 
 - 정답률 : 68% (59,879명)
 - 난이도 : Lv.2
 - 유형 : 정렬(구현)
 - [문제 링크](https://school.programmers.co.kr/learn/courses/30/lessons/42747 "프로그래머스 H-Index")
   
### 제출 코드
```java
import java.util.Arrays;

class Solution {
    public int solution(int[] citations) {
        Arrays.sort(citations);

        int hIndex = 0;
        for(int i=citations.length-1; i >= 0; i--){
            if(citations[i] >= hIndex + 1){
                hIndex++;
            } else {
                break;
            }
        }
        
        return hIndex;
    }
}
```
### 풀이 방향
- 논문의 인용 횟수를 담은 배열 ``citations``을 오름차순 정렬
- 가장 많이 인용된 논문부터 역순으로 순회하며 현재까지 확인한 논문 수를 `hIndex'로 관리
- 현재 논문의 인용 횟수가 `hIndex + 1` 이상이면, `hIndex + 1`편의 논문이 해당 횟수 이상 인용된 것이므로 `hIndex`를 증가

### 후기
- 초기 구현시에 {100, 100, 100} 등이 입력되었을 때, H-Index는 100이 안되므로 0을 반환하게 구현 하였다.
- 테스트 케이스를 추가하며 다시 분석해보니, 위의 경우 H-Index는 3이 반환되어야 했다.
- 문제의 요구사항을 제대로 이해하는 능력을 키워야되겠다.
