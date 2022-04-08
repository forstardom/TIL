## JVM

자바 프로그램이 실행되면 자바 소스코드는 컴파일러를 통해 .class 라는 바이트 코드로 변환되고, Class Loader에 의해 JVM 메모리 영역인 Runtime Data Area로 이동 시킨다.

Runtime Data Area 영역은 Method Area, Heap, Stack, PC Register, Native Method Stack이라는 총 5가지 영역으로 나눠져 있고, 이 중 Method Area와 Heap은 모든 스레드가 공유하며 나머지 영역들은 스레드마다 1개씩만 생성되게 된다.

**Method Area**: JVM이 시작될 때 생성되는 공간으로 바이트 코드가 저장된다.  
**Heap**: 동적으로 생성된 객체들이 저장되고 GC의 대상이 되는 공간이며, GC가 정리하기 전까지는 데이터가 남아있다.  
**Stack**: 지역 변수나 메소드의 매개변수, 메소드의 정보 등이 저장되는 영역이며, 매개변수의 특성상 해당 메소드의 호출이 종료되면 이 안에 선언된 변수들은 사라지게 된다.  
**PC Register**: 스레드가 생성될 때 생성되며, 현재 수행중인 JVM의 명령어 주소를 저장하는 공간이다.  
**Native Method Stack**: 자바가 아닌 다른 언어로 저장된 코드를 저장하는 공간 입니다.

이후 Runtime Data Area에 로딩된 클래스 파일이 Execution Engine(Interpreter, JIT, GC)을 통해 바이트 코드가 기계어로 해석되게 된다.

**Interpreter**: 명령어를 한줄씩 해석하며 실행하는 방법  
**JIT Compiler**: 인터프리터의 단점을 해결하기 위해 나온 방법으로 런타임시 한번에 실행하여 변경

이렇게 기계어로 해석된 것들이 Runtime Data Area에 배치되어 스레드 동기화나 가비지 컬렉션을 수행하게 된다. 그리고 마지막으로 Native Method Interface와 Native Method가 있다.

**Native Method Interface**: JVM에 의해 실행되는 코드중 네이티브로 실행되는 것이 있다면 해당 코드를 호출할 수 있도록 만든 일종의 프레임워크  
**Native Method Library**: 네이티브 메소드 실행에 필요한 라이브러리
