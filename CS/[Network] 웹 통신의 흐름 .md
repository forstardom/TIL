## 웹 사이트에 접속할 때 일어나는 일

<br>

3줄 요약

1. 웹 브라우저에 도메인 입력
2. DNS Server에 해당 도메인에 매핑되는 IP 주소 요청
3. DNS Server로부터 받은 IP주소로 웹 서버에 접속
   <br>
   <br>

### **1. 웹 브라우저에 도메인 입력**

**1-1. Browser DNS Cache**  
PC는 가장 먼저 브라우저 내에 존재하는 Browser DNS Cache라는 공간을 탐색한다. 브라우저 종류마다 공간이 다 다른데, Chrome의 경우 브라우저 창에 chrome://net-internals/#dns 라고 입력하면 해당 공간으로 접근 가능 하다.

**1-2. OS DNS Cache**  
만약 Browser DNS Cache에서 찾지 못하면 OS에 저장된 DNS Cache를 탐색한다. Hosts라 불리는 OS DNS Cache 파일의 위치는 Windows: C:\Windows\System32\drivers\etc\hosts MAC: /private/etc/hosts 에 위치한다.

**1-3. Router DNS Server**  
만약 OS DNS Cache에서도 찾지 못하면 Router DNS Server라는 곳을 조회한다. Router에서 DNS 기록을 캐싱하고 있기 때문에 접속하려는 도메인의 IP 주소를 얻어올 수 있는 것 이다.

**1-4. DNS Server**  
만약 Router DNS Server에도 도메인에 대한 IP 주소가 없다면 Root DNS Server부터 조회하며 아래 과정을 통해 IP주소를 알아내야 한다.  
<br>

---

<br>

### **2. DNS Server에 해당 도메인에 매핑되는 IP 주소를 요청**

접속하려는 도메인에 해당하는 IP 주소를 알아내기 위해 DNS Server에 Resursive Query를 진행한다. 최종적으로는 DNS Server는 해당 도메인에 매핑되는 웹 서버의 IP 주소를 사용자에게 반환하거나 찾지 못하는 경우에는 에러를 발생시킨다.

**DNS 질의 과정**

(1) 사용자의 PC는 가장 먼저 지정된 DNS Server에 DNS Query를 송신한다(우리나라의 경우 통신사 별로 지정된 DNS Server가 존재)
이때 지정된 DNS Server를 DNS Recursor라고 부른다.(Recursive Query 수행)

(2) 지정된 DNS Server는 Root Name Server에 www.google.com을 질의 하는데, 이때 Root Name Server는 "나는 걔 IP 주소 같은 건 모르겠고, .com Name Server IP 주소는 알아. 그거 줄게" 라고 .com Name Server IP 주소를 넘겨준다.

(3) PC는 다시 .com Name Server에 www.google.com을 질의하는데, 이때 .com Name Server도 "나도 걔 IP 주소 같은 건 모르겠고, google.com Name Server IP 주소는 아니까 그거 줄게" 라고 google.com Name Server IP 주소를 넘겨준다.

(4) 최종적으로 PC는 google.com Name Server에 www.google.com을 질의하는데, 드디어 사용자가 원하는 구글의 IP 주소를 받을 수 있다.  
<br>

---

<br>

### **3. DNS Server로부터 받은 IP주소로 웹 서버에 접속**

DNS Server로부터 웹 서버의 IP 주소를 받았다고 끝난 것이 아니라 웹 사이트는 브라우저에 띄울 수 있도록 이미지 파일, CSS 등과 같은 컨텐츠를 웹 서버로부터 받아야 한다. 이러한 정보들은 HTTP Request를 통해 요청을 하고, HTTP Response를 통해 받아온다. (HTTP Request는 인터넷 프로토콜을 사용해서 해당 웹 서버와 연결을 해야한다.)

**3-1. Browser와 웹 서버 간의 Connection**  
인터넷 프로토콜은 여러 종류가 있지만 웹 사이트의 HTTP 요청의 경우 일반적으로 TCP를 사용한다. TCP Connection을 위해 TCP Socket을 개방하고, TCP 3 Way-Handshake라는 연결 검증 절차를 성공해야지만 데이터를 주고 받을 준비가 된다.

TCP 3 Way-Handshake란?  
본격적으로 통신하기 전, Client <-> Server 간의 연결이 잘 되었는지 확인하는 과정이다. 아래와 같이 3단계의 인증 과정을 거친다.
(SYN = Synchronize Sequence Numbers, ACK = Acknowledgement)

(1) Client -> Server: SYN 패킷을 서버에 보내 Connection 요청  
(2) Server -> Client: SYN+ACK으로 응답  
(3) Client -> Server: ACK 패킷을 서버에 보냄

**3-2. Browser가 웹 서버에 HTTP Request**  
TCP로 웹 서버와 연결이 완료 되었으니 TCP Socket을 통해 HTTP Request(GET)를 전송한다. 요청시 비밀 자료를 포함할 수도 있고, form 형식으로 제출하는 경우에는 POST 요청도 사용할 수 있다.

아래와 같은 다른 부가적인 정보들도 함께 전달된다.

- Browser Identification (User-Agent Header)
- 수신할 Request 종류(Accept Header)
- 추가적인 Request를 위해 TCP Connection 유지를 요청하는 Connection Header
- Browser에서 얻은 Cookie 정보

**3-3. 웹 서버의 Request 처리 및 Response 생성**  
웹 서버는 Browser로부터 받은 HTTP Request를 Request Handler에 전달하여 Request 내용을 읽고 Response를 생성하게 된다.

Request Handler란?  
프로그래밍 언어로 작성된 프로그램을 의미하며 Request와 Response의 Header, Cookie를 읽어서 Request가 무엇인지 파악하고, 필요하다면 웹 서버에 정보를 업데이트 하기도 한다. 그 후 HTTP Response를 JSON, XML, HTML 등의 특정 포맷으로 작성한다.

**3-4. 웹 서버의 HTTP Response 전송**  
HTTP Response에는 아래와 같은 정보가 포함된다.

- Browser가 요청한 웹 페이지
- Status Code(현재 Response 상태)
- Compression Type(Content-Encoding, 인코딩 방식)
- Cache-Control(페이지 캐싱 방법)
- (설정할 Cookie가 있다면) Cookie
- 개인 정보
- etc

Status Code 종류

- 1xx: 정보만 담긴 메시지
- 2xx: 성공적인 Response
- 3xx: Client를 다른 URL로 Redirect
- 4xx: Client 측 에러 발생
- 5xx: Server 측 에러 발생

**3-5. Browser의 HTML Content Rendering**  
Browser는 HTML Content를 단계적으로 보여준다.

(1) HTML의 기본 틀을 Rendering 한다.  
(2) HTML Tag들을 체크 후, 추가적으로 필요한 Image, CSS, JS 파일 등과 같은 웹 페이지 구성 요소들을 GET으로 요청한다. (정적 컨텐츠들은 Browser에 의해 캐싱되어 나중에 해당 페이지를 재방문했을 때, 다시 서버로부터 불러오는 등의 과정이 생략되어 웹 페이지 로딩 속도가 빨라진다.)  
(3) 최종적으로 웹 페이지 Rendering
