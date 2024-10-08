## 프로그래머스 - 완주하지 못한 선수
```
import java.util.*;

class Solution {
    public String solution(String[] participant, String[] completion) {
        String answer = "";
        
        Map<String,Integer> player = new HashMap<String,Integer>();
        // key : 이름, value : 해당 이름을 가진 사람의 수
        for(String el : participant) {
            if(!player.containsKey(el))         // map에 해당 이름을 가진 사람이 없다면 value를 1로 설정한다.
                player.put(el,1);
            else {                              // map에 해당 이름을 가진 사람이 있다면 value에 1을 더한다.
                int count = player.get(el);
                count++;
                player.put(el,count);
            }
        }
        for(String el : completion) {
            if(player.get(el)==1)               // map에 해당 이름을 가진 사람의 value가 1이라면 map에서 삭제한다.
                player.remove(el);
            else {                              // map에 해당 이름을 가진 사람의 value가 1이상이면 value를 1 줄인다.
                player.replace(el, player.get(el)-1);
            }
        }
        Iterator<String> key = player.keySet().iterator();
            while (key.hasNext()){
                answer += key.next();           // map에 남은 이름을 answer에 더한다.
            }
        
        return answer;
    }
}
```
## 프로그래머스 - 더 맵게
```
import java.util.PriorityQueue;
import java.util.*;
class Solution {
    public int solution(int[] scoville, int K) {
        int answer = 0;
        PriorityQueue<Integer> heap = new PriorityQueue<>();    // 우선순위 큐 생성
        for(int food : scoville) {
            heap.add(food);                                     // 우선순위 큐에 각 스코빌지수를 삽입
        }
        while(heap.peek()<K) {                                  // 큐에 가장 작은 값이 K를 넘는 순간 반복을 그만둔다.
            if(heap.size()>=2) {                                // 큐의 사이즈가 2보다 클 경우 음식을 섞는다.
                heap.add(heap.poll()+heap.poll()*2);
                answer++;
            } else {                                            // 큐의 사이즈가 2미만인 경우 스코빌 지수를 K이상으로 만들 수 없으므로 -1을 리턴
                return -1;
            }
        }
        return answer;
    }
}
```

