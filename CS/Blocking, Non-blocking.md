# Blocking, Non-blocking

**블로킹**

- A함수가 B함수를 호출하면, 제어권을 A가 호출한 B함수에 넘겨준다.
- 제어권이 호출된 함수에게 넘어가서 호출된 함수 내에서 작업이 모두 끝난 후 호출한 함수에게 다시 제어권이 넘어온다.

**논블로킹**

- A함수가 B함수를 호출해도 제어권은 그대로 자신이 가지고 있는다.
- 제어권이 계속 호출한 함수에 있기 때문에 작업의 완료여부와 관계없이 새로운 작업을 수행할 수 있다.
