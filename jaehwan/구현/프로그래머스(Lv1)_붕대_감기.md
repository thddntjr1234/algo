```
class Solution {
    private static final int CASTING = 0;
    private static final int HEAL_PER_SEC = 1;
    private static final int BONUS_HEAL = 2;
    
    private static final int ATTACK_TIME = 0;
    private static final int DAMAGE = 1;
    
    public int solution(int[] bandage, int health, int[][] attacks) {
        final int MAX_HEALTH = health; // 최대 체력
        
        int attackIdx = 0;
        int successCnt = 0; // 연속 성공 횟수
        int lastAttackTime = attacks[attacks.length-1][ATTACK_TIME];
        
        for(int sec = 1; sec <= lastAttackTime; sec++){
            if(sec == attacks[attackIdx][ATTACK_TIME]){
                health -= attacks[attackIdx][DAMAGE];
                attackIdx++;
                successCnt = 0;
                if(health <= 0) return -1;
            } else {
                health = heal(health, bandage[HEAL_PER_SEC], MAX_HEALTH);
                successCnt++;
                if(successCnt == bandage[CASTING]){
                    health = heal(health, bandage[BONUS_HEAL], MAX_HEALTH);
                    successCnt = 0;
                }
            }
        }
        
        return health;
    }
    
    private int heal(int currentHealth, int healValue, int maxHp){
        int healedHp = currentHealth + healValue;
        return healedHp < maxHp ? healedHp : maxHp;
    }
}
```
### 문제 링크
https://school.programmers.co.kr/learn/courses/30/lessons/250137

### 요구사항
1 -> 마지막 공격 시간까지 반복하며 공격 감지 및 체력회복

### 후기
매 초마다 반복하지 않고 마지막 공격 시간 - 현재 공격 시간으로 시간 차이 계산하면 attacks.length 만큼만 반복하게 만들면 좋을 듯
