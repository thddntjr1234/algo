# 가장 큰 
 - 정답률 : 68% (80,182명)
 - 난이도 : Lv.2
 - 유형 : Queue
 - [문제 링크](https://school.programmers.co.kr/learn/courses/30/lessons/42586 "프로그래머스 기능개발")
   
### 제출 코드
```java
import java.util.Queue;
import java.util.ArrayDeque;
import java.util.List;
import java.util.ArrayList;

class Solution {
    public int[] solution(int[] progresses, int[] speeds) {
        Queue<Integer> queue = new ArrayDeque<>(); // 기능 완성일을 담는 큐
        List<Integer> list = new ArrayList<>(); // 결과 반환용 List
        
        // 기능 완성일 계산
        for(int i=0; i<progresses.length; i++){
            int remainRate = 100 - progresses[i];
            int completeDays = (remainRate + speeds[i] - 1) / speeds[i];
            queue.offer(completeDays);
        }
        
        int releaseDate = queue.poll(); // 최우선 기능 배포 일
        int count = 1; // 배포된 기능의 개수
        
        // 배포되는 기능의 개수 계산
        while(!queue.isEmpty()){
            if(releaseDate >= queue.peek()){
                count++;
                queue.poll();
            } else {
                list.add(count);
                count = 1;
                releaseDate = queue.poll();
            }
        }
        list.add(count);
        
        
        return toIntArray(list);
    }
    
    // Convert List to Array
    private int[] toIntArray(List<Integer> list){
        int[] answer = new int[list.size()];
                               
        for(int i=0; i<list.size(); i++){
            answer[i] = list.get(i).intValue();
        }
                               
        return answer;
    }
}
```
### 풀이 방향
- 기능별 작업 완료일을 계산 및 큐에 담기.
- 최우선 기능과 함께 배포 가능한 기능 개수 판별(최우선 기능 배포 일 >= 다음 우선 기능 배포일)
- 반환 타입은 int[]이나, 크기를 모르기에 List 활용

### 후기
- 배포가 끝날때(if-else 경우)만, releaseDate = queue.poll()를 수행해야 하는데, 매 반복마다 수행하여 일부 케이스만 성공했었음. ~~생각 좀 더 하자~~
- 엣지 케이스를 스스로 찾는 연습을 많이 해야겠다.
