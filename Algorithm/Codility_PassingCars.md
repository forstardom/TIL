## Lesson 5. Prefix Sums

### Easy PassingCars

---

### **[Task]**

A non-empty array A consisting of N integers is given. The consecutive elements of array A represent consecutive cars on a road.

Array A contains only 0s and/or 1s:

        0 represents a car traveling east,
        1 represents a car traveling west.

The goal is to count passing cars. We say that a pair of cars (P, Q), where 0 ≤ P < Q < N, is passing when P is traveling to the east and Q is traveling to the west.

For example, consider array A such that:
A[0] = 0
A[1] = 1
A[2] = 0
A[3] = 1
A[4] = 1

We have five pairs of passing cars: (0, 1), (0, 3), (0, 4), (2, 3), (2, 4).

Write a function:

    class Solution { public int solution(int[] A); }

that, given a non-empty array A of N integers, returns the number of pairs of passing cars.

The function should return −1 if the number of pairs of passing cars exceeds 1,000,000,000.

For example, given:
A[0] = 0
A[1] = 1
A[2] = 0
A[3] = 1
A[4] = 1

the function should return 5, as explained above.

Write an efficient algorithm for the following assumptions:

        N is an integer within the range [1..100,000];
        each element of array A is an integer that can have one of the following values: 0, 1.

Copyright 2009–2022 by Codility Limited. All Rights Reserved. Unauthorized copying, publication or disclosure prohibited.

---

### **[Solution]**

0 = 오른쪽 이동  
1 = 왼쪽 이동

**주어진 예제:**  
A[0] = 0  
A[1] = 1  
A[2] = 0  
A[3] = 1  
A[4] = 1

**원하는 정답:** 5

**풀이:**  
먼저 1인 경우를 구해야 한다.  
이 문제는 한쌍(0,1)을 만들려면 시작 숫자가 0일 경우 다음 번에 1을 만날 수 있는 경우의 수를 구해야 하는데, 이 과정에서 1의 값을 알아야 0이 최초 시작되는 위치에서부터 1을 만날 수 있는 경우와 그 다음 0이 1을 만날 수 있는 경우를 구할 수 있기 때문이다.

0 다음에 1일 만났을 경우 oneCount--;를 해주면 다음 0이 1을 만날 경우의 값을 구할 수 있다.
그렇게 되면 A[0]일 경우 예제와 같이 1을 만날 경우는 3번이고, A[2]가 1을 만날 경우는 2번이기 때문에 5라는 결과값을 구할 수 있다.

---

### **[Source]**

```Java
class Solution {
    public int solution(int[] A) {

        Integer passingCar = 0;
        int oneCount = 0;

        for(int i=0; i < A.length; i++){
            if(A[i] == 1) {
                oneCount++;
            }
        }

        for(int j=0; j < A.length; j++){
            if(A[j] == 0){
                passingCar += oneCount;
            } else {
                oneCount--;
            }
            //A     passingCars, oneCount
            //A[0]      3           3
            //A[1]      3           2
            //A[2]      5           2
            //A[3]      5           1
            //A[4]      5           0

            if(passingCar > 1000000000){
            passingCar = -1;
            break;
            }
        }




        return passingCar;
    }
}
```
