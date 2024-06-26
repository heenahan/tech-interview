## 1. 쿠키와 세션의 차이에 대해 설명해주세요.
### 쿠키
클라이언트에 저장되는 key-value 형태의 작은 데이터 파일이다. 웹 사이트 재방문 시 효율적으로 서비스를 제공하기 위해 사용한다.

특징
- 브라우저 단위로 생성
- 다른 도메인을 대신하여 쿠키 발급 불가
- 만료 시간까지 상태 정보 유지

쿠키 탈취 시 쿠키의 값을 임의로 바꿀 수 있고 대신 로그인 할 수 있다.
### 세션
웹 사이트에 이용되는 사용자 정보를 서버에 저장하는 방법이다. 쿠키 + 세션 사용 시, 쿠키에 sessionId 외의 정보를 기록하지 않음으로써 안전성을 확보한다.

단점
- 유저 정보가 서버에 있기 때문에 처리 속도에 대한 비용이 발생한다.
- 서버 자원을 사용하기 때문에 유저가 많아지면 저장 공간에 대한 비용 발생
## 2. HTTP 응답코드에 대해 설명해 주세요.
**1xx(정보)**, 요청을 받았으며 프로세스를 계속 처리 중이다.

**2xx(성공)**, 요청을 성공적으로 처리했다.
- 200 OK 요청을 성공했다.
- 201 Created 요청 성공해서 새로운 리소스가 생성되었다. 주로 POST, PUT 요청 이후에 따라온다.
- 202 Accepted, 요청을 수신했지만 아직 처리가 완료되지 않았다. 예를 들어, 요청 접수 후에 서버에서 1시간 뒤에 배치 프로세스가 요청을 처리한다.
- 204 No Content, 요청을 성공했지만 응답 페이로드 본문에 보낼 데이터가 없다.

**3xx(리다이렉션)**, 요청 완료를 위해 웹 브라우저에서 추가 작업 조치가 필요하다. 웹 브라우저는 3xx 응답의 결과에 Location 헤더가 있으면 Location 위치로 자동 이동한다. 
- 영구적인 리다이렉션, 특정 리소스의 URI가 영구적으로 이동한다. 301(Moved Permanently), 308(Permanent Redirect)
- 일시적인 리다이렉션, 일시적인 변경이다. 302(Found), 303(See Other), 307(Temporary Redirect)
- 특수한 리다이렉션, 결과 대신 캐시를 사용한다. 304(Not Modified)

**4xx(클라이언트 오류)**, 요청의 문법이 잘못되었거나 요청을 처리할 수 없다.
- 400(Bad Request), 잘못된 문법이나 메시지를 요청해서 서버가 이해할 수 없다.
- 401(Unauthorization), 클라이언트가 해당 리소스에 대한 인증이 필요하다. 예를 들어 로그인이다.
- 403(Forbidden), 서버가 요청을 이해했지만 승인을 거부했다. 인증, 즉 로그인은 되었지만
접근이 불충한 경우이다.
- 404(Not Found), 요청 리소스를 찾을 수 없다.

**5xx(서버 오류)**, 서버가 정상 요청을 처리하지 못했다.
- 500(Internal Server Error), 서버 내부 문제로 오류가 발생했다.
- 502(Bad Gateway), 서버 간 유효하지 않은 응답을 받았다.
- 503(Service Unavaliable), 서버가 일시적으로 요청을 처리할 준비가 되지 않았다. 유지보수를 위한 작동이 중단되거나 과부하가 걸렸다.
## 3. HTTP Method 에 대해 설명해 주세요.
GET, 리소스를 조회한다.

POST, 요청 데이터를 처리하며 주로 등록에 사용된다. 헤더에 신규 리소스 주소인 Location이 포함된다.

PUT, 리소스를 완전히 대체하고 해당 리소스가 없으면 생성한다.

PATCH, 리소스를 부분 변경한다.

DELETE, 리소스를 삭제한다.

HEAD, 데이터는 받지 않고 Header만 받는다.

