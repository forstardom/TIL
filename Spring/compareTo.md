# compareTo() 메소드

## **1. 숫자 비교**

```Java
기준값.compareTo(비교값)
```

- 기준값 > 비교값
  - 1 반환
- 기준값 < 비교값
  - -1 반환
- 기준값 == 비교값
  - 0 반환

### int 형 비교

- compare() 사용

```Java
int a = 10;
int b = 5;

Integer.compare(x,y);
```

<br>

---

## **2. 문자 비교**

- 기준값 != 비교값
  - 다른 문자의 개수만큼 반환(기준값과 비교값의 첫 문자가 동일해야만 다른 문자 개수만큼 반환)
- 기준값 == 비교값
  - 0 반환

```Java
String str = "abcd";

str.compareTo("ab");
>> 3 - 2 = 1

str.compareTo("c");
>> -2
```

## **str.compareTo("c")의 결과가 -2가 나오는 이유**

- 기준값과 비교값의 첫 문자가 동일한 문자가 아니고, 중간에 같은 문자일 경우에는 각각의 문자열에서 가장 낮은 아스키코드의 차이값을 반환하기 때문이다.

```Java
String str = "abcd";

str.compareTo("c");
>> 각각 문자열의 가장 낮은 아스키코드 문자: a, c
>> 97 - 99 = -2
```
