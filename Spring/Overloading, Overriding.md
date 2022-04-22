# 오버로딩과 오버라이딩

## **오버로딩(Overloading)**

같은 이름의 메소드 여러개를 가지면서 매개변수의 유형과 개수가 다르도록 하는 기술

## **오버라이딩(Overriding)**

상위 클래스가 가지고 있는 메소드를 하위 클래스가 재정의해서 사용

<br>

## 오버로딩 예제

소스 코드

```Java
class Overload {

    void cat() {
        System.out.println("매개변수 없음");
    }

    void cat(int a, int b) {
        System.out.println("매개변수 :" + a + ", " + b);
    }

    void cat(String c){
        System.out.println("매개변수 : "+ c);
    }

}

public class Test {
    public static void main(String[] args) {

        Overload ol = new Overload();

        ol.cat();

        ol.cat(10, 20);

        ol.cat("예제 테스트");

    }
}
```

실행 결과

```Java
매개변수 없음
매개변수 : 10, 20
매개변수 : 예제 테스트
```

<br>

---

## 오버라이딩 예제

소스 코드

```Java
class Man {
    public String name;
    public int age;

    public void info() {
        System.out.println("남자의 이름은" + name + ", 나이는 " + age + "살 입니다.");
    }

}

class Hobby {
    String hobby;

    public void info() {
        super.info();
        System.out.println("남자의 취미는" + hobby + "입니다.");
    }
}

public class Test {
    public static void main(String[] args) {

        Hobby hobby = new Hobby();

        hobby.name = "X";
        hobby.age = "99";
        hobby.hobby = "게임";

        hobby.info();

    }

}

```

실행 결과

```Java
남자의 취미는 게임입니다.
```
