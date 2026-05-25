# 가장 큰 
 - 정답률 : 66% (63,543명)
 - 난이도 : Lv.2
 - 유형 : 큐
 - [문제 링크](https://school.programmers.co.kr/learn/courses/30/lessons/42587 "프로그래머스 프로세스")
   
### 제출 코드
```java
import java.util.PriorityQueue;
import java.util.Queue;
import java.util.ArrayDeque;

class Solution {
    public int solution(int[] priorities, int location) {
        //우선순위 큐
        PriorityQueue<Integer> pq = new PriorityQueue<>((a,b) -> b - a);
        
        // 대기 큐(Process.priority, Process.index)
        Queue<Process> queue = new ArrayDeque<>();
        
        for(int i=0; i < priorities.length; i++){
            pq.add(priorities[i]); // 우선순위 큐
            queue.offer(new Process(priorities[i], i)); // 대기 큐 (priority, index)
        }
        
        int answer = 0; // 실행 순서
        
        while (!queue.isEmpty()) {
            // 조건1. 실행 대기 큐에서 프로세스 하나 꺼내기
            Process current = queue.poll();

            // 조건2. 대기중인 프로세스중 우선 순위 높은 프로세스가 있는지 판별
            if (current.priority < pq.peek()) {
                queue.offer(current); // 조건2. 방금 꺼냈었던 프로세스를 다시 큐에 넣기
            } else {
                pq.poll(); 
                answer++; 

                if (current.index == location) { // 꺼내었던 프로세스가 원하는 프로세스인지 판별(인덱스 비교)
                    return answer;
                }
            }
        }
        
        return answer;
    }
}

class Process {
    int priority;
    int index;
    
    Process(int priority, int index){
        this.priority = priority;
        this.index = index;
    }
}
```
### 풀이 방향
- 큰 수 우선 ``PriorityQueue`` 우선순위 큐에 프로세스 삽입
- 프로세스 중요도와, 원본 배열에서의 인덱스를 멤버변수로 갖는 Process 객체를 ``Queue``에 삽입
- 중요도와 인덱스를 비교하여 location 프로세스가 몇번째로 실행되는지 판별

### 후기
- 큐에 배열 혹은 클래스 형태로 '값' 과 '인덱스'를 같이 삽입한다는 생각을 바로 떠올리지 못했다.
- 큐를 다양한 방식으로 사용, 활용하는 방법을 공부해야 할것 같다
