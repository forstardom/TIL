## Lesson 4. Counting Elements

### Easy FrogRiverOne

---

### **[Task]**

A small frog wants to get to the other side of a river. The frog is initially located on one bank of the river (position 0) and wants to get to the opposite bank (position X+1). Leaves fall from a tree onto the surface of the river.

You are given an array A consisting of N integers representing the falling leaves. A[K] represents the position where one leaf falls at time K, measured in seconds.

The goal is to find the earliest time when the frog can jump to the other side of the river. The frog can cross only when leaves appear at every position across the river from 1 to X (that is, we want to find the earliest moment when all the positions from 1 to X are covered by leaves). You may assume that the speed of the current in the river is negligibly small, i.e. the leaves do not change their positions once they fall in the river.

For example, you are given integer X = 5 and array A such that:

A[0] = 1
A[1] = 3
A[2] = 1
A[3] = 4
A[4] = 2
A[5] = 3
A[6] = 5
A[7] = 4
In second 6, a leaf falls into position 5. This is the earliest time when leaves appear in every position across the river.

Write a function:

class Solution { public int solution(int X, int[] A); }

that, given a non-empty array A consisting of N integers and integer X, returns the earliest time when the frog can jump to the other side of the river.

If the frog is never able to jump to the other side of the river, the function should return −1.

For example, given X = 5 and array A such that:

A[0] = 1
A[1] = 3
A[2] = 1
A[3] = 4
A[4] = 2
A[5] = 3
A[6] = 5
A[7] = 4
the function should return 6, as explained above.

Write an efficient algorithm for the following assumptions:

N and X are integers within the range [1..100,000];
each element of array A is an integer within the range [1..X].
Copyright 2009–2022 by Codility Limited. All Rights Reserved. Unauthorized copying, publication or disclosure prohibited.

---

### **[Solution]**

set: 중복 없이 입력받기 위해 HashSet 사용  
answer: 결과값

**풀이:**  
HashSet을 이용하여 A배열의 길이만큼 탐색한뒤 set에 A[i] 번지의 값을 저장한다.  
만약 set의 길이와 X가 같다면 1부터 X까지의 수가 모두 채워졌다는 뜻이므로 해당 index를 answer에 저장하여 반환한다.  
위 과정을 거쳤는데도 충족하는 index 값이 없다면 -1을 return 한다.

---

### **[Source]**

```Java
class Solution {
    public int solution(int X, int[] A) {

        HashSet<Integer> set = new HashSet<>();

        int answer = -1;

        for(int i=0; i < A.length; i++){
            set.add(A[i]);
            if(set.size() == X){
                answer = i;
                break;
            }
        }

        return answer;

    }
}
```
