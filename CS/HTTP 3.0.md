# **HTTP 3.0**

기존 TCP 기반이었던 HTTP/1, HTTP/2와는 다르게 UDP 기반의 프로토콜인 QUIC을 사용하여 통신하는 프로토콜이다.

## **QUIC이란?**

2013년에 구글에서 발표한 공식 프로토콜이며, TCP 기반으로 연결하는 TCP의 성능을 개선하고자 시작된 프로젝트에서 UDP를 채택한 기술이다. 전달 속도의 개선과 더불어 클라이언트의 서버의 연결수를 최소화하고, 대역폭(bandwidth)를 예상하여 패킷 혼잡(congestion)을 피하는 것이 주요 특징이다.

## **HTTP/3의 특징**

TCP/IP 기반의 어플리케이션 레이어 프로토콜인 HTTP를 QUIC위에 얹었다는 것이다. 이를 "HTTP over QUIC"이라고 표현하고 줄여서 HQ라고 한다. HTTP 자체가 TCP 일종이었는데 이것이 UDP 기잔의 QUIC으로 바뀐 것이 가장 큰 변화이다. HTTP/2에 있는 프레임, 스트림, 메시지 구조와 기술들은 그대로 HTTP/3로 승계 되었고, 명칭만 HQframe, QPACK 등으로 변경 되었다.

## **HTTP/3를 사용하는 이유?**

**1. 연결 설정 시 지연시간 감소**  
QUIC은 TCP를 사용하지 않기 때문에 통신을 시작할때 3-Way Handshake 과정을 거치지 않아도 된다. 클라이언트가 보낸 요청을 서버가 처리한 후 다시 클라이언트로 응답해주는 사이클을 RTT(Round Tip Time)이라고 하는데, TCP는 연결을 생성하기 위해 기본적으로 1 RTT가 필요하고, 여기에 TLS를 사용한 암호화까지 하려고 한다면 TLS의 자체 Handshake까지 더해져 총 3 RTT가 필요하다.

반면 QUIC은 첫 연결 설정에 1 RTT만 소요된다. 클라이언트가 서버에 어떤 신호를 한번 보내고, 서버도 거기에 응답하기만 한면 바로 통신을 시작할 수 있다는 것이다. 즉, 연결 설정에 드는 시간이 반 정도밖에 안 된다.

이것이 가능한 이유는 첫 번째 Handshake과정을 거칠 때 연결 설정에 필요한 정보와 데이터도 함께 보내버리는 것이다.

TCP+TLS: 데이터를 보내기 전에 신뢰성 있는 연결과 암호화에 필요한 모든 정보를 교환하고 유효성 검사를 한 뒤에 데이터를 교환  
QUIC: 처음부터 데이터를 보내기 시작

결론은 TCP+TLS는 서로 자신의 세션 키를 주고받아 암호화된 연결을 성립하는 과정을 거치고 나서야 세션 키와 함께 데이터를 교환할 수 있지만, QUIC은 서로의 세션 키를 교환하기도 전에 데이터를 교환할 수 있기 때문에 연결설정이 더 빠르다.

<br>

**2. 패킷 손실 감지에 걸리는 시간 단축**  
QUIC도 TCP와 마찬가지로 전송하는 패킷에 대한 흐름 제어를 해야 한다. 왜냐하면 QUIC, TCP 모두 결국 본질적으로는 ARQ 방식을 사용하는 프로토콜이기 때문이다. 통신 과정에서 발생한 에러를 어떻게 처리할 것인지를 이야기하는 것인데, ARQ 방식은 에러가 발생하면 재전송을 통해 에러를 복구하는 방식을 말한다.

TCP는 여러 ARQ 방식 중에서 Stop and Wait ARQ 방식을 사용하고 있다. 이 방식은 송신 측이 패킷을 보낸 후 타이머를 사용하여 시간을 재고, 일정 시간이 경과해도 수신 측이 적절한 답변을 주지 않는다면 패킷이 손실된 것으로 판단하고 해당 패킷을 다시 보내는 방식이다.

TCP에서 패킷 손실 감지에 대한 대표적인 문제는 송신 측이 패킷을 수신 측으로 보내고 난 후 얼마나 기다려줄 것인가, 즉 타임아웃을 언제 낼 것인가를 동적으로 계산해야한다는 것이다. 이때 이 시간을 RTO(Retransmission Time Out)라고 하는데, 이때 필요한 데이터가 바로 RTT(Round Trip Time)들의 샘플들이다.

