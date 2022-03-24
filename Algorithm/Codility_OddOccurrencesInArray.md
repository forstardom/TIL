## Lesson 2. Arrays

### Easy OddOccurrencesInArray

---

### **[Task]**

A non-empty array A consisting of N integers is given. The array contains an odd number of elements, and each element of the array can be paired with another element that has the same value, except for one element that is left unpaired.

For example, in array A such that:

A[0] = 9 A[1] = 3 A[2] = 9
A[3] = 3 A[4] = 9 A[5] = 7
A[6] = 9
the elements at indexes 0 and 2 have value 9,
the elements at indexes 1 and 3 have value 3,
the elements at indexes 4 and 6 have value 9,
the element at index 5 has value 7 and is unpaired.
Write a function:

class Solution { public int solution(int[] A); }

that, given an array A consisting of N integers fulfilling the above conditions, returns the value of the unpaired element.

For example, given array A such that:

A[0] = 9 A[1] = 3 A[2] = 9
A[3] = 3 A[4] = 9 A[5] = 7
A[6] = 9
the function should return 7, as explained in the example above.

Write an efficient algorithm for the following assumptions:

N is an odd integer within the range [1..1,000,000];
each element of array A is an integer within the range [1..1,000,000,000];
all but one of the values in A occur an even number of times.
Copyright 2009–2022 by Codility Limited. All Rights Reserved. Unauthorized copying, publication or disclosure prohibited.

---

### **[Solution]**

**풀이:**  
홀수 개의 숫자를 갖는 배열 A를 입력받아 짝이 없는 정수를 반환하도록 구현하는 문제  
Map을 이용하여 A배열의 길이만큼 Loop 하면서 중복값 여부 체크하면 된다.

- Key = 배열 값 / Value = 배열 안에 중복값 체크(존재시 +1)

이 과정을 거친 후 entrySet()을 활용하여 해당 map에 저장된 값들 중 Value가 2로 나누었을 때 나머지가 1인 경우를 찾는다. 즉 map.getValue의 값이 1이면 짝이 없는 경우라고 판단할 수 있다. (홀수 개의 숫자를 갖는 배열이기 때문에 중복값이 홀수가 나올 수가 없음)

---

### **[Source]**

```Java
class Solution {
    public int solution(int[] A) {

        Map<Integer, Integer> map = new HashMap<>();

        for(int i=0; i < A.length; i++){
            if(map.get(A[i]) == null) {
                map.put(A[i], 1);
            } else {
                map.put(A[i], map.get(A[i])+1);
            }
        }

        for(Map.Entry<Integer, Integer> entry : map.entrySet()){
            if(entry.getValue() % 2 == 1){
                return entry.getKey();
            }
        }

        return 0;
    }
}
```
