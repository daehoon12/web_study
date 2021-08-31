# HTTP & Network  

## 1 HTTP와 TCP/IP  

### 1.1 HTTP  
- 웹 서버와 웹 클라이언트가 데이터를 주고 받을 수 있는 프로토콜  
- 처음 나올 당시에는 주로 텍스트를 전송. 지금은 그림 동영상 뿐 아니라 웹이라는 틀을 넘어 다양하게 사용되고 있음.  

### 1.2 TCP/IP  
- 인터넷에서 컴퓨터들이 서로 정보를 주고받는 데 쓰이는 통신규약(프로토콜)의 모음. (TCP, IP, UDP, HTTP, ICMP 등)   
- **애플리케이션, 트랜스포트, 네트워크, 링크 계층**으로 나뉨

#### 1.2.1 TCP/IP 4 Layers  
1. 애플리케이션 : 유저에게 제공되는 애플리케이션에서 사용하는 통신의 움직임을 결정 (HTTP, DNS)  
2. 트랜스포트 : 애플리케이션 계층에 네트워크로 접속되어 있는 2대의 컴퓨터 사이의 데이터 흐름을 제공 (TCP, UDP)  
3. 네트워크 : 네트워크 상에서 패킷의 이동을 다룸. (라우팅) 주 프로토콜은 IP.    
4. 링크 : 네트워크에 접속하는 하드웨어적인 면을 다룸.  

#### 1.2.1 TCP/IP 통신의 흐름  
1. 클라이언트에서 어느 웹 페이지를 보고 싶다는 HTTP Request를 **어플리케이션 계층**에 알림  
2. 그 아래에 있는 트랜스포트 계층에서는 위에서 받은 HTTP 메시지를 쉽게 조각내고 안내 **안내 번호와 포트 번호**를 붙여 네트워크 계층에 전달  
3. 네트워크 계층(IP)에서는 수신지 MAC 주소를 추가해 링크 계층에 전달. (여기까지 캡슐화) 
4. 서버는 링크 계층에서 데이터를 받아들여 순서대로 위의 계층에 전달  
5. 서버 어플리케이션 게층은 HTTP 리퀘스트 내용을 수신하고 Response를 보낸다.  

### 1.3 IP/TCP/DNS  

#### 1.3.1 IP  
- IP주소와 MAC 주소를 통해 개개의 패킷을 상대방에게 전달하는 프로토콜.  
- IP 주소는 각 노드에 부여된 주소, MAC 주소는 NIC에 할당된 고유의 주소. IP 주소는 변경이 가능하지만 MAC 주소는 변경이 불가능하다.  
- ARP (Address Resolution Protocol)을 사용해 IP 주소를 바탕으로 보낼 MAC 주소를 조사.  

#### 1.3.2 TCP  
- 신뢰성 있는 데이터 전송 서비스를 제공.  
- 데이터를 확실하게 보내기 위해 **3 way handshaking** 사용.  
<details>
<summary>3 way handshaking</summary>  
</br>
<p> - 송신측에서 수신측에 접속함과 동시에 SYN 플래그를 보내면, 수신측에서는 송신측으로 접속과 동시에 SYN/ACK 플래그로 패킷을 수신했다고 알린다. 마지막으로 송신측에서 ACK 플래그를 보냄으로 패킷 교환이 완료되었음을 알림 </p>    
</details>

#### 1.3.3 DNS  
- 도메인 이름과 IP 주소 이름 확인을 제공하는 프로토콜  
- 주로 사용하는 IP 주소 대신 이름을 이용해 상대의 컴퓨터를 지정.  
- 컴퓨터가 주로 사용하는 IP 주소 대신 인간에게 친숙한 영어나 숫자 등으로 표기하기 위함.  

<details>
<summary>DNS의 동작</summary>  
</br>
<p> 1. 송신 측에서 도메인 명을 통해 hackr.kr 웹 페이지에 접속 요청 </p>
<p> 2. DNS는 도메인 명을 받아 hackr.kr IP 주소를 송신 측에 전달 </p>
<p> 3. DNS에서 받은 IP 주소를 통해 hackr.kr 웹 페이지에 접속 </p>
</details>

### 1.4 URI와 URL  
- URI(Uniform Resource Identifier) : 인터넷상 표현할수 있는 모든 리소스를 의미. (URL, URN)
- URL(Uniform Resource Locator) : URI에서 네트워크상 경로, 어떤 자원의 위치에 대한 절대경로값을 지닌 문자열를 의미.
- URN은 거의 쓰지 않아 보통 URI = URL이라 생각하면 됨.  

<details>
  <summary>URL 포맷</summary>

### http://user:pass@www.example.kr:80/dir/index.htm?uid=1#ch1  

1. 스키마 (http:): http:, data: 같은 스키마를 사용해 **리소스를 얻기 위해 사용하는 프로토콜을 지시**  
2. 자격정보 (user:pass) : 서버로부터 리소스를 취득하기 위해 유저명과 패스워드를 지정. (Optional)  
3. 서버 주소(www.example.kr) : DNS 이름이나 IP 주소  
4. 서버 포트 (80) : 서버의 접속 대상이 되는 네트워크 포트 번호 지정 (Optional, Default=80)  
5. 계층적 파일 경로 (dir/index.htm) : 특정 리소스를 식별하기 위해 서버 상의 파일 패스를 지정. UNIX의 디렉토리 지정 방식과 비슷.  
6. 쿼리 문자열 (uid=1) : 파일 경로에 지정된 리소스에 파라미터를 넘겨주기 위해 사용. (Optional)  
7. 프레그멘트 식별자 (ch1) : 얻은 리소스에서 서브 리소스를 가리키기 위해 사용 (Optional)  