HTTP 메서드는 3가지 속성이 있다. 
- 안전한 메서드(Safe Methods)
    - 메서드를 호출해도 리소스를 변경하지 않는다는 특성이다. 즉, 서버에 데이터를 변경하지 않는 요청 메서드로 GET이 해당된다.
- 멱등성(Idempotent Methods)
    - 연산을 여러 번 적용하더라도 결과가 달라지지 않는 성질을 말한다.
    - GET은 멱등이고 안전한다.
    - PUT, DELETE는 멱등이지만 안전하지 않다.
    - POST, PATCH는 멱등이지도 안전하지도 않다.
    - 참고로 PATCH는 멱등으로 설계할 수도 멱등이 아니게 설계할 수도 있다. PATCH 요청할 때마다 like를 1씩 더하는 메서드를 설계한다면 멱등이 아니다.
- 캐싱 가능(Cacheable Methods)
    - 응답 결과를 서버에 캐싱해서 사용해도 되는 메서드를 의미한다. 
    - 캐싱을 해서 데이터를 효율적으로 가져올 수 있다. GET, HEAD, POST, PATCH가 가능하지만 일반적으로 GET, HEAD 정도만 캐싱한다.
## 4. HTTP에 대해 설명해 주세요.
Hypertext Protocol, 서버 - 클라이언트 간의 메시지 교환 프로토콜이다.
### Request 구조
![Request](https://github.com/heenahan/tech-interview/assets/83766322/17a968fd-9103-4ed0-ac0e-22ace49a7c77)
- start line 
메서드, URI, 프로토콜 버전
- headers
- 공백 라인
- 바디
### Response 구조
![Response](https://github.com/heenahan/tech-interview/assets/83766322/b4a36997-144f-440a-808c-2695cb4489f4)
- status line
프로토콜 버전, 상태 코드, 상태 코드 설명
- headers
- 공백 라인
- 바디
HTTP의 특징은 
- Stateless 상태 없음
과거 정보를 남기지 않고 새로운 Request를 보낼 때마다 새로운 Response를 보낸다. 상태와 무관하니 확장이 쉽다.
- URI로 리소스를 식별
Request에서 URI로 리소스를 식별한다.
- 지속 연결
초기 HTTP는 비지속 연결을 사용했다. 요청을 주고 받을 때마다 새로운 TCP 커넥션을 연결하고 종료했다.
주고 받을 데이터가 많아지면서 매번 TCP 연결과 종료를 하니 자원 낭비가 있고 속도가 느려졌다. 그래서 지속 연결을 통해 통신을 좀 더 빠르게 했다. 
## 5. 웹소켓과 소켓 통신의 차이에 대해 설명해 주세요.
**소켓**은 OS 커널에 구현되어 있는 프로토콜 요소에 대한 **추상화된 인터페이스**이다. 장치 파일의 일종으로 일반 파일에 대한 개념이 대부분 적용된다. 소켓은 파일이라고 생각해야 한다.
소켓 프로그래밍은 TCP 소켓을 이야기하며 TCP 대상을 추상화시킨 파일에 대한 입출력 방법론이다. 주체인 Process가 TCP 소켓을 Open, Create, Close, Delete가 가능한데 Write는 송신, Read는 수신한다고 한다.
**웹소켓**은 소켓처럼 IP, Port 통신을 한다. 웹 브라우저는 HTTP 프로토콜을 사용하는데 요청을 보내면 응답이 오는 단방향적 구조로 통신한다. 그렇기 때문에 TCP/IP 프로토콜을 사용하는 소켓처럼 계속 connection이 유지되는 실시간 통신을 할 수 없다. 이런 실시간 통신의 문제점을 해결하기 위해 웹소켓 프로토콜이 등장했다. 웹 소켓을 사용하면 웹 브라우저에서도 소켓 통신을 하는 것처럼 실시간으로 데이터를 주고받을 수 있다.
## 6. HTTP/1.1과 HTTP/2의 차이점은 무엇인가요?
**HTTP/1.1**는 하나의 TCP 연결을 재사용해 많은 콘텐츠를 제공할 수 있는 지속적 연결 기술(keep alive)가 추가되었다.
HTTP1.1의 또 다른 특징 중 하나는 파이프라이닝 기술이다. 파이프라이닝은 브라우저가 웹 서버에 여러 개의 콘텐츠를 요청했을 때, 이전 요청에 대한 응답을 완전하게 받지 않더라도 하나의 connection 내에서 미리 다음 요청을 전달하면서 전체적인 전달 시간을 줄인다.
![HTTP/1.1](https://github.com/heenahan/tech-interview/assets/83766322/2c4e054a-863a-4105-8c90-181925800097)
HTTP/1.1은 단점은 다음과 같다.
- HOL(Head Of Line) Blocking 
특정 응답의 지연이 발생한다. Connection을 통해서 다수개의 파일을 요청받을 때 첫번째 요청의 응답이 지연되면 뒤의 요청의 응답이 함께 지연된다.
- 무거운 Header 구조
HTTP/1.1의 헤더에는 많은 메타정보를 저장한다. 매 요청마다 중복된 Header 값을 전송하게 된다.
**HTTP/2**는 이러한 HTTP/1.1의 단점을 여러가지 방법으로 극복했다.
- Binary Framing
HTTP/1.1에서 text 형식으로 전달되던 요청, 응답 메시지를 **프레임 단위**로 나누고 바이너리 형식으로 인코딩했다. 바이너리는 컴퓨터가 더 이해하기 쉬워 파싱, 전송 속도가 빨라진다.
- Multiplex Streaming
TCP 연결한 뒤 스트림을 생성할 수 있다. 스트림은 파이프와 다르게 양방향 데이터 흐름이 가능하고 각 스트림에는 고유 식별자와 우선순위 정보가 있다. 
HTTP 메시지는 하나 이상의 프레임으로 구성되는데, 프레임을 전달받은 쪽에서 프레임의 헤더에 있는 스트림 식별자를 통해 재조립하여 요청과 응답 메시지를 확인할 수 있다.
- 헤더 압축 
HPACK 압축 형식을 사용하여 요청 및 응답 헤더 메타데이터를 압축한다.
- Server Push
클라이언트가 요청한 리소스에 연관된 다른 리소스들을 함께 push할 수 있다. 이를 통해 클라이언트의 요청을 최소화하여 성능을 향상시킨다.
## 7. TCP와 UDP의 차이에 대해 설명해 주세요.
### Transport Layer
end point간 **신뢰성**있는 데이터 **전송**을 담당하는 계층이다.

데이터를 순차적이고 안정적인 전달한다. ➡️ 신뢰성

포트 번호에 해당하는 프로세스에 데이터를 전달한다. ➡️ 전송
## TCP(Transmission Control Protocol)
신뢰성있는 데이터 통신을 가능하게 해주는 프로토콜

- 특징
    - 양방향 통신 ➡️ connection 연결(3 way-handshake)
    - 데이터의 순차 전송을 보장한다.
    - 흐름 제어 ➡️ 수신자가 처리할 수 있는 데이터량을 초과할 때 발생하는 송수신간의 데이터 처리 속도의 차이 문제를 해결
    - 혼잡 제어 ➡️ 네트워크가 혼잡할 때 제어
    - 오류 감지 
- 세그먼트(Segment), TCP의 PDU
    - Appilcation Layer에서 내려온 데이터를 자른 뒤 데이터 앞에 TCP 헤더를 붙인다.
- TCP 헤더
    - 시퀀스 번호, 현재 데이터의 첫 번째 위치가 전체 송신 데이터에 몇 번째 위치임을 나타내는 일련번호
    - SYN, 송신측과 수신측에서 시퀀스 번호를 공유함을 나타냄
    - ACK, 수신 데이터의 시퀀스 번호가 유효함
    - FIN, 연결 끊기를 나타냄

TCP는 전송의 신뢰성은 보장하지만 매번 connection을 연결해서 시간 손실이 발생한다. 패킷을 조금만 손실해도 재전송한다.
### UDP (User Datagram Protocol)
TCP보다 신뢰성이 떨어지지만 전송 속도가 일반적으로 빠른 프로토콜 (순차 전송❌, 흐름 제어❌, 혼잡 제어❌)

- 특징
    - 비연결성 (3 way-handshake ❌)
    - 오류 감지 (UDP 헤더의 checksum)
    - 영상 스트리밍처럼 비교적 데이터의 신뢰성이 중요하지 않을 때 사용
- User Datagram, UDP의 PDU
    - TCP와 달리 Appilcation Layer에서 내려온 데이터를 자르지 않는다. 전체 데이터 앞에 TCP 헤더를 붙인다.
### 왜 배울까?
- TCP, UDP 특성을 파악하고 상황에 따라 적절한 프로토콜을 사용한다.
- TCP, UDP 헤더에 대해 파악하고 성능 개선에 이용한다.
## 8. DHCP가 무엇인지 설명해 주세요.
DHCP(Dynamic Host Configuration Protocol)은 동적으로 호스트를 설정하는 규약이다.

네트워크 안의 컴퓨터에 자동으로 네임 서버 주소, IP 주소, 게이트웨이 주소를 할당해주는 것을 의미하고 해당 클라이언트에게 일정 기간 임대를 하는 동적 주소 할당 프로토콜이다. 

공유기에 노트북을 LAN으로 연결하면 자동으로 DHCP 클라이언트의 MAC 주소가 DHCP 서버에게 IP 주소를 요청한다. DHCP 서버는 DHCP 클라이언트에게 사용 가능한 IP를 자동으로 할당한다. 단, DHCP를 통해 할당 받은 IP 주소는 영구적인 것이 아니다. 할당 받은 IP 주소를 사용하다가 임대 시간이 지나면 기간을 연장하거나 IP 주소를 반납한다.

이 IP 설정 과정은 매우 복합한데, 라우터나 장치에 내장된 DHCP 기술 덕분에 이 과정이 자동으로 진행되어 편리하다.
## 9. IP 주소는 무엇이며, 어떤 기능을 하고 있나요?
IP(internet protocol)는 인터넷에 연결되어 있는 모든 장치들을 식별할 수 있도록 각각의 장비에게 부여되는 고유 주소이다.

### IPV4, IPV6
## 10. OSI 7계층에 대해 설명해 주세요.
![osi 7 layer](https://github.com/heenahan/tech-interview/assets/83766322/052c7b3f-70c3-4084-8264-23ec138a22ab)

1. 물리 계층(Physical layer)
    - 전기적 신호가 나가는 물리적인 장비
    - 단지 데이터를 전달할 뿐, 송신하거나 수신하려는 데이터가 무엇인지 어떤 에러가 있는지 등에 대해서는 신경쓰지 않는다.
    - 데이터를 전기적인 신호로 변환해서 주고받음
    - 장비 : 케이블, 허브, 리피터
2. 데이터 링크 계층(Data link layer)
    - 물리 계층을 통해 송수신되는 정보의 오류와 흐름을 관리하여 안전한 정보의 전달을 수행할 수 있도록 도와준다. 따라서 통신에서 오류도 찾아주고 재전송하는 기능을 가지고 있다.
    - 이 계층에서는 Mac 주소를 가지고 통신한다.
    - 데이터 링크 계층은 포인트 투 포인트(Point to Point)간 신뢰성 있는 전송을 보장하기 위한 계층으로 CRC 기반의 오류 제어와 흐름 제어가 필요하다.
    - 장비 : 브릿지, 스위치, 이더넷
3. 네트워크 계층(Network layer)
    - 경로(Route)와 주소(IP)를 정하고 패킷을 전달한다.
    - 목적지까지 가장 안전하고 빠르게 데이터를 보내는 기능을 말한다. 
    - 따라서 최적의 경로를 설정해야하며 이런 라우팅 기능을 맡고 있다.
4. 전송 계층(Transport layer)
    - 양 끝단의 사용자들 간의 신뢰성 있는 데이터를 주고 받게 해준다.
    - 송신자와 수신자 간의 신뢰성있고 효율적인 데이터를 전송하기 위해 **오류 검출 및 복구, 흐름제어와 중복검사 등을 수행**한다.
5. 세션 계층(Session layer)
6. 표현 계층(Presentaion layer)
    - 전송하는 **데이터의 표현 방식**을 결정한다. 예를 들어, 데이터 변환, 압축, 암호화 등이 있다.
    - GIF, JPEG, ASCII 등
7. 응용 계층(Application layer)
    - HTTP, FTP 등의 프로토콜이 속한다.

## 11. 3-Way Handshake에 대해 설명해 주세요.
TCP가 connection을 수립하는 과정이다.

![3 way handshake](https://github.com/heenahan/tech-interview/assets/83766322/01894539-15d2-4347-800a-2888d9fe5acd)


1. 클라이언트가 SYN 비트를 1로 설정해 패킷을 송신한다.
2. 서버가 SYN, ACK 비트를 1로 설정해 패킷을 송신한다.
3. ACK 비트를 1로 설정해 패킷을 송신한다.

connection 연결 후 데이터를 전송할 때 다음과 같은 과정을 거친다.
1. 클라이언트가 패킷을 전송한다.
2. 서버에서 ACK를 송신한다.
3. ACK를 수신하지 못하면 재전송한다.
## 12. 4-Way Handshake에 대해 설명해 주세요
TCP가 connection을 끊는 과정이다.

![4 way handshake](https://github.com/heenahan/tech-interview/assets/83766322/47b989c0-3b67-4726-b800-a24828912620)

1. 데이터를 전부 송신한 클라이언트가 FIN을 송신한다.
2. 서버가 ACK를 송신한다.
3. TIME_WAIT, 일정 시간 대기가 되는데 서버에서 남은 패킷을 송신한다.
4. 서버가 FIN을 송신한다.
5. 클라이언트가 ACK를 송신한다.
## 13. www.github.com을 브라우저에 입력하고 엔터를 쳤을 때, 네트워크 상 어떤 일이 일어나는지 최대한 자세하게 설명해 주세요.
1. 브라우저 캐시 체크

기존에 google.com에 방문했다면 구글에 빠르게 접근할 수 있는 내용이 담겨있는 **브라우저 캐시**를 읽는다. 브라우저 캐시에서 찾을 수 없다면 **OS 캐시**를 찾는다. 운영체제 안에 있는 캐시로 systemcall을 통해 내용에 접근할 수 있다. 세번 째로 **라우터 캐시**를 읽는다. 라우터는 집에서 사용하는 공유기로 DNS의 내용을 저장한다. 마지막으로 **ISP(Internet Service Provider) 캐시**를 확인한다. ISP는 인터넷을 제공하는 통신사를 생각하면 된다.

2. DNS로 IP 주소 획득

ISP 캐시에서 IP 주소를 찾을 수 없다면, ISP의 name server에 DNS 쿼리를 보낸다. 이때 Recursive search를 진행하고 이러한 탐색을 ISP의 DNS recursor가 담당한다. 

3. 브라우저가 TCP/IP 프로토콜을 사용하 서버에 연결

IP 주소를 알게 되어 TCP를 사용해 서버에 연결을 하기 위해 신호를 보낸다. TCP는 데이터를 잃지 않고 잘 보내는 방법을 담당하고 IP는 주소에 맞게 잘 보내는 방법을 담당한다. TCP 연결을 위해 3 way handshaking을 진행하여 클라이언트와 서버가 안전하게 연결한다.

4. Firewall & Https/SSL

TCP 연결 중 Firewall과 Https/SSL를 이용해 접근을 제한한다. Firewall을 설치해 특정 IP 주소나 어떤 지역에서 접근해 오는 신호를 차단한다. Https/SSL은 클라이언트와 서버와의 암호화를 통해 중간에 누가 패킷을 엿듣는 것을 차단한다.

5. Load Balancer

트래픽을 측정하여 여러 대의 서버 중 트래픽을 받을 수 있는 서버에게 전달한다. 트래픽이 망가지거나 지연되지 않도록 도와준다.

6. 웹서버

TCP 연결이 된 후 클라이언트는 데이터를 보낸다. 브라우저 버전과 종류, 쿠키 등의 내용과 함께 HTTP 코드를 통해 성공 아니면 실패를 알 수 있다.

7. HTML 컨텐트 렌더링

브라우저는 서버로부터 받은 HTTP 코드와 HTML을 통해 렌더링을 시작한다. 필요한 이미지나 다른 파일들이 있으면 보내달라고 요청한다.

## 14. DNS에 대해 설명해 주세요.
DNS, Domain Name System은 도메인 이름과 IP 주소에 대한 정보를 관리하는 시스템이다. DNS는 도메인 이름을 IP 주소로 변환해준다. 즉, 의미있는 문자열로 IP 주소로 추상화하여 인터넷 사용자는 IP 주소를 몰라도 된다. 

하나의 서버에서 전 세계 모든 DNS 정보를 관리한다는 것은 단일 장애 지점이 될 수 있다. 따라서 DNS는 도메인을 **계층적으로 관리**하여 트래픽과 데이터를 분산한다. 

www.google.com.이라는 도메인이 있고 계층 구조로 나타내면 다음과 같다. 루트 도메인은 .으로 생략된다. 다음 com은 Top Level Domain(TLD)라고 한다. TLD 아래, google과 www는 모두 Sub Domain이라 부른다. 

상위 서버는 하위 서버의 주소를 알고 있으며 상위에서 하위로 이동하며 원하는 도메인에 도착한다. 이 서버들은 네임 서버(Name Server)라고 부르면서 다양한 기관에서 관리한다. Root 네임서버는 ICANN(국제 인터넷 주소 관리기구), TLD 네임서버는 도메인 등록 기관(Registry), Sub Domain 네임서버는 가비아나 Route53과 같은 도메인 판매업체(Register)가 관리한다.

위 세 네임서버는 DNS 정보를 가지고 있어 권한 있는 네임서버라고 부른다. 반대로 DNS 정보를 가지고 있지 않는 **로컬 DNS 서버**는 권한이 없는 네임서버라 부른다. 로컬 DNS 서버는 ISP를 제공하는 KT, SKT, LG와 같은 통신사가 관리한다.

### DNS 동작 순서 

1. 브라우저 캐시를 확인
2. hosts 파일과 DNS 캐시를 확인
3. 로컬 DNS 서버에게 질의
4. 로컬 DNS 서버에 캐싱되어 있지 않으면 로컬 DNS 서버는 루트 DNS 서버에 질의
5. 못찾았다는 응답이 오면 로컬 DNS 서버는 TLD DNS 서버에 질의
6. 못찾았다는 응답이 오면 로컬 DNS 서버는 Sub DNS 서버에 질의
7. 수신 받은 IP 주소를 캐싱하고 IP 주소를 단말에 전달

PC는 로컬 DNS 서버를 통해 받아온 IP 주소를 캐시한다. 이것을 **DNS 캐시**라 한다.

### DNS 레코드
DNS 레코드는 DNS 서버가 패킷을 받았을 때 어떤 식으로 처리할지를 나타내는 지침이다. 즉, DNS 상에서 도메인에 관한 설정을 하기 위해 사용되는 일련의 설정 문자이다.

- A 레코드
    - 도메인 주소와 서버의 IP 주소와 직접 매핑한다.
    - 매핑 설정에 따라 일대다, 다대일도 가능하다.
- CNAME (Canonical Name Record)
    - 도메인 별명 레코드라고도 부르며, 도메인 주소를 또 다른 도메인 주소로 이중 매핑 시킨다.
    - google.com이라는 도메인의 CNAME을 google2.com으로 정한다는 예시가 있다. 브라우저에 google2.com으로 입력하면 google.com으로 접근된다.
- AAAA
    - A 레코드의 IPv6 버전으로 도메인에 IPv6 주소가 매핑되어 있는 레코드이다.

**A 레코드 vs CNAME**

A 레코드는 도메인이 바뀌어도 IP는 그대로 이므로 유지가 된다. 하지만 서버 이전 등의 문제로 IP가 변동될 시 일일히 변경해야 한다.

CNAME은 서버 이전 등의 문제로 IP가 변동될 시 변경하지 않아도 된다. 반대로 도메인이 바뀌면 변경해야 한다. 그리고 실제 IP 주소를 얻을 때까지 여러번 DNS 정보를 요청해서 성능저하가 일어난다.
## 15. SOP 정책에 대해 설명해 주세요.
**Origin**은 URL에서 프로토콜 + 호스트 + 포트를 뜻한다.  

**SOP(Same-Origin Policy)**는 동일한 출처에서만 리소스를 공유할 수 있다는 **브라우저 정책**이다. 즉, 동일 출처(Same-Origin) 서버⸺프로토콜 + 호스트 + 포트 모두 동일⸺에 있는 리소스는 자유로이 가져올 수 있지만 다른 출처(Cross-Origin) 서버에 있는 리소스는 상호 작용이 불가능하다. 동일 출처 정책을 통해 CSRF, XSS 등의 공격을 막을 수 있다.

반대로 CORS(Cross-Origin Resource Sharing)은 다른 출처의 리소스를 허용하는 정책이다.

### CORS 작동 방식
- 단순 요청(Simple Request)
    - 예비 요청 생략하고 본 요청 바로 보낸다.
    - 본 요청에 대한 응답의 헤더의 Acess-Control-Allow-Origin을 비교하여 CORS 정책 위반 여부를 확인한다.
    - 조건이 까다로워 단순 요청이 일어나는 상황은 드물다.
- 예비 요청(Preflight Request)
    - 먼저 브라우저는 Origin 헤더에 자신의 출처를 넣어 서버에 예비 요청을 보낸다. 예비 요청의 HTTP 메서드는 OPTIONS이다. 
    - Origin 헤더의 출처와 응답의 Access-Control-Allow-Origin 헤더의 출처와 비교하여 안전한 요청인이 확인한다.
    - 안전한 요청이면 본 요청을 보낸다.
- 인증된 요청(Credentialed Request)
    - 클라이언트에서 자격 인증 정보(Credential)를 실어 요청할 때 사용
    - 쟈격 인증 정보는 쿠키 혹은 Authorization 헤더이다.
    - 일반적인 CORS 요청과는 다르게 대응된다.
        - 응답 헤더의 Access-Control-Allow-Crendtial를 true로 설정해야 한다.
        - 응답 헤더의 Access-Control-Allow-Origin에 와일드카드(*)를 사용할 수 없다.
        - 응답 헤더의 Access-Control-Allow-Methods에 와일드카드(*)를 사용할 수 없다.
        - 응답 헤더의 Access-Control-Allow-Headers에 와일드카드(*)를 사용할 수 없다.
## 16. Stateless와 Connectionless에 대해 설명해 주세요.
**Stateful(상태 유지)**는 서버가 클라이언트의 상태를 보존함을 의미한다. TCP는 대표적인 Stateful한 프로토콜이다. TCP는 3-way handshake과정에서 세션 상태에 따라 서버의 응답이 달라져 stateful하다고 할 수 있다. 하지만 Stateful은 서버에 장애가 발생해 멈추게 되어 다른 서버를 사용해야 하거나 서버가 여러개 운영될 때 문제가 발생한다. 새로운 서버는 이전 서버에서 가지고 있는 상태값들을 가지고 있지 않다. 그래서 클라이언트는 처음부터 다시 일을 해야한다.
> 현업에서는 클라이언트의 상태 데이터를 따로 캐시 서버(Redis)에 저장하여 이용한다.

**Stateless(무상태)**는 서버가 클라이언트의 상태를 보존하지 않음을 의미한다. Stateless 구조에서 서버는 단순히 요청이 오면 응답을 보내는 역할만 수행하며, 상태 관리는 전적으로 클라이언트에게 책임이 있다. 즉, 통신에 필요한 모든 상태 정보들은 클라이언트에서 가지고 있다가 서버와 통신할 때 데이터를 실어 보낸다. 

대표적인 Stateless한 프로토콜은 HTTP와 UDP이다. UDP는 TCP와 달리 handshaking 과정이 없고 세션 상태에 관계 없이 데이터를 전송한다. Stateless는 Scale Out에 용이하지만 Stateful보다 상대적으로 더 많은 데이터가 소모된다. 왜냐하면 매번 요청할때마다 브라우저는 자신의 정보를 줘야하기 때문이다.
## 17. 라우터 내의 포워딩 과정에 대해 설명해 주세요.
라우팅과 포워딩은 **네트워크 레이어**에서 수행하며 네트워크 레이어 장비인 라우더(Router)가 가진 기능이다.

**라우팅**은 패킷 단위로 출발지부터 목적지까지 경로를 설정한다. 네비게이션 역할을 하며, 최단 거리를 찾는 알고리즘을 사용한다. 데이터를 전송하는 과정에서 라우팅이 잘못되면 포워딩도 불완전해지기 때문에 라우터의 역할이 중요하다.

**포워딩**은 라우터의 입력 포트에서 출력 포트로 패킷을 이동시키는 것을 뜻한다. 스위칭(switching)으로도 불린다.

라우팅 알고리즘에 의해 포워딩 테이블이 만들어진다. 패킷은 라우팅 알고리즘을 통해 만들어진 포워딩 테이블을 연속적으로 참조하여 출발지에서 목적지까지 운반된다.
## 18. 로드밸런서가 무엇인가요?
프록시(Proxy)는 대리를 뜻하며, 결국 프록시 서버는 클라이언트와 서버 간의 중계 서버로 통신을 대리 수행하는 서버이다. 프록시 서버는 Forward Proxy와 Reverse Proxy로 나뉜다.

- Froward Proxy
    - 클라이언트 바로 뒤에 위치한다. 클라이언트에게 Response를 밀어준다.
    - 같은 내부망에 존재하는 클라이언트의 요청을 받아 인터넷을 통해 외부 서버에서 데이터를 가져와 클라이언트에게 응답한다.
    - 캐싱
        - 페이지 캐싱하여 부하를 줄인다.
    - 암호화
        - 클라이언트의 IP를 감춰준다.
- Reverse Proxy
    - 웹 서버와 WAS 앞에 놓여 있다. 서버에게 Request를 밀어준다.
    - 캐싱
    - 보안
        - 서버의 IP 주소를 노출시키지 않아 DDos 공격을 막을 수 있다.
   - 로드 밸런싱(Load Balancing)
        - scale out한 서버에서 부하를 분산한다.
### 로드 밸런싱 알고리즘
- 라운드 로빈
    - 클라이언트의 요청을 여러 대의 서버에 순차적으로 배분
    - 들어온 요청을 빠르게 서버에 분산해 전송
    - 가장 많이 사용되며 모든 서버의 스팩이 동일하거나 비슷한 경우 사용
- 가중 라운드 로빈
    - 각 서버에 처리량(가중치)를 지정한 후, 가중치가 높은 서버에 클라이언트 요청을 우선적으로 전달
    - 특정 서버의 사양이 더 좋을 경우 사용
### 로드 밸런서 종류
OSI 7 layer를 기준으로 부하를 어떻게 분산할지 종류가 나뉜다. L2, L3, L4, L7이 있고 L4, L7 로드 밸런서가 가장 많이 사용된다.

- L4 로드 밸런서
    - IP 주소와 포트 번호를 로드 밸런싱에 사용
    - 한 대의 서버에 다른 포트 번호를 부여하여 다수의 서버 프로그램을 운영하는 경우, L4 로드 밸런서를 사용해야한다.
- L7 로드 밸런서
    - URL, HTTP 헤더와 쿠기와 같은 사용자의 요청을 기준으로 트래픽을 분산
    - 서버의 응답을 알고 분석할 수 있어 클라이언트의 요청을 전달하기 전 서버의 상태를 파악 후 로드 밸런싱을 진행할 수 있다.
## 19. 서브넷 마스크와, 게이트웨이에 대해 설명해 주세요.
서브넷(subnet)이란 하나의 네트워크가 불할되어 나눠진 작은 네트워크이다. 서브넷을 만들기 위해 네트워크를 분할하는 것은 서브네팅(subnettin)이다. 서브네팅을 하면 IP 할당 범위를 더 작은 단위로 쪼갤 수 있다. 서브네팅을 서브넷 마스크(subnet mask)를 통해서 계산되어 수행된다.

IP를 사용하는 네트워크 장치 수에 따라 효율적으로 사용할 수 있다. 