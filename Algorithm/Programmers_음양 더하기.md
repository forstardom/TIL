## 월간 코드 챌린지 시즌2

### 음양 더하기

---

### **[Task]**

어떤 정수들이 있습니다. 이 정수들의 절댓값을 차례대로 담은 정수 배열 absolutes와 이 정수들의 부호를 차례대로 담은 불리언 배열 signs가 매개변수로 주어집니다. 실제 정수들의 합을 구하여 return 하도록 solution 함수를 완성해주세요.
제한사항

    absolutes의 길이는 1 이상 1,000 이하입니다.
        absolutes의 모든 수는 각각 1 이상 1,000 이하입니다.
    signs의 길이는 absolutes의 길이와 같습니다.
        signs[i] 가 참이면 absolutes[i] 의 실제 정수가 양수임을, 그렇지 않으면 음수임을 의미합니다.

입출력 예
absolutes signs result
[4,7,12] [true,false,true] 9
[1,2,3] [false,false,true] 0
입출력 예 설명

입출력 예 #1

    signs가 [true,false,true] 이므로, 실제 수들의 값은 각각 4, -7, 12입니다.
    따라서 세 수의 합인 9를 return 해야 합니다.

입출력 예 #2

    signs가 [false,false,true] 이므로, 실제 수들의 값은 각각 -1, -2, 3입니다.
    따라서 세 수의 합인 0을 return 해야 합니다.

---

### **[Solution]**

absolutes: 절댓값이 담긴 배열  
signs: 정수들의 부호가 담긴 배열  
answer: signs가 적용된 absolutes 값들의 합(return)

먼저 정수들의 부호가 담긴 배열인 signs 의 길이만큼 for문을 활용하여 탐색하고, signs 배열의 담긴 값을 기준(true/false)으로 판단한다. 만약 true(양수)이면 절댓갑 배열의 담긴 i번지의 값에 _1을 하여 양수로 만들고, false(음수)이면 _-1로 처리하여 음수로 만든다. 이렇게 나온 값들을 answer 변수에 합산하면 결과값을 구할 수 있다.

---

### **[Source]**

```Java
class Solution {
    public int solution(int[] absolutes, boolean[] signs) {
        int answer = 0;

        for(int i=0; i < signs.length; i++){
            if(signs[i] == true){
                absolutes[i] = absolutes[i] * 1;
                answer += absolutes[i];

            } else {
                absolutes[i] = (absolutes[i] * -1);
                answer += absolutes[i];
            }

        }

        return answer;
    }
}
```
