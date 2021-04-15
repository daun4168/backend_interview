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
  주소창에 URL을 입력하면 브라우저는 DNS서버에 요청을 해서 IP주소를 얻습니다. 
  IP주소를 얻으면 HTTP를 이용해서 IP주소로 웹사이트에 대해 요청합니다. 
  서버는 요청을 받으면, 처리해서 다시 응답을 보냅니다. 
  브라우저는 응답을 받으면 HTML코드를 파싱해서 화면에 출력합니다. 
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



## 운영체제


## 자료구조와 알고리즘


## 컴퓨터 보안


## 프로그래밍 언어


## 기술동향


## 기타


## 참고자료
[네이버 기술 블로그](https://d2.naver.com/helloworld)

[라인 기술 블로그](https://engineering.linecorp.com/ko/blog/)

[카카오 기술 블로그](https://tech.kakao.com/blog/)

[쿠팡 기술 블로그](https://medium.com/coupang-tech/technote/home)

[우아한형제들 기술 블로그](https://woowabros.github.io/)

[NHN 기술 블로그](https://meetup.toast.com/)

https://github.com/ksundong/backend-interview-question



