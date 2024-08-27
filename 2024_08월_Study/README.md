## 프로그래머스 - 숫자 문자열 영단어
```
import java.lang.Integer;

class Solution {
    public int solution(String s) {
        int answer = 0;
        
        String[] number = {"zero","one", "two", "three", "four", "five", "six", "seven", "eight", "nine"};
        // 숫자와 영단어를 치환하기 위한 배열
        
        for (int i=0; i<10; i++) {
            s = s.replace(number[i], Integer.toString(i));
        }
        // replace로 각 영단어를 숫자(String형식)으로 치환
        
        answer = Integer.parseInt(s);
        // String으로 된 숫자를 Int형으로 변환
        
        return answer;
    }
}
```
## 프로그래머스 - 폰켓몬
