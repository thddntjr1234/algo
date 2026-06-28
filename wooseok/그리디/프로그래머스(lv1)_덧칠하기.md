```java
class Solution {
    public int solution(int n, int m, int[] section) {
        int answer = 0;
        int paintedEnd = 0; // 현재까지 칠해진 마지막 구역 번호

        for (int target : section) {
            // target 구역이 아직 칠해지지 않았으면 칠하는 것으로 처리
            if (target > paintedEnd) {
                answer++;
                paintedEnd = target + m - 1;
            }
        }

        return answer;
    }
}
```

### 문제 링크
https://school.programmers.co.kr/learn/courses/30/lessons/161989
### 문제 유형
구현, 그리디
### 요구사항&풀이
롤러가 최소 횟수로 움직이도록 계산
### 후기
