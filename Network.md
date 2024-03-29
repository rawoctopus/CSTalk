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

## MAC 주소
- 네트워크 상에서 서로를 구분하기 위하여 Device 마다 할당된 __물리적인 주소__. MAC 주소는 총 12자리 숫자로 구성되어 있으며 숫자중 앞의 6자리(24bit)는 벤더사에 할당되며 나머지 6자리(24bit)는 각 벤더에서 제품에 할당한다.
- 통신을 위해서는 MAC 주소를 알아야 한다. IP주소로 MAC 주소를 알기 위해서는 IP 주소를 MAC으로 바꾸는 ARP(Address Resolution Protocol) 과정이 필요하다.
- IP 주소는 집 주소(우편번호)와 같은 논리적인 주소를 뜻하고, MAC 주소는 그 집에 사는 사람이 누군지(이름)와 같은 물리적인 주소를 뜻한다.

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

## URL vs URL

### URI (Uniform Resource Identifier)
통합 자원 식별자.
- rewrite
    - rewrite 기술을 이용하여 만든 의미있는 식별자
    - [http://localhost/service/Customer](http://localhost/service/Customer) → [http://localhost/Customer](http://localhost/Customer)
    - [http://www.store.com/products.aspx?category=books](http://www.store.com/products.aspx?category=books) → http://www.store.com/products/category/books
- REST 서비스
    - url로 실행되는 서비스
    - [https://www.google.co.kr/search?q=uri](https://www.google.co.kr/search?q=uri)
- Web-oriented architecture
    - kakaotalk://sendmsg?text=hello! (kakaotalk 프로토콜을 해석할 수 있는 프로그램이 핸들링.)

### URL (Uniform Resource Locator)
자원. 파일의 위치.
URL은 URI의 특별한 형태이자 부분 집합으로 볼 수 있다.
- [http://example.xxx/blog/sample.pdf](http://example.xxx/sample.pdf)

### Example

**URI**  
주소가 [http://](http://naver.com)example.xxx/blog/category 라고 했을 때, 요청하는 주소가 파일이라기 보다는 구분자가 되는 것,
실제로 해당 웹사이트에 blog/category 라는 파일은 없다.

**URL**  
[http://example.xxx/blog/sample.pdf](http://example.xxx/sample.pdf)
[example.xxx](http://example.xxx) 서버에서 blog라는 폴더 안의 sample.pdf를 요청하는 것.
  
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

<br>

## HTTP와 HTTPS
- HTTP
  - HyperText Transfer Protocol
  - 웹서버와 사용자의 인터넷 브라우저 사이에 문서를 전송하기 위한 통신 규약
  - 암호화가 전혀 되어 있지 않은 프로토콜
  
- HTTPS
  - HTTP + over Secure socket layer
  - http에 보안을 강화한 프로토콜로 패킷을 암호화하여 전송
  - L4 전송계층에서 암호화가 이루어짐 -> TLS(Transport Layer Security)
  - 암호화 과정 때문에 HTTP보다 속도가 느리지만, 요즘은 인터넷 속도의 향상으로 사실상 큰 차이 없음

<br>

## Gateway란
   - 서로 다른 네트워크로 이동하기 위한 관문
   - 두 컴퓨터가 네트워크 상에서 서로 연결되려면 동일한 통신 프로토콜을 사용해야한다. 따라서 프로토콜이 다른 네트워크 상의 컴퓨터와 통신하려면 두 프로토콜을 적절히 변환해주는 변환기가 필요한데, 게이트웨이가 바로 이러한 변환기 역할을 한다.
   - 일반적으로 하드웨어 형태
   - 라우터와 동일한 개념으로 이해할 수 있다. 하지만 좀 더 포괄적인 개념이다.
     - 라우터 : 네트워크 장비의 일종으로, 패킷을 다른 네트워크로 보내주는 역할을 한다. 이와 함께 최적의 네트워크 경로를 찾아주는 역할도 함께 수행한다.
   - 예시로는 인터넷 유무선 공유기가 우리가 만나는 첫 번째 게이트웨이다.
     - 공유기는 사용자 컴퓨터의 네트워크와 인터넷을 연결하여 사용자가 웹 사이트에 접근할 수 있도록 관문을 열어준다. 사용자가 속해 있는 로컬 네트워크의 통신 프로토콜과 인터넷의 통신 프로토콜이 다르기 때문이다. 참고로 공유기는 게이트웨이의 역할과 라우터의 역할, 방화벽 역할 등을 동시에 제공하는 종합 네트워크 장비다.
   - 일반적으로 게이트웨이의 IP주소는 해당 네트워크 내 컴퓨터에 할당된 IP 주소 중 끝자리만 다른 형태다. 보통 1을 지정한다.
     - ex) 컴퓨터 IP 주소가 123.123.123.123 이면, 게이트웨이 주소는 123.123.123.1이 된다.

<br>
   
## 오류 제어 기법
*데이터 링크 계층에서*
- Forward Error Correction
- Backward Error Correction

#### 1. Forward Error Correction (전진 오류 수정)
- 수신 측에서 오류를 스스로 검출, 정정할 수 있는 방법으로, 송신시 오류 복구를 위한 잉여 비트를 추가하여 전송하는 방식

    ##### 1.1. 수정 방식
    - **해밍 코드** : 자기 정정 부호로서, 오류를 검출해서 1비트의 오류를 수정하는 방식
    - **상승 코드** : 해밍 코드 방식은 1개의 오류 비트를 수정할 수 있지만 상승 코드 방식은 여러 개의  비트의  오류가 있더라도 한계 값(경계 값), 순차적 디코딩을 이용하여 모두 수정할 수 있는 방식

#### 2. Backward Error Correction (후진 오류 수정)
- 전송된 데이터에 오류가 발생된 경우, 송신 측에 오류 사실을 알려서 재전송(ARQ)으로 복원하는 방식

    ##### 2.1. 오류 검출 방식
    - **패리티 검사** (Parity check) : 데이터의 끝에 한 비트를 추가하여 1의 개수로 오류 유무 판단
    - **블록합 검사** (Block Sum check) : 이차원 패리티 검사, 가로와 세로로 두 번 검사하여 다중 비트 오류와 폭주 에러를 검출할 가능성을 높임
    - **순환 잉여 검사** (Cycle Redundancy Check, CRC) : 이진 나눗셈 연산을 기반으로 오류를 검출하는 방식, 성능이 우수하며 여러 비트에서 발생하는 집단 오류(burst error)도 검출 가능
    - **검사합 검사** (Check Sum) : 전송 데이터의 맨 마지막에 앞서 보낸 모든 데이터를 다 합한 합계를 보수화하여 전송, 수신 측에서는 모든 수를 합산하여 검사하는 방법

    ##### 2.2. (검출 후) 재전송 방식
    - Stop and Wait ARQ
    - Go-Back-N
    - Selective-Repeat ARQ
    - 적응성(Adptive) ARQ
    
#### 참고
http://www.jidum.com/jidums/view.do?jidumId=426
    
<br>

## TCP/IP 프로토콜 스택 4계층
  #### 1. LINK 계층
  - 물리적인 영역의 표준화에 대한 결과. 가장 기본이 되는 영역으로 LAN, WAN, MAN과 같은 네트워크 표준과 관련된 프로토콜을 정의하는 영역.
  #### 2. IP 계층
  - 경로검색을 해주는 계층. 
  - IP 자체는 비연결지향적이며 신뢰할 수 없는 프로토콜. 데이터를 전송할 때마다 거쳐야 할 경로를 선택해주지만, 그 경로는 일정치 않음. 
  - 특히 데이터 전송 도중에 경로상에 문제가 발생하면 다른 경로를 선택해 주는데, 이 과정에서 데이터가 손실되거나 오류가 발생하는 등의 문제가 발생한다고 해서 이를 해결해주지 않음. 
  - 즉, 오류발생에 대한 대비가 되어있지 않은 프로토콜
  #### 3. TCP/UDP(전송) 계층
  - 데이터의 실제 송수신을 담당. 
  - UDP는 TCP에 비해 상대적으로 간단하며, TCP는 신뢰성 있는 데이터의 전송을 담당. 
  - 그런데 TCP가 데이터를 보낼 때 기반이 되는 프로토콜이 IP이다. 앞서 말했듯이 IP 계층은 문제가 발생한다면 해결해주지 않는 신뢰되지 않은 프로토콜이다 
  - 그 문제를 해결해 주는 것이 TCP. 데이터가 순서에 맞게 올바르게 전송이 갔는지 확인을 해주며 대화를 주고받는다. 확인절차를 걸쳐서 신뢰성 없는 IP에 신뢰성을 부여한 프로토콜이라 생각하면 됨.
  #### 4. APPLICATION 계층
  - 이러한 서버와 클라이언트를 만드는 과정에서 프로그램의 성격에 따라 데이터 송수신에 대한 약속(규칙)들이 정해지기 마련인데, 이를 가리켜 Aplication 프로토콜이라한다.

<br>

## Multi-Thread 서버
  - 듣기 소켓을 통해서 새로운 클라이언트가 들어오면 fork 함수를 이용해서 자식 프로세스를 만드는 대신에, pthread_create 함수를 이용해서 새로운 스레드를 만드는 것이다. 이 스레드는 문맥을 포함한 코드 조각으로 듣기 소켓의 소켓 지정 번호를 매개 변수로 받아들일 수 있다. 이 듣기 소켓을 이용해서 클라이언트를 처리하는 식이다.
  - 핵심은 서버 프로그램이 듣기 소켓과 연결 소켓이 분리되어 있는데, 듣기 소켓에 클라이언트 연결이 들어와서 연결 소켓이 만들어 지면, 스레드를 만들어 클라이언트 요청을 처리하는데 있다. (대리자)
  - 스레드는 코드 조각이므로 프로세스를 복사하는 멀티 프로세스 방식보다 좀 더 작고 빠르게 작동하는 프로그램을 만들 수 있다. 반면 독립된 프로세스 단위로 구동되지 않기 때문에, 디버깅이 힘들다는 단점이 있다. 또한 하나의 스레드에 생긴 문제가 전체 프로세스에 문제를 줄 수 있다는 문제점도 있다.
  - 구현 예제 : https://www.joinc.co.kr/w/Site/Network_Programing/Documents/Multi_thread

<br>

## HTTP keep alive
#### 정의
  - HTTP 기본 구조를 바탕으로 맺어진 Socket 연결이 종료된 시점(HTTP Response 이후)부터 웹 서버에 정의된 Keep alive Timeout까지 기존 연결(Socket)을 유지하는 기능.
  - 즉, 정의된 Timeout 내에 새로운 HTTP 요청이 발생한다면 연결을 유지하고 그렇지 않다면 연결을 끊는 기능
#### 예시
  - image를 4개를 보여주는 구조에서 client는 동시에 2개의 image만 얻어 올수 있고 1개의 image는 얻는데 2초 걸리고 port를 여는데 1초가 걸린다고 가정.
  - keep alive : false 
    처음 server에 2개의 port를 열고 image를 얻고 client socket의 닫고 ( 3초 )    
    다시 server에 2개의 port를 열고 image를 얻고 client socket을 닫음 ( 3초 )    
    총 6초가 걸림.   
    keep alive : true    
    처음 server에 2개의 port를 열고 image를 얻고 ( 3초 )     
    다시 첫번째 요청에서 열어 둔 2개의 port에 2개의 image를 얻음 ( 2초 )    
    keep alive time out이 되었을 때 client의 socet이 닫히거나 browser가 더 이상 얻어 올 것이 없으면 자동으로 닫어 버림.     
    총 5초가 걸림.   
#### 어떻게 쓸 수 있는가?
  - 개발자 영역에서 할 부분은 전혀 없음
  - client(browser)는 http 1.1을 준수하고 이해 할수 있다고 request에 Connection: Keep-Alive를 넣어서 Server에 전송    
    즉 client는 http 1.1 spec을 구현하고,    
    server도 http 1.1 spec을 구현하고 keep alive 기능을 활성화하고 keep alive time out을 설정

#### 참고
https://b.pungjoo.com/entry/HTTP-11-Keep-Alive-%EA%B8%B0%EB%8A%A5%EC%97%90-%EB%8C%80%ED%95%B4

<br>
