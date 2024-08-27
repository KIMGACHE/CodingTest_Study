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
```
import java.util.Arrays;

class Solution {
    public int solution(int[] nums) {
        int answer = 0;
        int count = 0;
        int limit = nums.length/2;
        
        Arrays.sort(nums);
        // 배열을 정렬
        for (int i=0; i<nums.length ; i++) {
            if(i==0) {count++;}
            else if (nums[i] != nums[i-1]) {count++;}
        }
        // 오름차순으로 정렬한 배열에서 포켓몬의 종류를 count에 저장
        if(limit < count) {answer=limit;}
        else {answer= count;}
        
        return answer;
    }
}
```

## 
