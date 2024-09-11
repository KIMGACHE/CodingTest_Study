## 프로그래머스 - 체육복
```
import java.util.*;

class Solution {
    public int solution(int n, int[] lost, int[] reserve) {
        int answer = 0;
        
        int[] std = new int[n];
        ArrayList<Integer> plus = new ArrayList<>();
        
        for(int i=0; i<lost.length; i++){
            std[lost[i]-1] -= 1; // 체육복을 도난당한 학생은 -1
        } 
        
        for(int i=0; i<reserve.length; i++){
            std[reserve[i]-1] += 1; // 여벌 체육복이 있는 학생은 +1
        }
        
        for(int i=0; i<n; i++) {
            if(std[i]==1) {
                plus.add(i); // 여벌 체육복이 있는 학생들 중 도난당하지 않은 학생들을 plus에 저장
            }
        }
        
        for(int i=0; i<plus.size();i++) {
            if(plus.get(i)-1 >= 0 && std[plus.get(i)-1]==-1) {
                // 여벌 체육복이 있는 학생의 전 순번 도난당한 학생이 있는 경우
                std[plus.get(i)] -= 1;
                std[plus.get(i)-1] += 1;
            } else if(plus.get(i)+1 < n && std[plus.get(i)+1]==-1) {
                // 여벌 체육복이 있는 학생의 후 순번 도난당한 학생이 있는 경우
                std[plus.get(i)] -= 1;
                std[plus.get(i)+1] += 1;
            }
        }
        
        for(int i=0; i<n; i++) {
            if(std[i]>=0) {
                answer += 1; // 체육복이 최소 1개 이상 있는 학생들의 수를 더한다.
            }
        }
        
        return answer;
    }
}
```