</details> 

## 2. HTTP의 특징  

### 2-1. HTTP는 클라이언트와 서버 간에 통신을 한다.  
- 텍스트, 이미지 등과 같은 리소스를 요구하는 쪽이 클라이언트가 되고, 이러한 리소스를 제공하는 쪽이 서버.  

### 2-2. 리퀘스트와 리스폰스를 교환하여 성립  
- HTTP는 클라이언트가 Request 메시지를 송신되며, 그 결과는 서버로부터 Response 메시지로 되돌아옴.  
- 반드시 클라이언트 측으로부터 통신이 먼저 시작된다.  

### 2-3. HTTP는 상태를 유지하지 않는 프로토콜 (Stateless)  
- HTTP는 상태를 계속 유지하지 않는 Stateless 프로토콜  
- 이전에 보냈던 Request나 Response에 대해서 전혀 기억하지 않음.  
- 서버, CPU, 메모리 같은 자원 절약  
- HTTP/1.1에서 로그인 같이 상태를 계속 유지해야하는 특성에 대해 쿠키(Cookie)라는 기술이 도입.  

### 2-4. Request URI로 리소스를 식별  
- HTTP는 URI를 사용해 인터넷 상의 리소스를 지정.  
- 클라이언트는 리소스를 호출할 때 Request 메시지 안에 URI를 포함해야 한다.  

### 2-5 HTTP 메소드  
1. GET: 서버에 리퀘스트 URI로 식별된 리소스를 가져올 수 있도록 요구  
2. POST : 서버에 엔티티를 전송하기 위한 메소드  
3. PUT : 서버에 파일을 전송하기 위해서 사용. 인증 없이 눈구든지 파일 업로드가 가능해 보안 상의 문제 존재  
4. HEAD : GET과 같은 기능이지만 메시지 바디는 돌려주지 않음. URI 유효성과 리소스 갱신 시간을 확인하는 목적으로 사용.  
5. DELETE : 파일을 삭제하기 위해 사용.  


<details>
  <summary>GET, POST</summary>

  ### 1. GET  
  - Request Message  
  GET /index.html HTTP /1.1  
  Host : www.hackr.kr  
  if-Modified-Since : Thu. 12 Jul 2012 07:30:0 GMT  
  
  - Response Message  
  index.html 리소스가 2012년 7월 12일 7시 30분 이후에 갱신된 경우에만 리퀘스트 URI에 있는 index.html을 보낸다.  
  이외에는 304 Not Modified Response를 보낸다.  

  
  ### 2. POST  
  - Request Message  
  POST /submit.cgi HTTP /1.1  
  Host : www.hackr.jp  
  Content-Length: 1560 (1560바이트 데이터)  
  
  - Response Message  
  submit.cgi가 수신한 데이터의 처리한 결과를 돌려준다.  
  

</details> 

### 2-6 지속 연결로 접속량을 절약  
- HTTP 발전에 따라 리퀘스트의 송신도 나날이 늘어남. 예를 들어 하나의 html에 여러 이미지가 포함되어 있는 경우 HTML 문서에 있는 이미지를 획득할 때 마다 Request 메시지를 송신. 이는 **매번 TCP 연결과 종료를 하게 되어 Overhead가 증가.**  

#### 2-6-1. 지속 연결  
- 어느 한 쪽이 명시적으로 연결을 종료하지 않는 이상 TCP 연결을 계속 유지  
- HTTP/1.1에서 표준 동작  
- 서버는 데이터를 HTML에 있는 데이터를 다 보내면 **4 wawys handshaking으로 연결을 종료**  

#### 2-6-2. 파이프라인  
- 이전에는 Request 송신 후에 Response를 수신할 때 까지 기다리는 것이 아니라, 기다리지 않고 바로 다음 Request 메시지를 서버에 보내는 방식.  

### 2-7 쿠키를 사용한 상태 관리  
- HTTP는 **Stateles Protocol** -> 과거에 교환한 Response와 Request를 관리하지 않음.  
- 과거 상태를 바탕으로 현재 Request(로그인, 인증 등)를 처리하기 위해 쿠키(Cookie)라는 시스템이 도입  

<details>
<summary>쿠키의 동작 방식</summary>  
</br>
1. 최초로 클라이언트가 서버에게 Request 메시지 송신.  
2. 서버는 Response 메시지에 있는 Set-Cookie라는 헤더에 쿠키를 붙여서 클라이언트에게 송신.  
3. 이후 클라이언트는 Request 메시지에 쿠키를 붙여서 서버에 송신.  
</details>

<details>
<summary>1.1 HTTP</summary>  
</br>
<p> - 웹 서버와 웹 클라이언트가 데이터를 주고 받을 수 있는 프로토콜</p>  
<p> - 처음 나올 당시에는 주로 텍스트를 전송. 지금은 그림 동영상 뿐 아니라 웹이라는 틀을 넘어 다양하게 사용되고 있음.</p>    
</details>
