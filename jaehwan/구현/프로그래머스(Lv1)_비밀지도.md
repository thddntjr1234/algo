# 비밀지도
 - 정답률 : 71% (44,265명)
 - 난이도 : Lv.1
 - 유형 : 구현
 - [문제 링크](https://school.programmers.co.kr/learn/courses/30/lessons/17681 "프로그래머스 [1차]_비밀지도")
   
### 제출 코드
```java
class Solution {
    public String[] solution(int n, int[] arr1, int[] arr2) {
        String[] answer = new String[n];
        
        for(int i=0; i < n; i++){
            StringBuilder sb = new StringBuilder();
            String decryptMaps = String.format("%" + n + "s", Integer.toBinaryString(arr1[i] | arr2[i]));
            for(char c : decryptMaps.toCharArray()){
                sb.append(c == '1' ? "#" : " ");
             }
            answer[i] = sb.toString();
        }
        
        return answer;
    }
}
```
### 풀이 방향
- `arr1[i]` , `arr2[i]` -> n개의 비트 수를 가지는 2진수로 변환
- 2진수끼리 OR 연산(|)
- 연산 결과를 한자리씩 순회하며 StringBuilder에 적재.
  
### 후기
- 없음.
