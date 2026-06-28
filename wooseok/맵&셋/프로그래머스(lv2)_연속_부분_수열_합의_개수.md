```java
import java.util.*;

class Solution {
    public int solution(int[] elements) {
        // 부분수열 합의 개수를 구하기 위해 중복제거 set 시영
        Set<Integer> sumSet = new HashSet<>();

        int n = elements.length;
        // 1~n 까지 연속 부분 수열 합을 구할 시작점
        for (int start=0; start<n; start++) {
            int sum = 0;
            
            // 1~n까지 연속 부분수열 합을 구함
            // sum은 1, 1~2, 1~3, ..., 1~n까지의 합을 차례대로 저장
            for (int length=0; length<n; length++) {
                int index = (start + length) % n;

                sum += elements[index];
                sumSet.add(sum);
            }
        }

        return sumSet.size();
    }
}
```

### 문제 링크
https://school.programmers.co.kr/learn/courses/30/lessons/131701
### 문제 유형
Set
### 요구사항&풀이
배열을 원형으로 연결한 것으로 가정하고 각 배열 index별로 배열 총 길이만큼의 부분 수열의 합을 계산해서 나올 수 있는 숫자를 카운트
### 후기
