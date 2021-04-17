# Backend Interview
백엔드 인터뷰의 질문 및 답변 내용에 대해 정리하였습니다. 
CS인터뷰를 준비하는데 도움이 되기를 바랍니다. 


## Table Of Contents
- [데이터베이스](#데이터베이스)
- [네트워크](#네트워크)
- [운영체제](#운영체제)
- [자료구조와 알고리즘](#자료구조와-알고리즘)
- [컴퓨터 보안](#컴퓨터-보안)
- [프로그래밍 언어](#프로그래밍-언어)
- [기술동향](#기술동향)
- [기타](#기타)
- [참고자료](#참고자료)


<details>
  <summary>질문질문?</summary>
  </br>
  답변답변<br>
  
  </br>
</details>


## 데이터베이스


## 네트워크
<details>
  <summary>웹사이트에 접속할 때 무슨 일이 일이 일어나는지 설명해 보세요.</summary>
  </br>
  주소창에 URL을 입력하면 브라우저는 DNS서버에 요청을 해서 IP주소를 얻습니다. <br>
  IP주소를 얻으면 HTTP를 이용해서 IP주소로 웹사이트에 대해 요청합니다. <br>
  서버는 요청을 받으면, 처리해서 다시 응답을 보냅니다. <br>
  브라우저는 응답을 받으면 HTML코드를 파싱해서 화면에 출력합니다. <br>
  </br>
</details>

<details>
  <summary>DNS서버에 요청하는 과정을 자세하게 설명해 보세요.</summary>
  </br>
  www.google.com 에 요청한다고 가정하겠습니다. <br>
  브라우저는 DNS서버에 요청하기 전, 브라우저에 도메인이 캐싱되어 있는지 확인합니다. <br>
  없을 경우, OS의 hosts파일에 도메인이 있는지 확인합니다. 없을 경우, local dns서버에 물어봅니다. <br>
  local dns서버는 root name서버의 ip주소를 기록한 hint파일이 있어, <br>
  이것을 참조하여 local dns 서버로 요청을 보냅니다. <br>
  root name서버는 NS레코드와 A레코드가 있는 Glue레코드를 참조하여 <br>
  top-level name server를 참조하라고 응답합니다. <br>
  top-level name server - com 서버는 그 아래 서버에 대한 정보를 갖고 있어 <br>
  google.com의 네임서버를 참조하라고 응답합니다. <br>
  최조 요청을 받은 네임서버는 클라이언트에게 google.com의 IP주소를 전송합니다. <br>
  물론 각 서버는 한번 요청한 이후 캐시를 저장하고 있어 동일한 요청에 대해 계속 <br>
  다른 DNS서버로 요청을 보내지는 않습니다. 단, 캐시에는 TTL이 있어 유효기간이 지나면 삭제됩니다. <br>
  <br>
  DNS서버에 요청을 보낼 때, 보편적으로는 UDP/53 포트를 사용하지만, 전송 데이터가 512Byte이상이거나, <br>
  Zone Transfer가 일어나는 경우에는 TCP/53을 사용합니다. <br>
  DNS프로토콜은 원래 암호화를 하지 않지만, 감청 이슈로 인해, DNS over TLS, DNS over HTTPS 등을 <br>
  이용해 암호화하려는 기술들이 사용되고 있습니다. <br>
  </br>
</details>

<details>
  <summary>TCP와 UDP의 특징을 설명해 보세요.</summary>
  </br>
  TCP/UDP 모두 OSI 7 Layer 중 Transport layer에서 사용하는 기술입니다. <br>
  TCP는 3-way handshake 과정을 통해 연결을 설정하고 4-way handshaker과정을 통해 해제합니다. <br>
  TCP는 흐름 제어를 위해 보편적으로 Sliding Window 방식을 사용합니다. 한 번에 처리할 수 있는 <br>
  데이터를 정해 놓고, 보내고, 응답받고, 윈도우를 밀어내는 방식을 반복해서 전송합니다. <br>
  이 때, Receiver는 Sender로 ACK을 보냅니다. ACK을 보낼 때, Seq번호를 순차적으로 같이 <br>
  전송하기 때문에 Sender는 같은 Seq번호의 ACK이 여러 번 도착할 경우 문제가 발생한 것을 <br>
  알 수 있습니다.  <br>
  TCP는 세그먼트가 손실되었거나 훼손된 경우 를 통해 Go-Back-ARQ 등을 통해 재전송합니다.<br>
  네트워크가 혼잡해지지 않도록, Slow Start등의 혼잡제어 기법또한 사용합니다. <br>
  UDP에는 이러한 제어가 존재하지 않습니다. <br>
  TCP와 UDP 모두Checksum을 이용해서 전송받은 데이터가 정확한지 검증하는 과정을 거칩니다. <br>
  <br>
  TCP는 연결 지향형 프로토콜로, HTTP, FTP등에서 주로 사용하며 속도가 느리나 신뢰성을 보장합니다. <br>
  UDP는 그 반대로, 순서와 확실한 전송이 보장되지 않지만, 속도가 빠르고 헤더 크기가 작습니다. <br> 
  UDP는 DNS, 일부 실시간 동영상 서비스, 응답속도가 중요한 게임 등에서 사용합니다. <br>
  <br>
  다른 Transport Layer의 프로토콜로는 QUIC가 있습니다. <br>
  HTTP/3에서 사용하며, UDP기반이지만 신뢰성을 보장해줍니다. <br>
  </br>
</details>

<details>
  <summary>3-way handshake, 4-way handshake 과정을 설명해 보세요.</summary>
  </br>
  3-way handshake <br>
    1. Server는 Listen상태, Client에서 SYN(M) 전송 <br>
    2. Server는 응답을 받고 SYN_RCV로 상태 전환, ACK(N+1),SYN(N) 전송 <br>
    3. Client는 Established 상태로 전환, ACK(N+1)전송 <br>
    4. Server는 ACK을 받고 서버는 Established 상태로 전환 <br>
  <br>
  4-way handshake <br>
    1. Client는 FIN 전송 <br>
    2. Server는 FIN을 받고 TIMEOUT으로 상태 전환, 일단 ACK전송 <br>
    3. Server는 나머지 데이터 모두 전송 후 FIN 전송 <br>
    4. Client는 FIN받고, ACK전송 <br>
    5. Server는 ACK을 받고 소켓 Close <br>
    6. Client는 Time wait으로 일정 기간 대기 이후 Close <br>
  </br>
</details>

<details>
  <summary>라우터와 게이트웨이의 특징을 설명해보세요.</summary>
  </br>
  라우터는 OSI 7 Layer 중, Network Layer에서 동작하는 장비입니다. <br>
  Subnet이 다른 장비간을 연결 할 떄 사용합니다. <br>
  Routing Table을 참조하여 목적지의 IP주소에 따라 다른 Router로 패킷을 전달합니다. <br>
  라우팅 기법으로는 CIDR(사이더)방식을 가장 많이 활용하며, <br>
  각 네트워크의 영역을 구분지을 수 있습니다.  <br>
  게이트웨이는 서로 다른 통신망, 혹은 다른 프로토콜을 사용하는 네트워크 간을 연결해 줍니다. <br>
  다만 게이트웨이와 라우터는 명확하게 분리되는 개념이 아닙니다. 특정 역할을 의미하는 것이라서, <br>
  라우터가 게이트웨이의 역할을 할 수도 있고, 다른 장비나 소프트웨어가 그러한 역할을 할 수도 있습니다. 
  </br><br>
</details>

<details>
  <summary>스위치의 동작 방식을 설명해보세요.</summary>
  </br>
  스위치는 OSI 7 Layer 중, Data Link Layer에서 동작하는 장비입니다. <br>
  Mac Address가 기록된 테이블을 가지고 있어,  <br>
  목적지의 MAC주소를 가진 장비의 포트로만 프레임을 전송합니다. <br>
  스위치가 처음에 아무런 정보도 갖고 있지 않다면, 모든 포트로 프레임을 전송하지만, <br>
  프레임이 스위치를 거쳐갈 때, 각 포트의 MAC주소를 기억합니다. <br>
  처음 MAC주소를 사용한 통신을 하기 위해서는, 송신자는 ARP요청 패킷을 <br>
  Broadcast로 전송합니다. 모든 호스트와 라우터는 ARP 요청 패킷을 수신하지만, <br>
  요청 패킷에 해당하는 수신자만 ARP Reply 패킷을 유니캐스트로 전송합니다. <br>
  </br>
</details>

<details>
  <summary>HTTP와 HTTPS의 차이점에 대해서 설명해보세요.</summary>
  </br>
  HTTP는 평문 데이터를 전송하는 프로토콜이고, 이러한 과정에서 제3자가 패킷을 탈취할 경우, <br>
  패킷 안에 있는 정보를 볼 수 있습니다. HTTPS는 HTTP내용을 SSL/TLS를 프로토콜을 통해 <br>
  암호화 해서 전송합니다. <br>
  HTTPS는 80번 포트를, HTTPS는 443번 포트를 사용합니다.  <br>
  TLS통신을 위해서 Hannshake과정을 거치며, 내용은 다음과 같습니다. <br>
  1. Client는 ClientHello 전송 <br>
  2. Server는 ServerHello 전송 <br>
  3. Server는 인증서, 랜덤 데이터를 포함한 Certificate전송 <br>
  4. Client는 인증서 검증 <br>
  5. Client는 pre-master secret을 생성하고 인증서의 공개 키를 이용해 암호화, 전송 <br>
  6. Server는 복호화해서 pre-master secret을 알아내고, master secret생성 <br>
  7. Server는 master secret으로 Session key생성 <br>
  8. Server, Client는 ChangeCipherSpec, Finished전송으로 과정 완료 <br>
  9. Server, Client는 대칭키 암호를 이용해 통신 <br>
  <br>
</details>

<details>
  <summary>TLS/SSL에서 인증서를 검증하는 과정을 설명해보세요.</summary>
  </br>
  인증서에는, 발급자, 서명 알고리즘, 유효기간, 공개 키, 지문 등의 내용이 있습니다. <br>
  <br>
  인증서의 검증은 최상위 인증 기관 - Root CA가 신뢰할 수 있다는 것으로 시작합니다. <br>
  Root CA들의 인증서 및 공개 키는 보통 MS 트러스티드 루트 프로그램 등, OS에서 받아옵니다. <br>
  다만 최근 Chrome의 경우 자체 루트 인증인 Chrome root program을 운영할 계획이라고 합니다. <br>
  <br>
  중간 인증 기관(ICA)의 인증서가 신뢰할 만한 인증서인지 검증하기 위해, <br>
  ICA인증서의 지문을 RootCA의 공개키를 이용해서 복호화합니다. <br>
  이 지문이 인증서의 해시값과 일치할 경우 인증서를 신뢰할 수 있습니다 <br>
  동일한 과정을 하위 CA까지 검증하는 과정(Chain of Trust)으로 인증서를 검증할 수 있습니다. <br>
  암호화 알고리즘으로는 SHA256 RSA2048을 주로 사용합니다.<br>
  다만 RootCA를 신뢰할 수 없을 때, <br>
  즉 RootCA의 비밀키가 유출되었을 경우에는 문제가 발생할 수 있습니다. <br>
  참고: chrome://settings/security <br>
  <br>
</details>

<details>
  <summary>RESTful 대해서 설명해보세요.</summary>
  </br>
    
  </br>
</details>

<details>
  <summary>OSI 7 Layer와 TCP/IP의 차이에 대해서 설명해보세요.</summary>
  </br>

  </br>
</details>

<details>
  <summary>CORS에 대해서 설명해보세요.</summary>
  </br>

  </br>
</details>



## 운영체제


## 자료구조와 알고리즘


## 컴퓨터 보안


## 프로그래밍 언어


## 기술동향


## 기타


## 참고자료
https://github.com/ksundong/backend-interview-question

[네이버 기술 블로그](https://d2.naver.com/helloworld)

[라인 기술 블로그](https://engineering.linecorp.com/ko/blog/)

[카카오 기술 블로그](https://tech.kakao.com/blog/)

[쿠팡 기술 블로그](https://medium.com/coupang-tech/technote/home)

[우아한형제들 기술 블로그](https://woowabros.github.io/)

[NHN 기술 블로그](https://meetup.toast.com/)

[나무위키](https://namu.wiki/)




