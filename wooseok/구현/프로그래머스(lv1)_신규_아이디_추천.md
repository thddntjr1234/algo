```java
class Solution {
    public String solution(String newId) {
        newId = newId.toLowerCase();
        newId = newId.replaceAll("[^a-z0-9\\-_.]", "");
        newId = newId.replaceAll("\\.+", ".");
        newId = newId.replaceAll("^\\.+|\\.+$", "");
        if (newId.isEmpty()) {
            newId = "a";
        }
        if (newId.length() >= 16) {
            newId = newId.substring(0, 15);
            newId = newId.replaceAll("\\.+$", "");
        }
        while (newId.length() < 3) {
            newId += newId.charAt(newId.length() - 1);
        }
        
        return newId;
    }
}
```

### 문제 링크
https://school.programmers.co.kr/learn/courses/30/lessons/72410
### 문제 유형
문자열, 구현
### 요구사항&풀이

### 후기
