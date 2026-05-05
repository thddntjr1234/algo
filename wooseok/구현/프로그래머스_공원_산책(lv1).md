```java
import java.util.*;
import java.io.*;

class Solution {
    public int[] solution(String[] park, String[] routes) {
        int n = park.length; // y축
        int m = park[0].length(); // x축
        char[][] area = new char[n][m];

        // start -> end 좌표
        int x = -1;
        int y = -1;

        // park int필드 초기화
        for (int i=0; i<n; i++) {
            String str = park[i];
            for (int j=0; j<m; j++) {
                char c = str.charAt(j);
                area[i][j] = c;
                // start 좌표 지정
                if (c == 'S') {
                    x = j;
                    y = i;
                }
            }
        }

        // N, S, W, E 순서
        int[] directionX = {0, 0, -1, 1};
        int[] directionY = {-1, 1, 0, 0};

        // 명령어 실행
        for (int i=0; i<routes.length; i++) {
            String[] instructions = routes[i].split(" ");
            char direction = instructions[0].charAt(0);
            int move = Integer.parseInt(instructions[1]);

            int nx = x;
            int ny = y;
            boolean canMove = true;
            // 명령어 방향 파악
            for (int j=0; j<move; j++) {
                if (direction == 'N') {
                    nx = nx + directionX[0];
                    ny = ny + directionY[0];
                } else if (direction == 'S') {
                    nx = nx + directionX[1];
                    ny = ny + directionY[1];
                } else if (direction == 'W') {
                    nx = nx + directionX[2];
                    ny = ny + directionY[2];
                } else if (direction == 'E') {
                    nx = nx + directionX[3];
                    ny = ny + directionY[3];
                }

                // 매 이동시 이동할 좌표가 이동 가능한 좌표인지 검증
                if (nx < 0 || nx >= m || ny < 0 || ny >= n || area[ny][nx] == 'X') {
                    canMove = false;
                    break;
                }
            }

            // 이동 성공하면 현재 좌표를 변경
            if (canMove) {
                x = nx;
                y = ny;
            }
        }
        int[] answer = {y, x};
        return answer;
    }
}
```

### 요구사항
park는 직사각형(park배열의 각 문자 길이가 모두 동일함)
route는 공백으로 구분된 명령어(방향, 이동거리)
장애물에 충돌하는 경우, park를 벗어나는 경우에는 해당 명령어를 실행하지 않고 스킵함
명령어 모두 수행 후 최종 위치를 반환함

### 후기
반환되는 결과값은 인덱스 접근값()
계산은 좌표평면상의 x, y 계산
directionX, direcitonY => int dx, dy로 두고 매번 dx dy 초기화시켜서 ++, -- 처리해서 방향 고정하는게 더 간단할듯