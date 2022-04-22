# Web Server / Web Application Server

## **웹 서버(Web Server)**

- HTTP 기반으로 동작
- 정적 리소스 제공, 기타 부가기능
- 정적(파일) HTML, CSS, JS, 이미지, 영상
- 예) nginx, apache

## **웹 어플리케이션 서버(WAS - Web Application Server)**

- HTTP 기반으로 동작
- 웹 서버 기능 포함 + (정적 리소스 제공 가능)
- 프로그램 코드를 실행해서 어플리케이션 로직 수행
  - 동적 HTML, HTTP API(JSON)
  - Servlet, JSP, Spring MVC
- 예) Tomcat, Jetty, Undertow

## **Web Server vs WAS**

- Web Server는 정적 리소스(파일), WAS는 어플리케이션 로직
- 둘의 용어도 경계도 모호함
  - Web Server도 프로그램을 실행하는 기능을 포함하기도 함
  - WAS도 웹 서버의 기능을 제공함
- 자바는 서블릿 컨테이너 기능을 제공하면 WAS
  - 서블릿 없이 자바코드를 실행하는 서버 프레임워크도 있음
- WAS는 어플리케이션 코드를 실행하는데 더 특화

## **웹 시스템 구성 - WAS, DB**

- WAS가 너무 많은 역할을 담당, 서버 과부하 우려
- 가장 비싼 어플리케이션 로직이 정적 리소스 때문에 수행이 어려울 수 있음
- WAS 장애시 오류 화면도 노출 불가능

## **웹 시스템 구성 - WEB, WAS, DB**

- 정적 리소스는 웹 서버가 처리
- Web Server는 어플리케이션 로직같은 동적인 처리가 필요하면 WAS에 요청을 위임
- WAS는 중요한 어플리케이션 로직 처리 전담
- 효율적인 리소스 관리 방법
  - 정적 리소스가 많이 사용되면 Web Server 증설
  - 어플리케이션 리소스가 많이 사용되면 WAS 증설
- 장점
  - 정적 리소스만 제공하는 Web Server는 잘 죽지 않음
  - 어플리케이션 로직이 동작하는 WAS는 잘 죽음
  - WAS, DB 장애시 Web Server가 오류 화면 제공 가능
