### 프로그래머스-이상한 문자 만들기
```
import java.lang.*;
class Solution {
    public String solution(String s) {
        String answer = "";
        String noBlank = s.replaceAll("\\s+", " ");
        String[] arrs = noBlank.split(" ");
        int count = 0;
        for(int i=0; i<s.length(); i++) {
            if(s.charAt(i)==32) {
                answer+= " ";
            } else {
                answer += change(arrs[count]);
                i+=arrs[count].length()-1;
                count++;
            }
        }
        
        return answer;
    }
    
    String change(String str) {
        char[] arr = new char[str.length()];
        for(int i = 0; i<str.length(); i++) {
            if(i%2==0)
                arr[i] = Character.toUpperCase(str.charAt(i));
            else
                arr[i] = Character.toLowerCase(str.charAt(i));
        }
        String sol = new String(arr);
        
        return sol;
    }
}
```
