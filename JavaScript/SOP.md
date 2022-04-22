# SOP(Same-Origin Policy)

## **SOP(Same-Origin Policy)란?**

웹 어플리케이션 및 브라우저에서 중요한 보안 개념으로, 동일 출처의 리소스에 한해서만 데이터(DOM)에 접근할 수 있도록 하는 웹 브라우저 보안 정책으로, 동일 출처인지 판단하는 기준은 두 URL의 프로토콜, 포트 (명시한 경우), 호스트가 모두 같아야 동일 출처라고 말한다.

**동일 출처 판단 기준**  
URI 를 결정하는 알고리즘은 RFC 6454 에 명시되어 있으며 출처(Origin)는 Protocol, Host, Port 번호 등으로 구성된 정보를 의미하며, 만약 이 정보들 중 하나라도 다를 경우 동일 출처 원칙에 위배된 것으로 판단한다.

예시) http://forstardom.com/test/page.html

| URL                                           | 결과 이유                              |
| --------------------------------------------- | -------------------------------------- |
| http://forstardom.com/test/other.html         | 성공 경로만 다름                       |
| http://forstardom.com/test/inner/another.html | 성공 경로만 다름                       |
| https://forstardom.com/secure.html            | 실패 프로토콜 다름                     |
| http://forstardom.com:81/test/etc.html        | 실패 포트 다름 (http://는 80이 기본값) |
| http://new.forstardom.com/test/other.html     | 실패 호스트 다름                       |

만일 동일 출처 원칙에 위배되는 AJAX 요청을 전송했을 경우, 아래와 같이 전송된 요청에서 Access-Control-Allow-Origin 헤더가 없다는 에러 메시지를 받게 된다.

```
XMLHttpRequest cannot load ‘https://store.company.com'. No ‘Access-Control-Allow-Origin’ header is present on the requested resource. Origin ‘http://store.company.com' is therefore not allowed access.
```

## **동일 출처 원칙을 사용하는 이유**

가장 큰 이유는 브라우저 측면에서의 웹 어플리케이션 보안 강화

1. XSS 와 같은 스크립트 삽입 공격을 통해서 출처가 다른 웹 어플리케이션에 접근을 방지한다.
2. 웹 어플리케이션은 인증된 사용자 세션정보를 HTTP Cookie에 담아서 광범위하게 사용하곤 하는데, 출처(Origin)가 다른 페이지에서 스크립트를 이용해 해당 쿠키정보를 추출할 수 있기 때문이다.
3. 데이터의 기밀성 또는 일관성을 유지하기 위해서 클라이언트 측에서 관계 없는 사이트에서 제공된 컨탠츠를 분리해야 한다.

## **동일 출처 원칙 회피방법**

1. document.domain 속성 수정
   일부 제약이 있으나 페이지의 출처를 변경 가능하다. 스크립트로 document.domain 의 값을 현재 도메인이나 현재 도메인의 상위 도메인으로 변경할 수 있는데, 상위 도메인으로 설정한 경우 (더 짧은) 상위 도메인을 동일 출처 검사에 사용한다.
2. CORS(Cross-Orgin Resource Sharing)  
   CORS는 Cross-Orgin Resource Sharing(상호 출처 자원 공유)의 약자로, 현재 접속중인 도메인의 출처와 다른 출처에 리소스를 요청 및 접근을 허가하는 웹 브라우저 보안 정책의 일환이다. 이 방법은 서버단에서 처리해줘야 하는데, 요청된 리소스를 전송할때 HTTP 헤더에 Access-Control-Allow-Origin 헤더와 접근을 허가하는 값를 추가해 응답(Response) 메시지와 함께 전송하면 브라우저에서도 상호 출처 접근을 허가해 요청한 응답 리소스를 스크립트에서 사용할 수 있다.