한번 패킷을 보낸 후 잘 받았다는 응답을 받을 때 걸렸던 시간들을 측정해서 동적으로 타임 아웃을 정하는 것이다. 즉, RTT 샘플을 측정하기 위해서는 반드시 송신 측으로 부터 ACK를 받아야하는데, 정상적인 상황에서는 딱히 문제가 없으나 타임 아웃이 발생해서 패킷 손실이 발생하게 되면 RTT 계산이 애매해진다.

이때 이 ACK가 어느 패킷에 대한 응답인지 알기 위해서는 타임 스탬프를 패킷에 찍어주는 등 별도의 방법을 또 사용해야 하고, 또 이를 위한 패킷 검사도 따로 해줘야 한다. 이를 재전송 모호성(Retransmission Ambiguity)이라고 한다.

이 문제를 해결하기 위해 QUIC는 헤더에 별도의 패킷 번호 공간을 부여했다. 이 패킷 번호는 패킷의 전송 순서 자체만을 나타내며, 재전송 시 같은 번호가 전송되는 시퀀스 번호와는 다르게 전송마다 모노토닉하게 패킷 번호가 증가하기 때문에, 패킷의 전송 순서를 명확하게 파악할 수 있다.

TCP의 경우 타임스탬프를 통해 패킷의 전송 순서를 파악하거나 타임스탬프를 사용할 수 없는 상황이라면 시퀀스 번호에 기반하여 암묵적으로 전송 순서를 추론했다. 이에 반해 QUIC는 패킷마다 고유한 패킷 번호를 이용함으로써 앞서 봤던 불필요한 과정을 생략하고 패킷 손실 감지에 걸리는 시간을 단축할 수 있다.

<br>

**3. 멀티플렉싱 지원**  
멀티플렉싱(Multiplexing)은 위에서 TCP의 단점으로 언급했던 HOLB(Head of Line Blocking)을 방지하기 때문에 매우 중요하다. 여러 개의 스트림을 사용하면, 그중 특정 스트림의 패킷이 손실되었다고 하더라도 해당 스트림에만 영향을 미치고 나머지 스트림은 사용할 수 있기 때문이다.

참고로 멀티플렉싱은 여러 개의 TCP 연결을 만든다는 의미가 아니라, 단일 연결 안에서 여러 개의 데이터를 섞이지 않게 보내는 기법이다. 이때 각각의 데이터의 흐름을 스트림이라고 하는 것이다.

HTTP/1의 경우는 하나의 TCP 연결에 하나의 스트림만 사용하기 때문에 HOLB 문제에서 벗어날 수 없었다. 또한 한 번의 전송이 끝나게 되면 연결이 끊어지기 때문에 다시 연결을 만들기 위해서는 번거로운 Handshake 과정을 또 겪어야 했다.

비록 keep-alive 옵션을 통해 어느 정도의 시간 동안 연결을 유지할 수는 있지만 결국 일정 시간 안에 액세스가 없다면 연결이 끊어지게 되는 것은 똑같다.

그리고 HTTP/2는 하나의 TCP 연결 안에서 여러 개의 스트림을 처리하는 멀티플렉싱 기법을 도입하여 성능을 끌어올린 케이스이다. 이 경우 한번의 TCP 연결로 여러 개의 데이터를 전송할 수 있기 때문에 Handshake 횟수도 줄어들게 되어 효율적인 데이터 전송을 할 수 있게 된다.

HTTP/3도 HTTP/2와 같은 멀티플렉싱을 지원한다.

QUIC 또한 HTTP/2와 동일하게 멀티플렉싱을 지원하기 때문에, 이런 이점을 그대로 가져가고 있다. 혹여나 하나의 스트림에서 문제가 발생한다고 해도 다른 스트림은 지킬 수 있게 되어 이런 문제에서 벗어날 수 있다.

<br>

**4. 클라이언트의 IP가 바뀌어도 연결 유지**  
TCP의 경우 소스의 IP 주소와 포트, 연결 대상의 IP 주소와 포트로 연결을 식별하기 때문에 클라이언트의 IP가 바뀌는 상황이 발생하면 연결이 끊어져 버린다. 연결이 끊어졌으니 다시 연결을 생성하기 위해 결국 3 Way Handshake 과정을 다시 거쳐야 한다는 것이고, 이 과정에서 다시 레이턴시가 발생한다.

반면 QUIC은 Connection ID를 사용하여 서버와 연결을 생성한다. Connection ID는 랜덤한 값일 뿐, 클라이언트의 IP와는 전혀 무관한 데이터이기 때문에 클라이언트의 IP가 변경되더라도 기존의 연결을 계속 유지할 수 있다. 이는 새로 연결을 생성할 때 거쳐야하는 Handshake 과정을 생략할 수 있다.

<br>

Reference

- https://evan-moon.github.io/2019/10/08/what-is-http3/