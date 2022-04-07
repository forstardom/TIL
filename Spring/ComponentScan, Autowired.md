## ComponentScan

1. @ComponentScan은 @Component가 붙은 모든 클래스를 스프링 빈으로 등록한다.
2. 이때 스프링 빈의 기본 이름은 클래스명을 사용하되 맨 앞글자만 소문자로 변환된다.
   - 빈 이름 기본 전략: MemberServiceImpl 클래스 -> memberServiceImpl
   - 빈 이름 직접 지정: 만약 스프링 빈의 이름을 직접 지정하고 싶으면 @Component("memberService2) 이런식으로 설정하면 된다.

## Autowired

1. 생성자에 `@Autowired`를 지정하면, 스프링 컨테이너가 자동으로 해당 스프링 빈을 찾아서 주입한다.
2. 이때 기본 조회 전략은 타입이 같은 빈을 찾아서 주입한다.
   - getBean(MemberRepository.class) 와 동일하다.
