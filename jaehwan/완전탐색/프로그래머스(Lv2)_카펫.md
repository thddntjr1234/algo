# 카펫 
 - 정답률 : 74% (62,363명)
 - 난이도 : Lv.2
 - 유형 : 완전탐색
 - [문제 링크](https://school.programmers.co.kr/learn/courses/30/lessons/42842 "프로그래머스 카펫")
   
### 제출 코드
```java
class Solution {
    public int[] solution(int brown, int yellow) {
        int size = brown + yellow;
        
        for(int i=1; i <= size / i; i++){ // 제곱근까지 탐색
            if(size % i == 0){ // 약수 판별 (카페 가로 길이 >= 세로)
                int height = i;
                int width = size

                // 노란색 격자의 개수 검증
                if ((width - 2) * (height - 2) == yellow) return new int[] {width, height};
            }
        }
        
        return new int[] {};
    }
}
```
### 풀이 방향
- 카펫 크기의 제곱근까지만 반복하여 약수 탐색
- 테두리 1줄만 갈색이므로 (가로 길이 -2) * (세로 길이 -2 ) == 노란색 개수

### 후기
- 완전 탐색 유형 문제이지만, 제곱근까지 구하면 됨.
- 테두리 1줄만 갈색이란걸 이용해 검증하면 되는데, 문제를 제대로 안 읽어서 어떻게 검증할지 고민하느라 시간 좀 썻음
