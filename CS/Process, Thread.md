# Process와 Thread의 차이점

## **1. Process**

먼저 Program이란 파일이 저장 장치에 저장되어 있지만 메모리에 올라가지 않은 상태이며, Program을 실행하는 순간 해당 파일은 컴퓨터 메모리에 올라가게 되는데 이를 Process라고 한다.  
Process가 메모리에 올라가게 될때 OS로 부터 자원을 할당 받게 되는데 이때 OS는 Process마다 각각 독립된 메모리 영역을 할당 해준다. (Code/Data/Stack/Heap)  
각각 독립된 메모리 영역을 할당해주기 때문에 Process는 다른 Process의 변수나 자료에 접근할 수 없다.

## **2. Thread**

하나의 Program이 여러 작업을 하기 위해서는 서로 독립된 공간을 가지고 있어 서로 접근하지 못하는 특성을 가진 Process를 여러개 만드는 것으로는 해결할 수 없다. 이를 해결하기 위해 Process보다 더 작은 실행 단위로 나온 개념이 Thread이다.  
Thread는 다른 Thread와 메모리(자원)를 공유하며 작동한다. Process가 할당받은 메모리 영역 내에서 Stack 형식으로 할당된 메모리 영역은 따로 할당받고, 나머지 Code/Data/Heap 형식으로 할당된 메모리 영역을 공유하게 된다. 따라서 Thread는 별도의 Stack을 가지고 있지만 Heap 메모리는 서로 읽고 쓸 수 있게 된다.

## **3. 정리**

Process와 Thread는 개념의 범위부터 다르다. (OS > Program > Process > Thread)  
OS가 Process에게 Code/Data/Stack/Heap 메모리 영역을 할당해 주고, 최소 작업 단위로 삼는 반면 Thread는 Process 내에서 Stack 메모리 영역을 제외한 다른 메모리 영역을 같은 프로세스 내 다른 Thread와 공유하게 된다.

Process <-> Process 정보를 공유하려면 IPC(Inter-Process Communication), LPC(Local inter-Process Communication) 등의 번거로운 과정을 거쳐야 하는데, Thread <-> Thread는 기본 구조 자체가 메로리를 공유하는 구조이기 때문에 다른 Thread와 정보 공유가 쉽다.

Process는 실행 도중 오류가 발생해서 강제 종료된다면, 다른 프로세스에 영향을 주지 않는다. 반면 Thread는 Code/Data/Heap 메모리 영역을 공유하기 때문에 하나의 Thread에서 오류가 발생하여 강제 종료된면 다른 Thread가 모두 종료된다.
