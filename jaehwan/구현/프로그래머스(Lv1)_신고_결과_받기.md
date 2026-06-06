# 신고 결과 받기
 - 정답률 : 42% (40,873명)
 - 난이도 : Lv.1
 - 유형 : 구현
 - [문제 링크](https://school.programmers.co.kr/learn/courses/30/lessons/92334 "프로그래머스 신고 결과 받기")

### 제출 코드 
<details>
<summary>리팩토링 코드</summary>
  
```java
import java.util.Set;
import java.util.HashSet;
import java.util.Map;
import java.util.HashMap;
class Solution {
    Map<String, Integer> memberIndex = new HashMap<>();
    Set<String> suspensionTargets = new HashSet<>();
    
    public int[] solution(String[] id_list, String[] report, int k) {
        int[] answer = new int[id_list.length];
        Member[] members = new Member[id_list.length]; 
        
        initMembers(id_list, members); 
        saveReports(report, members);  
        countReports(members, k);
        
        for(String target : suspensionTargets){
            for(Member member : members){
                if(member.isReported(target)){ 
                    answer[member.getIndex()]++; 
                }
            }
        }
        return answer;
    }
    
    private void initMembers(String[] id_list, Member[] members){
        for(int i=0; i < id_list.length; i++){
            String id = id_list[i];
            members[i] = new Member(id, i);
            memberIndex.put(id, i);
        }
    }
    
    private void saveReports(String[] report, Member[] members){
        for(int i=0; i < report.length; i++){
            String[] token = report[i].split(" ");
            String reporterId = token[0];
            String reportedId = token[1];
            
            int index = memberIndex.get(reporterId);
            members[index].report(reportedId);
        }
    }
    
    private void countReports(Member[] members, int k){
        for(Member member : members){
            for(String memberId : member.getReportedMember()){
                int index = memberIndex.get(memberId);
                Member reportedMember = members[index];
                if(reportedMember.reported(k)){
                    suspensionTargets.add(reportedMember.getId());
                }
            }
        }
    }
}
class Member{
    String id;
    int index; // members 배열에서의 위치, answer 배열 인덱스와 대응
    Set<String> reportedMembers; // 중복 신고 방지를 위해 Set 사용
    int reportedCount;
    
    Member(String id, int index){
        this.id = id;
        this.index = index;
        this.reportedMembers = new HashSet<>();
        this.reportedCount = 0;
    }
    
    public boolean isReported(String id){
        return reportedMembers.contains(id);
    }
    
    public void report(String id){
        reportedMembers.add(id);
    }
    
    // k번 이상 신고되면 true 반환
    public boolean reported(int k){
        reportedCount += 1;
        return reportedCount >= k;
    }
    
    public String getId(){
        return id;
    }
    
    public int getIndex(){
        return index;
    }
    
    public Set<String> getReportedMember(){
        return reportedMembers;
    }
    
    public int getReportedCount(){
        return reportedCount;
    }
}
```
</details>

<details>
<summary>리팩토링 전</summary>
  
```java
import java.util.Set;
import java.util.HashSet;
import java.util.Map;
import java.util.HashMap;

class Solution {
    public int[] solution(String[] id_list, String[] report, int k) {
        int[] answer = new int[id_list.length];
        Member[] members = new Member[id_list.length];
        Map<String, Integer> memberMaps = new HashMap<>();
        Set<String> suspensionTargets = new HashSet<>(); // 정지 대상
        
        for(int i=0; i < id_list.length; i++){
            String id = id_list[i];
            Member member = new Member(id, i);
            members[i] = member;
            
            memberMaps.put(id, i); // 멤버 id를 인덱스 번호와 매핑
        }
        
        // 신고한 유저 저장
        for(int i=0; i < report.length; i++){
            String[] token = report[i].split(" ");
            String reporterId = token[0];
            String reportedId = token[1];
            
            int index = memberMaps.get(reporterId);
            members[index].report(reportedId);
        }
        
        // 신고당한 횟수 누적
        for(Member member : members){
            for(String memberId : member.getReportedMember()){
                int index = memberMaps.get(memberId);
                members[index].reported();
                
                // 신고 횟수가 특정횟수 이상이면 정지대상 (Member 클래스에서 boolean 값으로 반환후 분기 처리 가능할듯)
                if(members[index].getReportedCount() >= k){
                    suspensionTargets.add(members[index].getId());
                }
            }
        }
        
        for(String taget : suspensionTargets){
            int index = 0;
            for(Member member : members){
                if(member.isReported(taget)){
                    answer[index]++;
                }
                index++;
            }
        }
        
        return answer;
    }
}

class Member{
    String id;
    int index;
    Set<String> reportedMembers;
    int reportedCount;
    
    Member(String id, int index){
        this.id = id;
        this.index = index;
        this.reportedMembers = new HashSet<>();
        this.reportedCount = 0;
    }
    
    public boolean isReported(String id){
        return reportedMembers.contains(id);
    }
    
    public String[] getReportedMember(){
        String[] result = new String[reportedMembers.size()];
        
        int index = 0;
        for(String member : reportedMembers){
            result[index++] = member;
        }
        
        return result;
    }
    
    public void report(String id){
        reportedMembers.add(id);
    }
    
    public void reported(){
        reportedCount += 1;
    }
    
    public int getReportedCount(){
        return reportedCount;
    }
    
    public String getId(){
        return id;
    }
    
    public int getIndex(){
        return index;
    }
}
```
</details>

### 풀이 방향
- `Class Member` → 멤버 한 명의 상태(신고 목록, 신고당한 횟수)를 관리, 중복 신고 방지를 위해 신고 목록을 Set으로 관리
- `Map<String, Integer> memberIndex` -> id를 통해 특정 member 객체의 접근 가능 (시간복잡도 : O(1))

### 후기
- 어떤 자료구조를 사용하는게 효율적일까 고민을 열심히 했음.
- 클래스를 활용했더니 코드가 매우 길어졌다.
- 좀더 효율적인 방법이 있는지는 더 고민해봐야 할 것 같음
