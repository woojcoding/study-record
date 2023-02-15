<details>
<summary> 인터넷 네트워크</summary>
<div markdown="1">

## 1. 인터넷 통신  

클라이언트 – 인터넷 – 서버  
인터넷은 복잡한 망으로 구성되어있다
수많은 노드들을 거쳐 이동하게 되다.

## 2.  IP(Internet Protocol)

지정한 IP 주소에 데이터를 전달하는데 이 때 패킷이라는 통신 단위로 데이터를 전달한다.

### IP 패킷
- 클라이언트 IP, 서버 IP, 데이터로 구성된 IP 패킷을 전송한다.
- 노드 간 순회를 하며 결국 서버 IP에 도달하게 된다.

### IP 프로토콜의 한계
- 비연결성 : 패킷을 받을 대상이 없거나 서비스 불능 상태여도 패킷을 전송한다.
- 비신뢰성 : 패킷 소실, 패킷 전달 순서 문제 발생 -> TCP 프로토콜로 해결
- 프로그램 구분 : 같은 IP를 사용하는 서버에서 통신하는 애플리케이션이 둘 이상이면?

## 3. TCP

### 인터넷 프로토콜 스택의 4계층

애플리케이션 계층 – HTTP, FTP
전송 계층 – TCP, UDP
인터넷 계층 – IP
네트워크 인터페이스 계층

애플리케이션 – 채팅 프로그램 , SOCKET 라이브러리  
OS – TCP, IP  
네트워크 인터페이스 – LAN 드라이버, LAN 장비

1) 프로그램이 Hello world! 메시지 작성
2) SOCKET 라이브러리를 통해 OS계층에 전달한다.
3) OS 계층에서 메시지 데이터를 포함하여 TCP 정보를 생성한다.
4) TCP 데이터를 포함하여 IP 패킷을 생성한다.
5) LAN에서 이 패킷에 Ethernet frame을 포함시켜 인터넷에 전달한다.


#### TCP/IP 패킷 정보
IP – 출발지 IP, 목적지 IP, 기타...  
TCP – 출발지 PORT, 목적지 PORT, 전송 제어, 순서, 검증 정보

### TCP (Transmission Control Protocol, 전송 제어 프로토콜)

- 연결지향 : TCP3 3 way handshake (가상 연결)
- 데이터 전달 보증
- 순서 보장

- 신뢰할 수 있는 프로토콜
- 현재는 대부분 TCP 사용

#### 3 way handshake

SYN(접속 요청) / ACK(요청 수락) / 3.ACK와 함께 데이터 전송 가능


<connect, 연결과정>

클라이언트 – 1. SYN → 서버  
클라이언트 ← 2. ACK + SYN - 서버  
클라이언트 – 3. ACK → 서버
---------------------------------
클라이언트 – 4. 데이터 전송 → 서버

####  데이터 전달 보증

클라이언트 – 1. 데이터 전송 → 서버  
클라이언트 ← 2. 데이터 잘 받았음 – 서버

####  패킷 순서 보장

클라이언트 - 1. 패킷1, 2, 3 순서로 전송했으나 패킷2, 3 순서가 다르게 도착 → 서버  
클라이언트 ← 2. 패킷2부터 다시 전송해줘 – 서버

### UDP (User Datagram Protocol, 사용자 데이터그램 프로토콜)
- 하얀 도화지에 비유(기능이 거의 없음)
- 데이터 전달 보증 X
- 순서 보장 X
- 연결지향 – TCP 3 handshake X
- 데이터 전달 및 순서 보장이 되지 않으나 단순하고 빠르다.

- IP와 거의 같으며 PORT, 체크섬 정도만 추가된 것
- 애플리케이션에서 추가 작업이 필요하다.

## 3. PORT
같은 IP 내에서 프로세스를 구분한다.
-> PORT를 통해 프로세스 구분이 가능하기에 원활한 통신이 가능해진다.

- 0 ~ 65535할당 가능
- 0 ~ 1023 : 잘 알려진 포트로 사용하지 않는 것이 좋음
  

- FTP - 20, 21
- TELNET - 23
- HTTP - 80
- HTTPS - 443

####  TCP/IP 패킷
- 출발지 IP, PORT
- 도착지 IP, PORT
- 전송데이터

