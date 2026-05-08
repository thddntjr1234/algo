```java
import java.util.*;
import java.lang.*;

class Solution {
    public int[] solution(String[] keyinput, int[] board) {
        int n = 0;
        int m = 0;
        for (String instruction: keyinput) {
            int preN = n;
            int preM = m;
            switch (instruction) {
                case "left":
                    n--;
                    break;
                case "right":
                    n++;
                    break;
                case "up":
                    m++;
                    break;
                case "down":
                    m--;
                    break;
            }

            if (Math.abs(n) > board[0]/2 || Math.abs(m) > board[1]/2) {
                n = preN;
                m = preM;
                continue;
            }
        }

        int[] answer = {n, m};
        return answer;
    }
}
```
### 문제 링크
https://school.programmers.co.kr/learn/courses/30/lessons/120861

### 요구사항
상하좌우 이동 시 board 범위를 벗어나는 명령어는 무시
중앙점 기준 이동

### 후기
preN, M 안쓰고 더 숏코딩으로 풀 수 있을까 생각해봐도 좋을 듯