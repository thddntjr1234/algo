# 동영상 재생기
 - 정답률 : 42% (15,965명)
 - 난이도 : Lv.1
 - 유형 : 구현 / 시간 변환
 - [문제 링크](https://school.programmers.co.kr/learn/courses/30/lessons/340213 "프로그래머스 동영상 재생기")
### 제출 코드
```java
class Solution {
    public String solution(String video_len, String pos, String op_start, String op_end, String[] commands){
        
        int startOpening = toSec(op_start);
        int endOpening = toSec(op_end);
            
        if(isOpening(startOpening, endOpening, pos)) pos = toPos(endOpening); // 오프닝 스킵
        
        for(String command : commands){
            pos = switch(command){
                case "next" -> next(pos, video_len);
                case "prev" -> prev(pos);
                default -> "00:00";
            };
            if(isOpening(startOpening, endOpening, pos)) pos = toPos(endOpening); // 오프닝 스킵
        }
        
        return pos;
    }
    
    // 오프닝 스킵
    private boolean isOpening(int opStart,int opEnd, String pos){
            int currentTime = toSec(pos);
            
            return opStart <= currentTime && currentTime <= opEnd;
    }
        
    // 10초 뒤로 이동
    private String next(String pos, String video_len){
        final int NEXT_TIME = 10;
        
        int nextSec = toSec(pos) + NEXT_TIME;
        int endSec = toSec(video_len);
        
        return nextSec >= endSec ? video_len : toPos(nextSec);
    }
    
    // 10초 전으로 이동
    private String prev(String pos){
        final int PREV_TIME = 10;
        final int START_SEC = 0;
        
        int prevSec = toSec(pos) - PREV_TIME;
        
        return prevSec <= START_SEC ? "00:00" : toPos(prevSec);
    }
    
    // mm:ss 형식을 초(sec)로 변환
    private int toSec(String pos){
        String[] time = pos.split(":");
        
        int sec = Integer.parseInt(time[0]) * 60 + Integer.parseInt(time[1]);
        
        return sec;
    }
    
    // 초(sec)를 mm:ss 형식으로 변환
    private String toPos(int sec){
        int minute = sec / 60;
        String posMinute = "";
        
        int remainSec = sec % 60;
        String posSec = "";
        
        // mm 형식으로 파싱
        if(minute < 10){
             posMinute = "0" + String.valueOf(minute);
        } else {
            posMinute = String.valueOf(minute);
        }
        
        // ss 형식으로 파싱
        if(remainSec < 10){
            posSec = "0" + String.valueOf(remainSec);
        } else {
            posSec = String.valueOf(remainSec);
        }
        
        return posMinute + ":" + posSec;
    }
}
```
### 풀이 방향
- prev(), next() : pos (mm:ss) 시간을 sec(int)로 변환 후 시간 변환 수행.
- toPos(), toSec() : mm:ss ↔ sec 변환 수행.
- isOpening() : 최초 및 매 반복시 opening 구간인지 판별

### 후기
- 메서드를 최대한 분리하여 가독성이 좋아지도록 노력함.
- 메인(Solution) 메서드에서 항상 초 단위로 관리하고, 헬퍼 메서드는 초 단위로 매개변수로 받는 방식으로 하면 불피요한 시간 변환을 줄이고 가독성도 좋아질것 같다.
- 직접  mm:ss ↔ sec 변환을 수행했는데, String.format() 이란게 있었다..
- ~~아니 나는 오프닝이 보고 싶은데 문제 요구사항이 이게 맞냐고~~
