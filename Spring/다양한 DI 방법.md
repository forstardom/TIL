## 다양한 의존관계 주입 방법

**1. 생성자 주입**

- 생성자를 통해서 의존관계를 주입 받는 방법이다.
- 특징
  - 생성자 호출 시점에 1번만 호출되는 것이 보장된다.
  - "불변, 필수" 의존 관계에 사용
  - final 키워드를 사용하여 생성자에서만 값을 넣을 수 있게 된다. 그래서 생성자에서 혹시라도 값이 설정되지 않는 오류를 컴파일 시점에서 막아준다.

불변이란?

- 대부분의 의존관계 주입은 한번 일어나면 어플리케이션 종료시점까지 의존관계를 변경할 일이 없다. 오히려 대부분의 의존관계는 어플리케이션 종료 전까지 변하면 안된다.(불변해야함)
- 수정자 주입을 사용하면, setXxx 메소드를 public으로 열어두어야 하는데, 이렇게 구현할 경우 누군가 실수로 변경할 수도 있어 좋은 설계 방법이 아니다.
- 생성자 주입은 객체를 생성할 때 딱 1번만 호출되므로 이후에 호출될 일이 없다. 따라서 불변하게 설계할 수 있다.

예시

```Java
private final MemberRepository memberRepository;
private final DiscountPolicy discountPolicy;

@Autowired
public OrderServiceImpl(MemberRepository memberRepository, DiscountPolicy discountPolicy) {
    this.memberRepository = memberRepository;
    this.discountPolicy = discountPolicy;
}
```

생성자 주입 권장 이유

- 순환 의존성 확인: 생성자 주입을 하게 되면 서버 기동 시 순환 의존성을 가지는 요소들을 파악할 수 있게 에러 메시지를 표시하면서 서버 기동이 되지 않는다
- 불변성: 생성자 주입은 final을 선언하여 객체가 변하지 않도록 방지해준다.

<br>

**2. 수정자 주입(setter)**

- setter로 필드의 값을 변경하는 수정자 메소드를 통해서 의존관계를 주입하는 방식이다.
- 특징
  - "선택, 변경" 가능성이 있는 의존관계에 사용
  - 자바빈 프로퍼티 규약의 수정자 메소드 방식을 사용하는 방법이다.

※ @Autowired의 기본 동작은 주입할 대상이 없으면 오류가 발생한다. 주입할 대상이 없어도 동작하게 하려면 @Autowired(required = false)로 지정하면 된다.

예시

```Java
private MemberRepository memberRepository;
private DiscountPolicy discountPolicy;

@Autowired
public void setMemberRepository(MemberRepository memberRepository) {
    this.memberRepository = memberRepository;
}

@Autowired
public void setDiscountPolicy(DiscountPolicy discountPolicy) {
    this.discountPolicy = discountPolicy;
}
```

자바빈 프로퍼티 규약 예시

```Java
class Data {
    private int age;
    public void setAge(int age) {
        this.age = age;
    }

    public int getAge() {
        return age;
    }
}
```

<br>

**3. 필드 주입**

- 필드에 바로 주입하는 방식이다.
- 특징
  - 코드가 간결하긴 하지만 외부에서 변경이 불가능하여 테스트하기 힘들다는 단점이 있다.
  - DI 프레임워크가 없으면 아무것도 할 수 없다.
  - 일반적으로 잘 사용하지 않는다.

예시

```Java
@Autowired private MemberRepository memberRepository;
@Autowired private DiscountPolicy discountPolicy;
```

<br>

**4. 일반 메소드 주입**

- 일반 메소드를 통해서 주입 받을 수 있다.
- 특징
  - 한번에 여러번 주입 받을 수 있다.
  - 일반적으로 잘 사용하지 않는다.
