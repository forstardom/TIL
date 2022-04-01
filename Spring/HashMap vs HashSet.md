# HashMap vs HashSet

**1. 정의**  
HashMap: Map 인터페이스의 구현체로 HashTable과 유사한 자료구조로 데이터를 저장  
HashSet: Set 인터페이스의 구현체로 내부적으로 HashMap을 사용하기 때문에 역시나 HashTable과 유사한 자료구조로 데이터를 저장

**2. 데이터 저장 형태**  
HashMap: Key-Value 쌍 형태로 데이터를 저장  
HashSet: 객체 그 자체를 저장. Key 값은 삽입되는 객체 값 그 자체이고, Value 값은 HashSet 내부 구현 코드에서 미리 선언해둔 dummy 객체를 사용

**3. 중복 허용 여부**  
HashMap: Key는 중복 허용 X, Value는 중복 가능  
HashSet: 객체 자체를 데이터로 저장하기 때문에 중복 허용 X)

**4. NULL 허용 여부**  
HashMap: 단 하나의 NULL 값을 Key 값으로 가질 수 있고, Value는 NULL값을 여러개 가질 수 있음(중복 Key 값을 허용하지 않기 때문에 NULL도 마찬가지)  
HashSet: 단 하나의 NULL 값을 가질 수 있음

**5. 데이터 삽입 방법**  
HashMap: put() 메소드를 사용하여 Key-Value 쌍 데이터 형태로 저장하기 때문에 삽입 연산 동안 단 하나의 객체가 생성됨  
HashSet: add() 메소드를 사용하여 데이터를 삽입하는데, 객체 그 자체를 저장하고 내부적으로 HashMap을 사용하기 때문에 삽입되는 객체(Key값)와 dummy 객체(Value 값) 총 두 개의 객체가 삽입 연산동안 생성됨

**6. 성능**  
HashMap >> HashSet