## 4. DNS (Domain Name System)
IP는 기억하기 어렵다.  
IP는 변경될 수 있다.  

→ DNS를 사용하여 도메인 명을 IP 주소로 변환한다.  

클라이언트 - 1. 도메인 명: google.com → DNS 서버  
클라이언트 ← 2. 응답 200.200.200.2 - DNS 서버  
클라이언트 - 3. 접속 200.200.200.2 → 서버

## 정리
- 인터넷 망을 통해 통신을 하기 위해서는 IP 프로토콜이 필요하다.  
- IP 프로토콜만으로는 잘 전송되었는지 실뢰할 수도 없고 순서 보장도 못받는다.   
또한 PORT라는 개념도 존재하지 않는다.  
-> 이러한 문제들을 TCP 프로토콜이 해결해준다.  
- UDP는 IP에 PORT 개념정도만 추가된 것으로 필요하면 애플리케이션에서 기능을 확장할 수 있다.  
- PORT는 같은 IP 안에서 사용되는 애플리케이션을 구분하기 위하여 사용한다.  
- DNS는 도메인 명을 IP 주소로 변환하는데 사용된다.

</div>
</details>

<details>
<summary> URI와 웹 브라우저 요청 흐름</summary>
<div markdown="1">

## 1. URI(Uniform Resource Identifier)

## URI
- Uniform : 리소스 식별하는 통일된 방식
- Resource : 자원, URI로 식별할 수 있는 모든 것(제한 없음)
- Identifier : 다른 항목과 구분하는데 필요한 정보
-  URL, URN ⊂  URI
- URL : Uniform Resource Locator
- URN : Uniform Resource Name

## URL, URN
- URL : 리소스의 위치를 지정
- URN : 리소스의 이름을 부여
- 위치는 변할 수 있지만 이름은 변하지 않는다.
- URN 이름만으로 실제 리소스를 찾을 수 있는 방법은 보편화 되지 않았다.

## URL 문법

scheme://[userinfo@]host[:port][/path][?query][#fragment]  

https://www.google.com:443/search?q=hello&hl-ko 

- 프로토콜(https)
- 호스트명(www.google.com)
- 포트번호(443)
- 패스(/search)
- 쿼리파라미터(q=hello&hl=ko)

### scheme
- 주로 프로토콜 사용
- 프로토콜 : 어떤 방식으로 자원에 접근할 것인가에 대한 클라이언트와 서버와의 규칙 ex) http, https, ftp 등
- http는 80 포트, https는 443 포트를 주로 사용하며 포트는 생략 가능하다
- https는 http에 보안을 추가한 것이다.

### userinfo
- URL에 사용자 정보를 포함하여 인증해야 할 떄 사용
- 거의 사용하지 않음

### host
- 호스트명
- 도메인명 또는 IP 주소를 직접 사용가능

### PORT
- 포트
- 접속포트
- 일반적으로 생략, HTTP는 80, HTTPS는 443 포트

### path
- 리소스의 경로, 계층적 구조
- /members/100

### query
- key=value 형태
- ?로 시작, &로 추가가능 ?keyA=valueA&keyB=valueB
- query parameter, query string 등으로 불리며 웹서버에 문자형태로 제공하는 파라미터이다.
### fragment
- fragment
- html 내부 북마크 등에 사용
- 서버에 전송하는 정보는 아니다.

## 2. 웹 브라우저 요청 흐름
https://www.google.com:443/search?q=hello&hl-ko

1. DNS 조회 -> www.google.com:443 -> IP : 200.200.200.2
2. 웹브라우저가 HTTP 요청 메시지 생성  
    GET /search?q=hello&hl-ko HTTP/1.1   
    HOST: www.google.com
3. SOCKET 라이브러리를 통해 OS 계층에 있는 TCP/IP에 전달  
   1) IP와 PORT를 찾았으니 3 way handshake를 통해 구글서버와 연결
   2) TCP/IP에 데이터 전달
4. TCP/IP 패킷 생성, HTTP 메시지 포함
5. 네트워크 인터페이스로 전달
6. 인터넷을 통해 서버로 요청 패킷 전달
7. 구글 서버에서 TCP/IP 패킷, HTTP 응답 메시지를 포함한 응답 패킷 반환
8. 웹 브라우저 HTML 렌더링
</div>
</details>







