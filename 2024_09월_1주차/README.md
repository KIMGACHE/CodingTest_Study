## 프로그래머스 - 소수찾기
```
import java.util.*;

class Solution {
    static HashSet<Integer> primeNumbers = new HashSet<>();
    // 소수를 저장할 배열, HashSet은 중복을 허용하지 않는다.
    public int solution(String numbers) {
        boolean[] visit = new boolean[numbers.length()];
        // 문자열의 방문여부를 저장할 boolean배열, 기본값은 false
        for (int i=1; i<=numbers.length();i++){
            repeat(numbers, visit, 0, i,"");
        }
        
        return primeNumbers.size();
    }
    // 소수 판별 함수 isPrime
    public boolean isPrime(int num) {
        if(num<=1) return false;
        for(int i=2; i<num; i++) {
            if(num%i==0) {
                return false;
            }
        }
        return true;
    }
    public void repeat(String numbers, boolean[] visit, int idx, int count, String current) {
        if(idx==count){
            int num = Integer.parseInt(current);
            
            if(isPrime(num)) {
                primeNumbers.add(num);
            }
        }
        // 방문하지 않은 노드에 한해서 다시 함수를 사용한다. 이때 index가 증가하고 현재 문자열에 해당노드를 더한다.
        // idx와 count가 같을 경우에는 해당 문자열의 소수 여부를 판별하고 함수를 종료한다.
        // 함수를 종료하면 방문 표시를 지우고 다음으로 넘어간다.
        for(int i=0; i<numbers.length();i++) {
            if(!visit[i]) {
                visit[i]=true;
                repeat(numbers, visit, idx+1, count, current+numbers.charAt(i));
                visit[i]=false;
            }
        }
        
    }
}
```
