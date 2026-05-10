```
import java.util.Arrays;

class Solution {
    public int solution(int k, int m, int[] score) {
        int result = 0;
        Arrays.sort(score);
        
        int count = 0;
        for(int i=score.length; i > 0; i--){
            count++;
            if(count == m){
                count = 0;
                result += score[i-1] * m;
            }
        }
        
        return result;
    }
}
```
### 문제 링크
https://school.programmers.co.kr/learn/courses/30/lessons/135808

### 요구사항
score[] 배열을 오름차순 정렬, 맨뒤부터 탐색하여 과일 박스 하나의 가격 책정.

### 후기
별도의 count 함수와 if문을 사용하지 않고, for() 내의 조건식과 증감식을 잘 활용하면 더 깔끔하게 구현 가능할듯.
