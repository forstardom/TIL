# CSR(Client Side Rendering), SSR(Server Side Rendering)

## **CSR(Client Side Rendering)이란?**

- HTML 결과를 자바스크립트를 사용해 웹 브라우저에서 동적으로 생성해서 적용하는 것
- 주로 동적인 화면에 사용, 웹 환경을 마치 앱처럼 필요한 부분마다 변경할 수 있음
- 초기 로딩 속도가 느리지만, 클라이언트에서 이루어져서 빠른 화면 전환이 가능
- 예) 구글 지도, 구글 메일, 구글 캘린더
- 관련기술: React, Vue.js

## **SSR(Server Side Rendering)이란?**

- 서버에서 최종 HTML을 생성해서 클라이언트에 전달하는 것
- 초기 로딩 속도가 빨라서 사용자가 느끼기엔 좋지만, 동작은 하지 않음
- 화면 전환에 있어서 서버에 요청해야 하므로 서버에 부담을 줄 수 있음
- 주로 정적인 화면에 사용
- 관련기술: JSP, Thymeleaf

## **참고**

- React, Vue.js를 CSR + SSR 동시에 지원하는 웹 프레임워크도 있음
- SSR을 사용하더라도, 자바스크립트를 사용해서 화면 일부를 동적으로 변경 가능
