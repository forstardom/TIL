## Lesson 4. Counting Elements

### Easy PermCheck

---

### **[Task]**

A non-empty array A consisting of N integers is given.

A permutation is a sequence containing each element from 1 to N once, and only once.

For example, array A such that:

    A[0] = 4
    A[1] = 1
    A[2] = 3
    A[3] = 2

is a permutation, but array A such that:

    A[0] = 4
    A[1] = 1
    A[2] = 3

is not a permutation, because value 2 is missing.

The goal is to check whether array A is a permutation.

Write a function:

class Solution { public int solution(int[] A); }

that, given an array A, returns 1 if array A is a permutation and 0 if it is not.

For example, given array A such that:

    A[0] = 4
    A[1] = 1
    A[2] = 3
    A[3] = 2

the function should return 1.

Given array A such that:

    A[0] = 4
    A[1] = 1
    A[2] = 3

the function should return 0.

Write an efficient algorithm for the following assumptions:

N is an integer within the range [1..100,000];
each element of array A is an integer within the range [1..1,000,000,000].
Copyright 2009–2022 by Codility Limited. All Rights Reserved. Unauthorized copying, publication or disclosure prohibited.

---

### **[Solution]**

**풀이:**  
순열을 구하는 문제

1. 순열을 구하기 위해 입력받은 A배열을 sort
2. A배열의 길이만큼 for문을 돌면서 순열의 형태가 아닌 경우를 탐색한다.

-> (i+1) == A[i] 이어야 하는 이유  
A[0] = 1  
A[1] = 2  
A[2] = 3  
A[3] = 4

위와 입력받은 배열의 값이 순열인 경우라면 A배열의 번지를 나타내는 i값을 기준으로 A[i] = i+1의 규칙을 지닌다. 이 규칙을 만족하는 경우라면 1을 반환하고 그렇지 않으면 0을 반환하면 된다.

---

### **[Source]**

```Java
class Solution {
    public int solution(int[] A) {

        Arrays.sort(A);

        for(int i=0; i < A.length; i++){
            if((i+1) != A[i]){
                return 0;
            }
        }
        return 1;
    }
}
```
