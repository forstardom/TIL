## REST API - Set HTTP Headers

##

<br>

### 1 Content-Location

요청의 응답 헤더에 새로 생성된 리소스를 식별할 수 있는 속성이다. (HATEOAS로 Content-Location 대체 가능)

```Java
POST /users {
    "name": "yoon"
}
```

위와 같은 요청은 매번 다른 리소스를 반환한다.  
1 번째: /users/1  
2 번째: /users/2  
n 번째: /users/n

따라서 요청의 응답 헤더에 새로 생성된 리소스를 식별할 수 있는 Content-Location 속성을 이용한다.

```Java
HTTP/1.1 200 OK
Content-Location: /users/1
```

<br>

### 2. Content-Type

application/json을 우선으로 사용한다. application/xml 등으로 응답 포맷을 여러 개로 나누면 요청 포맷도 나눠야 한다.
<br>

### 3. Retry-After

비정상적인 방법(DoS, Brute-force attack)으로 API 서버를 이용하려는 경우 429 Too Many Requests 오류 응답과 함께 일정 시간 뒤 요청할 것을 나타낸다.
<br>

```Java
HTTP/1.1 429 Too Many Requests
Retry-After: 3600
```

<br>

### 4. Link

페이징 처리를 위해 사용한다.(고유한 URL을 구성하는 대신 링크 헤더 값을 사용하여 호출하는 것이 중요)

```Java
HTTP/1.1 200 OK
Link: <https://api.test.com/users?page=3&per_page=100>; rel="next",
    <https://api.test.com/users?page=50&per_page=100>; rel="last"
```

- rel
  - next: 바로 다음 페이지에 결과에 대한 링크 관계
  - last: 결과의 마지막 페이지에 대한 링크 관계
  - first: 결과의 첫 페이지에 대한 링크 관계
  - prev: 바로 이전 결과 페이지에 대한 링크 관계
