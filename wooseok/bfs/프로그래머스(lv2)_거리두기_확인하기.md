```java
// 단순 구현방식
class Solution {

    private static final int[] dx = {0, 0, -1, 1};
    private static final int[] dy = {-1, 1, 0, 0};

    public int[] solution(String[][] places) {
        int[] answer = new int[places.length];

        // String타입 배열 대기실을 별도의 2차원 Char배열의 대기실로 변환
        for (int i=0; i<places.length; i++) {
            String[] place = places[i];
            char[][] room = new char[place.length][];

            for (int j=0; j<place.length; j++) {
                room[j] = place[j].toCharArray();
            } 

            // 각 대기실이 거리두기를 준수하는지 검사
            if (isValidRoom(room)) {
                answer[i] = 1;
            } else {
                answer[i] = 0;
            }
        }

        return answer;
    }

    private boolean isValidRoom(char[][] room) {
        // 대기실의 전체 좌표를 순회하면서 P를 만나는 경우 거리두기 여부를 검사
        for (int y = 0; y < room.length; y++) {
            for (int x = 0; x <room[y].length; x++) {
                if (room[y][x] != 'P') continue;
                if (!isValidDistance(room, x, y)) return false;
            }
        }

        return true;
    }

    private boolean isValidDistance(char[][] room, int x, int y) {
        // P의 상하좌우에 다른 P 혹은 테이블이 있는지 검사
        for (int d = 0; d < 4; d++) {
            int nx = x + dx[d];
            int ny = y + dy[d];

            // 탐색할 다음 좌표 (nx, ny)가 유효한 좌표인지 확인
            if (ny < 0 || ny >= room.length || nx < 0 || nx >= room[ny].length) continue;

            // 유효한 좌표에 대해 탐색
            switch (room[ny][nx]) {
                case 'P':
                   return false;
                case 'O':
                    // 이동해온 좌표를 제외하고 나머지 방향에 대해 탐색
                    if (isInvalidDistance(room, nx, ny, new int[]{x, y})) return false;
                    break;
            }
        }

        return true;
    }

    private boolean isInvalidDistance(char[][] room, int x, int y, int[] exclude) {
        for (int d = 0; d < 4; d++) {
            int nx = x + dx[d];
            int ny = y + dy[d];

            // exclude 좌표인 경우 continue
            if (nx == exclude[0] && ny == exclude[1]) continue;
            // 탐색할 다음 좌표 (nx, ny)가 유효한 좌표인지 확인
            if (ny < 0 || ny >= room.length || nx < 0 || nx >= room[ny].length) continue;
            // 탐색할 좌표의 값이 P라면 거리두기가 지켜지지 않은 것이므로 true 반환
            if (room[ny][nx] == 'P') return true;            
        }
        return false;
    }
}
```

```java
// bfs 방식

import java.util.*;

class Solution {
    private static final int[] dx = {0, 0, -1, 1};
    private static final int[] dy = {-1, 1, 0, 0};

    public int[] solution(String[][] places) {
        int[] answer = new int[places.length];

        // 각 대기실별로 bfs 실행
        for (int i=0; i<places.length; i++) {
            if (isValidRoom(places[i])) {
                answer[i] = 1;
            } else {
                answer[i] = 0;
            }
        }

        return answer;
    }

    // 각 원소마다 bfs 실행
    private boolean isValidRoom(String[] room) {
        for (int x=0; x<room.length; x++) {
            for (int y=0; y<room[x].length(); y++) {
                if (room[x].charAt(y) == 'P') {
                    if (!bfs(room, x, y)) {
                        return false;
                    }
                }
            }
        }
        // bfs 통과하면 유효한 거리두기 대기실
        return true;
    }

    private boolean bfs(String[] room, int initX, int initY) {
        // bfs queue
        Queue<int[]> queue = new LinkedList<>();
        boolean[][] visited = new boolean[room.length][room[0].length()];

        // 'P' 좌표(최초 너비는 0)
        queue.offer(new int[]{initX, initY, 0});
        // 시작 위치는 방문 표시
        visited[initX][initY] = true;

        while (!queue.isEmpty()) {
            int[] cur = queue.poll();

            int x = cur[0];
            int y = cur[1];
            int distance = cur[2];
            // 맨해튼 거리 2 초과는 bfs 취소
            if (distance >= 2) {
                continue;
            }

            for (int d=0; d<4; d++) {
                int nx = x + dx[d];
                int ny = y + dy[d];
                int nDistance = distance + 1;
                // 배열 초과 확인
                if (nx < 0 || nx >= room.length || ny < 0 || ny >= room[nx].length()) {
                    continue;
                }

                // 이미 방문한 좌표인지 확인
                if (visited[nx][ny]) {
                    continue;
                }

                // 파티션이면 bfs 스킵
                if (room[nx].charAt(ny) == 'X') {
                    continue;
                }

                // 'P'가 있으면 맨해튼 거리 2 이내에 다른 응시자가 있음
                if (room[nx].charAt(ny) == 'P') {
                    return false;
                }

                visited[nx][ny] = true;
                queue.offer(new int[]{nx, ny, nDistance});
            }
        }

        return true;
    }
}

```
### 문제 링크
https://school.programmers.co.kr/learn/courses/30/lessons/81302
### 문제 유형
2차원 배열, bfs
### 요구사항
모든 응시자를 대상으로 각 응시자 별 맨해튼 거리 2 초과, 2 이내인 경우 모든 이동 경로에 파티션이 있으면 거리두기 준수
아니면 거리두기 실패 처리
### 후기
파티션이 있는 경우 -> 건너편에 뭐가 있든 거리두기 조건을 만족

따라서 파티션이 없는 방향으로 이동 후 이동해온 좌표를 제외한 나머지 방향을 탐색

3방향 중 하나라도 사람이 있으면 파티션으로 가로막히지 않은 응시자와 인접한 것으로 거리두기 미준수에 해당

bfs 사용하면 더 간단하게 풀이 가능 -> bfs로 다시 풀이 연습