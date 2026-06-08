```java
class Solution {
    public int[][] solution(int[][] arr1, int[][] arr2) {
        int[][] answer = new int[arr1.length][arr2[0].length];
        
        for (int i=0; i<arr1.length; i++) {
            for (int j=0; j<arr1[i].length; j++) {
                for (int k=0; k<arr1[i].length; k++) {
                    answer[i][j] += arr1[i][k] * arr2[k][j];
                }
            }
        }
        return answer;
    }
}
```

### 문제 링크
https://school.programmers.co.kr/learn/courses/30/lessons/12949?language=java
### 문제 유형
배열, 수학
### 요구사항&풀이
행렬의 곱 계산
### 후기
k 순회가 이해가 안 됐음

