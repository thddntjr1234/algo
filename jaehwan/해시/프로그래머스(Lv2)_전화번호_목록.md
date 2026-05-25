# 가장 큰 
 - 정답률 : 66% (79,409명)
 - 난이도 : Lv.2
 - 유형 : 해시
 - [문제 링크](https://school.programmers.co.kr/learn/courses/30/lessons/42577 "프로그래머스 전화번호 목록")
   
### 제출 코드
```java
import java.util.HashSet;

class Solution {
    public boolean solution(String[] phone_book) {
        HashSet<String> set = new HashSet<>();

        for (String phone : phone_book) {
            set.add(phone);
        }

        for (String phone : phone_book) {
            for (int i = 1; i < phone.length(); i++) {
                String prefix = phone.substring(0, i); // 자기 자신 제외

                if (set.contains(prefix)) return false;
            }
        }

        return true;
    }
}
```
### 풀이 방향
- ``HashSet``에 모든 전화번호를 삽입
- 자기 자신을 제외한 모든 요소 (0 ~ length - 1)를 substring() 하여, set에 존재하는지 확인

### 후기
- ``String.startsWith()`` 사용하는 방식도 좋을 것 같다.
