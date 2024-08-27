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

## 프로그래머스 - 네트워크
```
class Solution {
    public int solution(int n, int[][] computers) {
        int answer = 0;
        int arr[] = new int[n]; // 0은 미방문, 1은 방문
        int count = 0;
        
        for(int i=0; i<n; i++) {
            if( arr[i]==0) { // 방문하지 않은 노드일 경우
                count++;
                dfs(i, arr, computers); // dfs로 i와 연결된 모든 애들은 방문 표시함
            }
        }
        
	    answer = count;
        return answer;
    }
    
    public static void dfs(int index, int[] arr, int[][] computers) {
            arr[index] = 1; // 현재 인덱스가 방문했다는걸 표시
            
            for (int i=0; i<arr.length; i++) {
                if(computers[index][i]==1 && arr[i]==0) { // 해당 컴퓨터와 연결되어 있으면서 방문하지 않은 컴퓨터
                    dfs(i,arr,computers); // 와 연결된 컴퓨터를 찾는다
                }
            }
    }
}
```
