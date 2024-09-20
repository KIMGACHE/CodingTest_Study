## 프로그래머스 - 공원
```
import java.util.*;

class Solution {
    public int solution(int[] mats, String[][] park) {
        int answer = -1;
        
        for(int i=0; i<mats.length; i++) { // 돗자리 한 변의 길이
            int max = mats[i]*mats[i]; // 카운트의 최대값을 돗자리 넓이로 설정
            for(int j=0; j<park.length+1-mats[i]; j++) { // 공원 세로길이-돗자리길이+1 만큼 반복
                for(int k=0; k<park[0].length+1-mats[i]; k++){ // 공원 가로길이-돗자리길이+1 만큼 반복
                    int count=0;
                    boolean isPossible = false;
                    while(count<max){
                        int row = count / mats[i]; // 행을 나타내는 변수 설정
                        int col = count % mats[i]; // 열을 나타내는 변수 설정
                        isPossible = false; // 돗자리를 필 수 있는지 여부를 false로 설정
                        if(!park[j+row][k+col].equals("-1")) break;
                        // 해당 위치가 다른 사람의 자리라면 while문을 탈출한다.
                        isPossible = true; // 다른 사람 자리가 없었다면 true로 설정한다.
                        count++;
                    }
                    if(isPossible) answer = Math.max(answer,mats[i]);
                    // 돗자리 필 수 있는지 여부가 true라면 해당 돗자리 크기와 answer중 뭐가 더큰지 비교하교 answer에 할당
                }
            }
        }
        
        return answer;
    }
}
```
