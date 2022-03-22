## 깊이/너비 우선 탐색(DFS/BFS)

### 타겟 넘버

---

### **[Task]**

n개의 음이 아닌 정수들이 있습니다. 이 정수들을 순서를 바꾸지 않고 적절히 더하거나 빼서 타겟 넘버를 만들려고 합니다. 예를 들어 [1, 1, 1, 1, 1]로 숫자 3을 만들려면 다음 다섯 방법을 쓸 수 있습니다.

-1+1+1+1+1 = 3
+1-1+1+1+1 = 3
+1+1-1+1+1 = 3
+1+1+1-1+1 = 3
+1+1+1+1-1 = 3

사용할 수 있는 숫자가 담긴 배열 numbers, 타겟 넘버 target이 매개변수로 주어질 때 숫자를 적절히 더하고 빼서 타겟 넘버를 만드는 방법의 수를 return 하도록 solution 함수를 작성해주세요.
제한사항

    주어지는 숫자의 개수는 2개 이상 20개 이하입니다.
    각 숫자는 1 이상 50 이하인 자연수입니다.
    타겟 넘버는 1 이상 1000 이하인 자연수입니다.

입출력 예
numbers target return
[1, 1, 1, 1, 1] 3 5
[4, 1, 2, 1] 4 2
입출력 예 설명

입출력 예 #1

문제 예시와 같습니다.

입출력 예 #2

+4+1-2+1 = 4
+4-1+2-1 = 4

    총 2가지 방법이 있으므로, 2를 return 합니다.

---

### **[Solution]**

numbers: 알고리즘 실행할 대상 배열  
depth: 노드의 깊이  
target: 타겟 넘버  
sum: 이전 노드 까지의 결과 값

**풀이:**  
깊이 우선 탐색 알고리즘(DFS) 문제
-> 마지막 노드까지 탐색했을 때 타겟 넘버와 결과값이 같으면 정답 카운트 증가

마지막 노드까지 탐색했을 경우 depth와 numbers.length가 같으면 target과 total 값이 같은지 비교하여 일치하면 answer의 카운트를 증가시킨다.
그렇지 않고 탐색할 대상 노드가 남아있다면 이전 노드까지의 합에서 현재 노드 값을 더하고 빼는 두 가지 경우로 DFS 실행한다.

---

### **[Source]**

```Java
class Solution {

    int answer = 0;

    public void dfs(int[] numbers, int depth, int target, int total) {

        if (depth == numbers.length) {
            if(target == total) answer++;
        } else {
            dfs(numbers, depth + 1, target, total + numbers[depth]);
            dfs(numbers, depth + 1, target, total - numbers[depth]);
        }
    }

    public int solution(int[] numbers, int target) {
        dfs(numbers, 0, target, 0);
        return answer;
    }

}
```
