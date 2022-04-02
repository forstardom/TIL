## 좋은 객체 지향 설계의 5가지 원칙(SOLID)

**1. SRP: 단일 책임 원칙(Single Responsibility Principle)**

- 한 클래스는 하나의 책임만 가져야 한다.
- 중요한 판단의 기준은 변경이다. 변경이 있을 때 파급 효과가 적으면 단일 책임 원칙을 잘 따른 것
- ex) UI 변경, 객체의 생성과 사용을 분리

<br>

**2. OCP: 개방-폐쇄 원칙(Open/Closed Principle)**

- 소프트웨어 요소는 확장에는 열려 있으나 변경에는 닫혀 있어야 한다.
- 인터페이스를 구현한 새로운 클래스를 하나 만들어서 새로운 기능을 구현
- ex) 어플리케이션의 전체 동작 방식을 구성하기 위해 구현 객체를 생성하고 연결하는 책임을 가지는 별도의 설정 클래스를 생성(ex: AppConfig)

<br>

**3. LSP: 리스코프 치환 원칙(Liskov Subsitution Priciple)**

- 프로그램의 객체는 프로그램의 정확성을 깨드리지 않으면서 하위 타입의 인스턴스로 바꿀 수 있어야 한다.
- ex) 자동차 인터페이스의 엑셀은 앞으로 가는 기능, 뒤로 가게 구현하면 LSP 위반, 느리더라도 앞으로 가야함

<br>

**4. ISP: 인터페이스 분리 원칙(Interface Segregation Principle)**

- 특정 클라이언트를 위한 인터페이스 여러 개가 범용 인터페이스 하나보다 낫다.
- ex) 자동차 인터페이스 -> 운전, 정비로 분리 / 사용자 클라이언트 -> 운전자, 정비사 클라이언트로분리
- 분리하면 정비 인터페이스 자체가 변해도 운전자 클라이언트에 영향을 주지 않음
- 인터페이스가 명확해지고, 대체 가능성이 높아진다.

<br>

**5. DIP: 의존관계 역전 원칙(Dependency Inversion Principle)**

- 프로그래머는 "추상화에 의존해야지, 구체화에 의존하면 안된다." 의존성 주입은 이 원칙을 따르는 방법 중 하나다.
- 클라이언트 코드가 구현 클래스를 바라보지 말고 인터페이스만 바라봐야함
- MemberService가 MemberRepository 인터페이스만 바라보고 MemberMemoryRepository나 JdbcRepository에 대해서는 몰라야함(역할 의존)

<br>

**※ OCP, DIP 문제 예시(ex: 주문 서비스)**

```Java
public class OrderServiceImpl implements OrderService {
// private final DiscountPolicy discountPolicy = new FixDiscountPolicy();
 private final DiscountPolicy discountPolicy = new RateDiscountPolicy();
}
```

- 추상(인터페이스) 의존: DiscountPolicy
- 구체(구현) 클래스: FixDiscountPolicy, RateDiscountPolicy

**OCP 위반**  
위 코드는 기능을 확장해서 변경하면 클라이언트 코드에 영향을 준다. 따라서 OCP를 위반한다.

**DIP 위반**  
위 코드는 추상(인터페이스) 뿐만 아니라 구체(구현) 클래스에도 의존하고 있다.

<br>

**※ OCP, DIP 위반 문제 해결 방법**

추상에만 의존하도록 관심사를 분리한다. (ex: 공연)

- 배우는 본인의 역할인 배역을 수행하는 것에만 집중해야 한다.
- 남주는 어떤 여주가 선택되더라도 똑같이 공연을 할 수 있어야 한다.
- 공연을 구성하고, 담당 배우를 섭외하고, 역할에 맞는 배우를 지정하는 책임을 담당하는 별도의 공연 기획자가 필요하다.
- 공연 기획자를 만들고, 배우와 공연 기획자의 책임을 확실히 분리한다.

결론: 어플리케이션의 전체 동작 방식을 구성하기 위해 구현 객체를 생성하고 연결하는 책임을 가지는 별도의 설정 클래스를 생성여 해결한다.(ex: AppConfig)
