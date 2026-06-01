# 영어 끝말잇기 
 - 정답률 : 70% (35,321명)
 - 난이도 : Lv.2
 - 유형 : 구현
 - [문제 링크](https://school.programmers.co.kr/learn/courses/30/lessons/12981 "프로그래머스 영어 끝맛잇기")
   
### 제출 코드
```java
import java.util.HashSet;
import java.util.Set;

class Solution {
    public int[] solution(int n, String[] words) {
        Set<String> usedWords = new HashSet<>();
        int[] answer = new int[]{0, 0};
        
        usedWords.add(words[0]);
        String lastWord = words[0];
        
        for(int i=1; i < words.length; i++){
            String word = words[i];
            if(isPass(usedWords, word, lastWord)){
                usedWords.add(word);
                lastWord = word;
            } else {
                answer[0] = (usedWords.size() % n) + 1;
                answer[1] = (usedWords.size() / n) + 1;
                return answer;
            }
        }
        
        return answer;
    }
    
    private boolean isPass(Set<String> usedWords, String word, String lastWord){
        if(usedWords.contains(word)) return false;
        
        char lastAlphabet = lastWord.charAt(lastWord.length()-1);
        char startAlphabet = word.charAt(0);
        
        return lastAlphabet == startAlphabet;
    }
}
    }
}
```
### 풀이 방향
- HashSet에 '이미 말한 단어'를 삽입
- HashSet에 단어 포함 여부 및 끝 말 비교
- false일 경우, HashSet.size() 및 n 값으로 탈락 번호와 현재 사이클을 계산

### 후기
- n값 및 words.length가 작으므로, List 활용해도 될듯.
