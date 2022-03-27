## Summer/Winter Coding(~2018)

### 소수 만들기

---

### **[Task]**

주어진 숫자 중 3개의 수를 더했을 때 소수가 되는 경우의 개수를 구하려고 합니다. 숫자들이 들어있는 배열 nums가 매개변수로 주어질 때, nums에 있는 숫자들 중 서로 다른 3개를 골라 더했을 때 소수가 되는 경우의 개수를 return 하도록 solution 함수를 완성해주세요.
제한사항

    nums에 들어있는 숫자의 개수는 3개 이상 50개 이하입니다.
    nums의 각 원소는 1 이상 1,000 이하의 자연수이며, 중복된 숫자가 들어있지 않습니다.

입출력 예
nums result
[1,2,3,4] 1
[1,2,7,6,4] 4
입출력 예 설명

입출력 예 #1
[1,2,4]를 이용해서 7을 만들 수 있습니다.

입출력 예 #2
[1,2,4]를 이용해서 7을 만들 수 있습니다.
[1,4,6]을 이용해서 11을 만들 수 있습니다.
[2,4,7]을 이용해서 13을 만들 수 있습니다.
[4,6,7]을 이용해서 17을 만들 수 있습니다.

---

### **[Solution]**

1. 주어진 배열에서 3개의 숫자를 찾는 기능 구현  
   -> 3중 for문을 이용하여 얻을 수 있는 배열의 i + j + k 번째 인덱스의 합을 바탕으로 isPrime 메소드 실행  
   i = 배열의 첫 번째 인덱스  
   j = 비교할 두 번째 인덱스(i+1)  
   k = 비교할 세 번째 인덱스(j+1)
2. 소수 판별 기능 메소드(isPrime)  
   -> 2부터 num-1(i < num)까지 나누어질 경우(num%i == 0) 소수가 아니고, 나누어지지 않을 경우 소수이다.

---

### **[Source]**

```Java
class Solution {
    public int solution(int[] nums) {
        int answer = 0;

        for(int i=0; i < nums.length; i++){
            for(int j=i+1; j < nums.length; j++){
                for(int k=j+1; k < nums.length; k++){
                   if(isPrime(nums[i]+nums[j]+nums[k])){
                       answer++;
                   }
                }
            }
        }

        return answer;
    }

    //소수 판별 메소드
    public boolean isPrime(int num){
        boolean result = true;

        //1은 소수가 아니므로 2부터 시작
        for(int i=2; i < num; i++){
            if(num%i == 0){
                result = false;
                break;
            }
        }

        return result;

    }
}
```
