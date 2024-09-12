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

## 프로그래머스-동영상 재생기
```
import java.util.*;

class Solution {
    public String solution(String video_len, String pos, String op_start, String op_end, String[] commands) {
        // 분:초를 초로 통합한다.
        int total_s = timeToSecond(video_len);
        int pos_s = timeToSecond(pos);
        int op_start_s = timeToSecond(op_start);
        int op_end_s = timeToSecond(op_end);
        String answer ="";
        for(int i=0; i<commands.length; i++) {
            // 오프닝 체크
            if(opening(op_start_s, op_end_s, pos_s)){
                pos_s = op_end_s;                
            }
            if(commands[i].equals("prev")){ // prev명령어일 때
                if(closeStart(pos_s)) pos_s = 0; // 영상이 시작된지 10초미만이면 0으로 만든다.
                else pos_s-=10;
            } else if(commands[i].equals("next")){ // next명령어일 때
                if(closeEnd(total_s,pos_s)) pos_s = total_s;
                // 영상이 끝나기 10초전이라면 영상의 총길이로 현재위치를 변경한다.
                else pos_s+=10;
            }
            // 오프닝 체크
            if(opening(op_start_s, op_end_s, pos_s)){
                pos_s = op_end_s;                
            }
        }
        answer = secondToTime(pos_s); // 초를 분:초로 변경
        return answer;
    }
    
    public int timeToSecond(String str) { // 분:초를 초로 변경
        int minute = Integer.parseInt(str.substring(0,2));
        int second = Integer.parseInt(str.substring(3,5));
        int total = minute*60 + second;
        
        return total;
    }
    
    public String secondToTime(int total){ // 초를 분:초로 변경한다.
        int minute, second;
        String str_m="";
        String str_s="";
        String str ="";
        minute = total/60;
        second = total%60;
        if(minute<10){
            str_m = '0' + Integer.toString(minute); // 두자리수가 아니면 0을 붙여 자리를 맞춰준다.
        } else {
            str_m = Integer.toString(minute);
        }
        if(second<10){
            str_s = '0' + Integer.toString(second); // 두자리수가 아니면 0을 붙여 자리를 맞춰준다.
        } else {
            str_s = Integer.toString(second);
        }
        str = str_m+":"+str_s;
        return str;
    }
    
    public boolean opening(int start_time, int end_time, int pos) { // 오프닝 시간 사이에 있는가 판별
        if(pos>=start_time && pos<=end_time) {
            return true;
        } else {
            return false;
        }
    }
    
    public boolean closeEnd(int total, int pos) {
        if(Math.abs(total-pos)<=10) {
            return true;
        } else {
            return false;
        }
    }
    
    public boolean closeStart(int pos) {
        if(pos <= 10) {
            return true;
        } else {
            return false;
        }
    }
}
```
