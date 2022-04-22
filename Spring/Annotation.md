# 어노테이션(Annotation)

## **어노테이션(Annotation) 이란?**

코드 사이에 주석처럼 쓰이며 특정 의미, 기능을 수행하도록 하는 기술이다.

## **용도**

1. 컴파일러에게 코드 작성 문법 에러를 체크하도록 정보 제공
2. 소프트웨어 개발 툴이 아닌 빌드나 배치시 코드를 자동으로 생성할 수 있도록 정보 제공
3. 실행 시 (런타임) 특정 기능을 실행하도록 정보 제공

## **어노테이션 동작 순서**

1. 어노테이션 정의
2. 클래스에 어노테이션 배치
3. 코드 실행 도중 Relfection을 이용하여 추가 정보를 획득하여 특정 기능 실행

- Reflection  
  JVM에서 실행되는 어플리케이션의 런타임 동작을 검사하거나 수정할 수 있는 기능이 필요한 프로그램에서 사용된다. 클래스의 구조를 개발자가 확인할 수 있고, 값을 가져오거나 메소드를 호출하는 데 사용된다. 스프링에서 런타임시 개발자가 등록한 빈을 어플리케이션에서 가져와 사용할 수 있게 된다.

## **@ComponentScan**

@Component, @Service, @Repository, @Controller, @Configuration 어노테이션이 붙은 클래스 Bean들을 찾아 Context에 Bean 등록을 해주는 어노테이션이다.  
@ComponentScan은 시작 지점을 설정하는 basePackages(), basePackageClasses() 두 가지 속성이 있다.

- basePackages(): scan을 시작할 패키지를 문자열로 지정
- basePackageClasses(): 스캔 클래스 타입을 지정

<br>

## **@Component**

개발자가 직접 작성한 클래스를 Bean으로 등록하기 위한 어노테이션이다.  
@Controller, @Service, @Repository 어노테이션들은 @Component 어노테이션의 구체화된 형태이다.
(value = "") 옵션이 있고, 해당 옵션을 사용하지 않는다면 클래스의 이름을 camelCase로 변경한 것이 bean id로 등록된다.

<br>

## **@Bean**

개발자가 직접 제어 불가능한 외부 라이브러리 등을 Bean으로 만들려고 할 때 사용되는 어노테이션이다.
(name ="") 옵션이 있고, 해당 옵션을 사용하지 않는다면 메소드 이름을 camelCase로 변경한 것이 bean id로 등록된다.

<br>

## **@Autowired, @Qualifier**

@Autowired: field(속성), setter, method, constructor(생성자)에서 사용하여 Type에 따라 자동으로 Bean을 주입한다. Type을 먼저 확인하여 찾지 못하는 경우에는 name에 따라서 Bean을 주입 하는데, 이때 해당 타입의 Bean 객체가 존재하지 않거나 2개 이상 존재할 경우 스프링 예외가 발생한다.  
@Qualifier: 사용할 의존 객체를 선택할 수 있게 해준다.

같은 타입의 Bean이 두 개 이상 존재하는 경우 어떤 Bean을 주입해야 할지 알 수 없기 때문에 스프링 컨테이너를 초기화하는 과정에서 예외가 발생한다. 이 경우 @Qualifier 어노테이션을 @Autowired와 함께 사용하여 어떤 Bean을 사용할지 명시할 수 있다.
