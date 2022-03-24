## 정렬

### 가장 큰 수

---

### **[Task]**

0 또는 양의 정수가 주어졌을 때, 정수를 이어 붙여 만들 수 있는 가장 큰 수를 알아내 주세요.

예를 들어, 주어진 정수가 [6, 10, 2]라면 [6102, 6210, 1062, 1026, 2610, 2106]를 만들 수 있고, 이중 가장 큰 수는 6210입니다.

0 또는 양의 정수가 담긴 배열 numbers가 매개변수로 주어질 때, 순서를 재배치하여 만들 수 있는 가장 큰 수를 문자열로 바꾸어 return 하도록 solution 함수를 작성해주세요.

제한 사항
numbers의 길이는 1 이상 100,000 이하입니다.
numbers의 원소는 0 이상 1,000 이하입니다.
정답이 너무 클 수 있으니 문자열로 바꾸어 return 합니다.
입출력 예
numbers return
[6, 10, 2] "6210"
[3, 30, 34, 5, 9] "9534330"

---

### **[Solution]**

**풀이:**

1. 정수형을 문자열로 변환  
   -> int형 배열을 String형으로 바꾸어 숫자 자체가 아닌 앞자리의 크기로 비교한다.
2. 문자열을 내림차순 정렬  
   -> Arrays.sort: 입력값이 [3,30,34,5,9] 일 경우 -> 9534330으로 정렬되어야 하기 때문(34, 3, 30 순서)  
   -> compareTo: 기준값.compareTo(비교값)

- 기준값 > 비교값  
  -> 1 반환
- 기준값 < 비교값  
  -> -1 반환
- 기준값 = 비교값  
  -> 0 반환

      ※ 내림차순 정렬을 하지 않고 n2.compareTo(n1)만 수행할 경우(ex: [3,30,34,5,9])
      숫자가 작지만 먼저 오는게 큰 경우가 생길 수 있다. -> 34303 < 34330
      그렇기 때문에 단순 비교가 아니라 (n2+n1).compareTo(n1+n2)로 하고 내림차순 정렬을 해야한다.

3. 0 중복 검사(0만 존재하는 배열 예외처리)
   -> 배열의 값이 "0"으로만 이루어졌을 경우 return 값이 "000"이 아닌 "0"이 되어야 하기 때문이다.

---

### **[Source]**

```Java
class Solution {
    public String solution(int[] numbers) {
        String answer = "";

        String[] str = new String[numbers.length];

        for(int i=0; i < numbers.length; i++){
            str[i] = String.valueOf(numbers[i]);
        }

        // Comparator 파라미터로 넘어온 비교 기준으로 str 배열을 정렬 하겠다는 의미
        Arrays.sort(str, new Comparator<String>() {
            @Override
            public int compare(String a, String b){
                return (b+a).compareTo(a+b);
            }
        });

        if(str[0].equals("0")) return "0";

        for(String s : str) answer += s;

        return answer;
    }
}
```
