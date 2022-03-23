## 정렬

### K번째수

---

### **[Task]**

배열 array의 i번째 숫자부터 j번째 숫자까지 자르고 정렬했을 때, k번째에 있는 수를 구하려 합니다.

예를 들어 array가 [1, 5, 2, 6, 3, 7, 4], i = 2, j = 5, k = 3이라면

    array의 2번째부터 5번째까지 자르면 [5, 2, 6, 3]입니다.
    1에서 나온 배열을 정렬하면 [2, 3, 5, 6]입니다.
    2에서 나온 배열의 3번째 숫자는 5입니다.

배열 array, [i, j, k]를 원소로 가진 2차원 배열 commands가 매개변수로 주어질 때, commands의 모든 원소에 대해 앞서 설명한 연산을 적용했을 때 나온 결과를 배열에 담아 return 하도록 solution 함수를 작성해주세요.
제한사항

    array의 길이는 1 이상 100 이하입니다.
    array의 각 원소는 1 이상 100 이하입니다.
    commands의 길이는 1 이상 50 이하입니다.
    commands의 각 원소는 길이가 3입니다.

입출력 예
array commands return
[1, 5, 2, 6, 3, 7, 4] [[2, 5, 3], [4, 4, 1], [1, 7, 3]] [5, 6, 3]
입출력 예 설명

[1, 5, 2, 6, 3, 7, 4]를 2번째부터 5번째까지 자른 후 정렬합니다. [2, 3, 5, 6]의 세 번째 숫자는 5입니다.
[1, 5, 2, 6, 3, 7, 4]를 4번째부터 4번째까지 자른 후 정렬합니다. [6]의 첫 번째 숫자는 6입니다.
[1, 5, 2, 6, 3, 7, 4]를 1번째부터 7번째까지 자릅니다. [1, 2, 3, 4, 5, 6, 7]의 세 번째 숫자는 3입니다.

---

### **[Solution]**

start: 자르는 시작 위치  
end: 자르는 끝 위치  
select: 선택 위치(k번째 수)

**풀이:**  
Arrays.copyOfRange(arr, n1, n2)  
-> 대상 배열의 시작, 끝 위치에 해당하는 요소만을 새로운 배열로 복사한다.  
<br>
예시:  
"[1, 5, 2, 6, 3, 7, 4]를 2번째부터 5번째까지 자른 후 정렬합니다. [2, 3, 5, 6]의 세 번째 숫자는 5입니다." 를 정상 수행하려면?
<br>

1. Arrays.copyOfRange(arr, n1, n2) 개념  
   -> n1(start-1로 하는 이유): 배열은 0부터 시작하기 때문에 -1를 해야한다. 즉 i=0 기준일때 start=2가 되어 이 기준으로 값을 추출하여 정렬하게 되면 결과값이 [2,3,6]이 되어 정상 수행하지 못하게 된다.  
   -> n2: 전달된 인덱스 바로 전의 배열 요소까지만 복사된다.(5가 입력되면 배열의 4번째까지만 복사)  
   <br>
2. answer[i] = splitArray[select-1] 이유도 마찬가지로 결과값이 배열이라 0부터 시작하기 때문이다.  
   <br>

이 문제는 배열과 Arrays.copyOfRange 함수의 개념만 알고 있다면 충분히 쉽게 해결할 수 있다.

---

### **[Source]**

```Java
class Solution {
    public int[] solution(int[] array, int[][] commands) {
        int[] answer = new int[commands.length];

        for(int i = 0; i < commands.length; i++) {
            int start = commands[i][0];
            int end = commands[i][1];
            int select = commands[i][2];

            int[] splitArray = Arrays.copyOfRange(array, start-1, end);

            Arrays.sort(splitArray);

            answer[i] = splitArray[select-1];
        }

        return answer;
    }
}
```
