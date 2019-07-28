# Network

<br>

## 노드 vs 호스트
- 노드 : 네트워크와 연결된 모든 것. 
- 호스트 : 주소가 할당된 것.
- ex)
  - 노드이자 호스트 : 컴퓨터, 라우터, 핸드폰, 등등
  - 노드(호스트X) : 모뎀, 허브, 스위치 등등

<br>

## Port number
- 네트워크를 통해 데이터를 주고받는 프로세스를 식별하기 위한 것. 
  - 호스트 내부적으로 프로세스가 할당받는 고유한 값이다.
  - (소켓 통신에서 실제로 데이터를 주고 받는 것은 호스트 내의 프로세스이다.)
- Q. 소켓 통신을 할 때, 원하는 주소로 어떻게 데이터를 주고 받을 수 있을까? 
  - IP로 호스트를 찾아가고, TCP/UDP 등 패킷의 포트넘버를 통하여 해당 프로세스를 찾아갈 수 있다.
      - 인터넷 계층에서 IP 주소로 호스트를 찾는다.
        - [IP주소로 MAC 주소를 찾는 방식 비유](http://m.cafe.daum.net/v3study/O2EQ/4?q=D_oNeYewAwh3Y0&)
      - 전송 계층에서 Port number로 호스트의 해당 프로세스를 찾아간다.
  - 패킷
    - IP Datagram에 IP가 있고,
    - 그 내부의 TCP/UDP segment에 발/수신 Port number가 있음

<br>

## HTTP Method

##### GET 방식의 특징
  - URL에 변수(데이터)를 포함시켜 요청한다.
  - 데이터를 Header(헤더)에 포함하여 전송한다.
  - URL에 데이터가 노출되어 보안에 취약하다.
  - 전송하는 길이에 제한있다.
  - 캐싱할 수 있다.

##### POST 방식의 특징
  - URL에 변수(데이터를) 노출하지 않고 요청한다.
  - 데이터를 Body(바디)에 포함시킨다.
  - 전송하는 길이에 제한이 없다.
  - 캐싱할 수 없다.
  
<br>
  
## 브라우저에서 주소창에 URL 입력시
  - 브라우저의 주소창에 URL 입력
  - 브라우저 캐시에서 DNS 레코드를 확인하여 IP주소를 찾음(없다면 DNS resolver를 통해 IP주소를 알아냄)
  - 브라우저가 서버와 TCP 연결을 시작함
  - 브라우저가 웹 서버에 HTTP 요청을 보냄
  - 서버가 요청을 처리하고 응답을 되돌려 보냄
  - 브라우저는 서버가 보낸 HTML 내용을 표시

<br>

## TCP와 UDP
  - 공통점 : TCP와 UDP 프로토콜은 모두 전송계층(Transport Layer)에서 동작하는 프로토콜이다.
  - 차이점
    - TCP
      - 신뢰성있는 데이터 전송을 지원하는 연결지향형 프로토콜이다.
      - 패킷을 성공적으로 전송하면 Acknowledgement(ACK)라는 신호를 날린다. 만일 ACK 신호가 제 시간에 도착하지 않으면 Timeout이 발생하여, 패킷 손실이 발생한 패킷에 다시 전송해준다.
      - __3-way handshaking__
      - 흐름제어(flow control), 혼잡 제어(congestion control)를 지원하며 데이터의 순서를 보장.
      - UDP에 비해 속도가 느림 => 웹 HTTP 통신, 이메일, 파일전송에 사용됨.
    - UDP
      - 비연결형 프로토콜
      - TCP와 달리 연결 설정 없음.
      - 혼잡 제어를 하지 않기 때문에 TCP보다 빠르다.
      - 데이터 전송에 대한 보장을 하지 않기 때문에 패킷 손실이 발생할 수 있음. => DNS, 멀티미디어에서 사용됨.
      - 헤더에 있는 Checksum 필드를 통해 최소한의 오류는 검출한다.
 
    - 비교 표

     |                             TCP                              | UDP                                                       |
     | :----------------------------------------------------------: | --------------------------------------------------------- |
     |     Connection-oriendted protocol (연결지향형 프로토콜)      | Connection-less protocol (비 연결지향형 프로토콜)         |
     |    Connection by byte stream (바이트 스트림을 통한 연결)     | Connection by message stream (메시지 스트림을 통한 연결)  |
     |    congestion control, flow control (혼잡제어, 흐름제어)     | X                                                         |
     |      ordered, lower speed (순서 보장, 상대적 속도 느림)      | not ordered, higher speed (순서 보장x, 상대적 속도 빠름)  |
     | reliable data transmission (신뢰성 있는 데이터 전송, 안정적) | unreliable data transmission (데이터 전송 보장 x)         |
     |      TCP packet : segment (데이터 전송 단위는 세그먼트)      | UDP packet : datagram (데이터 전송 단위는 데이터 그램)    |
     |                  HTTP, Email, File transfer                  | DNS, Boradcasting (도메인, 실시간 동영상 서비스에서 사용) |
