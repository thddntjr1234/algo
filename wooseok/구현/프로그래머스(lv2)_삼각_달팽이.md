```java
import java.util.*;

class Solution {
    public int[] solution(int n) {
        // dx, dy 방향 전환 선언
        final int[] dx = {1, 0, -1};
        final int[] dy = {0, 1, -1};
        
        // n*n 2차원 배열
        int[][] arr = new int[n][n];
        
        int direction = 0;
        int x = 0;
        int y = 0;
        int num = 1;
        while (true) {
            arr[x][y] = num;
            num++;
            
            int nx = x + dx[direction];
            int ny = y + dy[direction];
            
            // 더이상 배열을 채울 수 없을 때 방향 전환
            if (nx >= n || nx < 0 || ny >= n || ny < 0 || arr[nx][ny] != 0) {
                direction = (direction + 1) % 3;
                
                nx = x + dx[direction];
                ny = y + dy[direction];
                // 방향 전환 후에도 더이상 배열을 채울 수 없으면 루프 종료
                if (nx >= n || nx < 0 || ny >= n || ny < 0 || arr[nx][ny] != 0) {
                    break;
                }
            }
            
            // 계속 이동 가능하면 좌표 반영
            x = nx;
            y = ny;
        }

        int[] answer = new int[num-1];
        int index = 0;

        for (int i=0; i<n; i++) {
            for (int j=0; j<=i; j++) {
                answer[index++] = arr[i][j];
            }
        }
        
        return answer;
    }
}
```

### 문제 링크
https://school.programmers.co.kr/learn/courses/30/lessons/68645
### 요구사항
2차원 배열 기준 가상의 삼각형을 만족하도록 반시계 방향으로 배열을 채워야 함
순서는 아래->오른쪽->왼쪽위 순서로 감
### 문제 유형
자료구조(2차원 배열) + 구현
### 후기
