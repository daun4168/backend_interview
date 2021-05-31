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
- [기타](#기타)
- [참고자료](#참고자료)


<details>
  <summary>질문에 대해서 설명해 보세요.</summary>
  </br>
  답변답변답변<br>
  </br>
</details>


## 데이터베이스
<details>
  <summary>RDBMS와 NOSQL의 특징에 대해서 설명해 보세요.</summary>
  </br>
  RDB의 경우, 정해진 스키마를 갖고 있습니다. <br>
  데이터는 관계를 통해서 여러개의 테이블에 분산됩니다. <br>
  테이블간의 관계에서 foreigen key를 사용해서 join이 가능하다는 점이 특징입니다. <br>
  NOSQL의 경우에는 다양한 프로그램들이 있어서 각기 특징이 다릅니다. <br>
  보편적인 특징으로는, RDB와 반대로 Schema가 존재하지 않고, 테이블 간의 관계를 정의하지 않으며, <br>
  분산 저장을 통한 Scale-out에 유리한 구조를 가지고 있습니다. <br>
  <br>
  RDB는 데이터 구조가 명확하고 변경 될 여지가 없고, <br> 
  데이터 무결성에 대한 보장이 필요한 시스템에서 사용하는 것이 좋습니다. <br>
  또한, 관계를 맺고 있는 데이터가 자주 Update가 일어나는 경우에 적합합니다. <br>
  NOSQL은 데이터 구조를 잘 알 수 없고, <br>
  데이터의 구조의 변경이 일어날 수 있는 경우에 사용하는  것이 좋습니다. <br>
  또한 데이터의 양이 많지만 Update가 많이 이루어지지 않는 시스템에 사용하는 것이 좋습니다. <br>
  </br>
</details>

<details>
  <summary>Transaction, ACID에 대해서 설명해 보세요.</summary>
  </br>
  트랜잭션이란 DB내에서 하나의 논리적 기능을 수행하기 위해서 여러 작업들을 묶어놓은 단위입니다. <br>
  ACID란 트랜잭션의 특징입니다. Atomicity, Consistency, Isolation, Durability를 나타냅니다.<br>
  <br>
  Atomicity, 원자성은 All or Nothing, 즉 한 트랜잭션 내의 모든 연산이<br>
  전부 수행되거나, 아니면 전부 수행되지 않는다는 것을 나타냅니다.<br>
  Consistnecy, 일관성은 트랜잭션 완료 이후에도 일관성 있는 DB상태를 유지하는 것을 의미합니다. <br>
  시스템의 규칙은 수행 전과 수행 후에도 같아야 합니다.<br>
  Isolation, 독립성은 트랜잭션 수행 중에는 다른 작업이 영향을 주지 않는다는 뜻입니다. <br>
  즉, 트랜잭션의 순서는 연속적이여야만 함을 의미합니다. <br>
  Durability, 영구성은 성공적으로 수행된 트랜잭션은 영원히 반영됨을 뜻합니다. <br>
  모든 트랜잭션은 로그로 남고, 이전 상태로 되돌릴 수 있습니다. <br>
  <br>
</details>

<details>
  <summary>Transaction의 Isolation Level에 대해서 설명해 보세요.</summary>
  </br>
  트랜잭션의 격리 수준은 여러가지 단계가 있습니다. <br>
  Lock 또는, MVCC(multiversion concurrency control)를 사용합니다. <br>
  <br>
  Level0, Read Uncommitted는 트랜젝션에서 처리중인,  <br>
  아직 커밋되지 않은 데이터를 다른 트랜잭션이 읽는 것을 허용합니다. <br>
  Dirty Read현상이 발생합니다.<br>
  정합성에 문제가 많아 주로 사용하지는 않습니다. <br>
  <br>
  Level1, Read Committed는 커밋되어 확정된 데이터만 읽는 것을 허용합니다.  <br>
  Non-Reapeatable Read(Inconsistent Analysis)현상이 발생합니다. <br>
  읽기를 공유하는 Lock를 이용해서 하나의 레코드를 읽을 때 Lock를 설정하고,  <br>
  해당 레코드에서 빠지는 순간 Lock을 해제해서 구현하는 방식이 있습니다. <br>
  또는 쿼리시작 시점의 Undo데이터를 제공하는 방식으로 구현이 가능합니다. <br>
  성능과 정합성에 적절한 타협을 한 방식으로 DBMS에서 주로 사용합니다. <br>
  <br>
  Level2, Repeatable Read는, 선행 트랜잭션이 읽은 데이터를 트랜잭션이 종료될 때 까지 <br>
  이후 트랜잭션이 Update/Delete를 하는 것을 허용하지 않습니다. <br>
  Phantom Read(첫번째 쿼리에서 없던 레코드가 두번째 쿼리에서 나타남)현상이 발생합니다.<br>
  Lock을 커밋할 때 까지 유지하는 방식으로 구현하거나,  <br>
  각 트랜잭션에 순차적으로 ID를 부여하여, <br>
  트랜잭션 ID보다 작은 번호에서 변경된 것만 읽게 하는 방식으로 구현이 가능합니다. <br>
  <br>
  Level3, Serializable는, 트랜잭션을 순차적으로 처리하는 것을 의미합니다. <br>
  읽는 것이 가장 엄격하고 정밀한 isolation을 보장하지만, <br>
  동시 처리성능이 낮아 거의 사용되지 않습니다. <br>
  <br>
</details>

<details>
  <summary>RDBMS의 Index에 대해서 설명해 보세요.</summary>
  </br>
  인덱스는 테이블의 동작 속도를 높여주는 자료 구조입니다. <br>
  인덱스를 설정할 때는, Cardinality 등의 기준을 사용해서 결정합니다. <br>
  Cardinality란, 특정 컬럼에 사용되는 값의 유니크한 값의 개수입니다.   <br>
  Cardinality가 높을 수록 인덱스를 설정했을 때 효율적입니다.  <br>
  Index를 설정할 경우 Select Query는 효과적으로 실행할 수 있지만,  <br>
  Create, Update, Delete Query의 경우 성능이 떨어지므로,  <br>
  DB가 어떻게 사용되는 지에 따라 적절한 수준으로 설정하는 것이 좋습니다.  <br>
  </br>
</details>

<details>
  <summary>데이터베이스 정규화에 대해서 설명해 보세요.</summary>
  </br>
  데이터베이스 정규화에는, 1NF, 2NF, 3NF, BCNF등이 있습니다. <br>
  정규화 되지 않은 테이블은, 갱신 이상, 삽입 이상, 삭제 이상 등의 문제가 있습니다. <br>
  정규화를 통해, Data Reduncamcy를 제거하며, <br>
  데이터 저장을 논리적으로, 의미있게(informative) 할 수 있는 장점이 있습니다.  <br>
  또한 데이터베이스 구조 확장 시에 구조 변경을 최소화 할 수 있습니다.  <br>
  <br>
  1NF, 1차 정규형의 핵심은, 각 Row마다 Column의 값이 1개씩만 있어야 합니다. (Atomic Value)<br>
  원칙적으로는 "어떤 관계와 동일 구조"임을 뜻하며, 아래의 조건이 있습니다.<br>
  1. 모든 Column(attribute)는 각 Table에서 Unique하다. <br>
  2. 모든 entry는 하나의 값을 가져야 하며, Atomic해야 한다. <br>
  3. 중복되는 Row가 없다.<br>
  <br>
  2NF, 2차 정규형의 핵심은, 부분적 종속이 없어야 합니다. (완전 함수 종속)<br>
  즉, Candidate Key와 K와, K에 속하지 않은 Attirbute A가 있을 때, <br>
  A를 결정하기 위해 K일부로 결정되지 않고, K전체를 참조해야 하는 경우,<br>
  1NF인 테이블은 2NF의 필요충분조건을 만족합니다. <br>
  <br>
  3NF, 3차 정규형의 핵심은 테이블 내의 모든 속성이 기본 키에만 의존해야 합니다. <br>
  (이행적 함수 종속 없음)<br>
  이행적 함수 종속이란 A -> B, B -> C  ==> A -> C 를 의미합니다. <br>
  <br>
  BCNF 정규화의 핵심은 모든 결정자가 후보 키가 되는 것입니다. <br>
  즉, 어떤 컬럼이 다른 컬럼의 값을 결정하는 결정자인데 Candidate Key가 아니라면,<br>
  BCNF 정규화를 만족시키기 위해 분해해야 합니다. <br>
  </br>
</details>

<details>
  <summary>Partitioning과 Sharding에 대해서 설명해 보세요.</summary>
  </br>
  파티셔닝은, Perfomance, Manageability, Availability를 향상시키기 위해<br>
  테이블/인덱스를 분리하는 방법입니다. <br>
  <br>
  파티셔닝 방법은 크게 두가지로 볼 수 있습니다.<br>
  Horizontal Partitioning은, 동일한 스키마의 데이터를 여러개의 테이블에<br>
  나누어 저장하는 것을 뜻합니다. Row기반으로 데이터를 분리합니다. <br>
  Vertical Partitioning은, 하나의 Entity에 저장된 데이터를 여러개의 엔티티로<br>
  분리하는것을 뜻합니다. Column기반으로 데이터를 분리합니다. <br>
  <br>
  Range Partitioning은, 연속적인 숫자 등을 기준으로 파티셔닝 하는 방식입니다. <br>
  Hash Partitioning은, 각 파티션마다 해시값의 범위를 할당하는 방식입니다. <br>
  범위 Query를 효율적으로 실행이 불가능하다는 단점이 있습니다. <br>
  추가적으로 보조 색인이 존재하는 DB라면 다음의 파티셔닝 방식을 사용합니다.<br>
  Document-based partitioning(Local index)의 경우, <br>
  각 파티션마다 index를 둡니다.<br>
  Term-based partitioning(Global index)의 경우, <br>
  모든 파티션의 데이터를 담당하는 index를 만들고, global index또한 파티셔닝합니다. <br>
  Global index의 갱신은 보편적으로 비동기적으로 이루어집니다. <br>
  <br>
  샤딩은, Horizontal Partitioning을 뜻하기도 하고, <br>
  그중에서도 물리적인 형태로 파티셔닝 하는 것만을 뜻하기도 합니다. <br>
  </br>
</details>

<details>
  <summary>Replication과 Clustering에 대해서 설명해 보세요.</summary>
  </br>
  리플리케이션은, DB를 권한에 따라 Master-Slave로 구축하는 방식입니다.  <br>
  Master Node는 쓰기작업만을, Slave Node는 읽기작업만을 처리합니다.  <br>
  비동기적으로 운영되어 지연시간이 적은 장점이 있지만, <br>
  데이터 동기화가 보장되지 않아 일관성에 문제가 있을 수 있고, <br>
  Master Node에 문제가 생길 경우 복구가 어렵습니다. <br>
  <br>
  클러스터링은, DB를 여러개의 서버에 수평적으로 구축하는 방식입니다. <br>
  클러스터링은 SPoF(Single point of Failure)와 같은 문제를 해결하기 위해서 사용합니다. <br>
  동기적으로 운영되어 Write에 지연 시간이 있습니다. <br>
  항상 일관성있는 데이터를 얻을 수 있고,  <br>
  하나의 노드가 죽어도 끊김없이 계속 운용이 가능합니다.  <br>
  </br>
</details>

<details>
  <summary>Consistent Hashing에 대해서 설명해 보세요.</summary>
  </br>
  Hash Ring을 사용해서 해싱을 하는 방법입니다. <br>
  메타정보 조회 없이 클러스터에서 키가 저장된 노드를 바로 찾아갈 수 있습니다.<br>
  Rebalancing문제를 해결하기 위한 방법입니다. <br>
  Virtual Node는, 실제 물리 노드보다 토큰을 더 많이 보유하는 방식입니다.<br>
  이를 통해, Object분포의 불균일성을 해결합니다. <br>
  <br>
  일반 HashTable을 사용하면, 분산 DB에서 node를 추가하거나 삭제하는데<br>
  O(K)의 시간이 걸립니다. (K는 Key의 수) Coninstent Hashing을 사용하면<br>
  O(K/N)의 시간으로 가능합니다. 단, Key를 추가하거나 삭제할 때, <br>
  일반적인 HashTable은 O(1)이면 가능하지만, Consistent Hashing의 경우<br>
  O(logN)의 시간이 걸립니다. (N은 Node의 수)<br>
  <br>
  DynamoDB, Memcached와 같은 NOSQL에 주로 사용되고 있습니다. <br>
  </br>
</details>

<details>
  <summary>DHT에 대해서 설명해 보세요.</summary>
  </br>
  Distributeed Hash Table
  Cassandra, BitTorrent
  </br>
</details>

<details>
  <summary>NOSQL 종류에 대해서 설명해 보세요.</summary>
  </br>
  
  </br>
</details>

<details>
  <summary>분산형 데이터베이스의 CAP에 대해서 설명해 보세요.</summary>
  </br>
  Database가 Consistency, Availability, Partitioning를 모두 만족할 수 없고, 
  둘만 만족할 수 있다는  것입니다. 
  </br>
</details>




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
  최  요청을 받은 네임서버는 클라이언트에게 google.com의 IP주소를 전송합니다. <br>
  물론 각 서버는 한번 요청한 이후 캐시를 저장하고 있어 동일한 요청에 대해 계속 <br>
  다른 DNS서버로 요청을 보내지는 않습니다. 단, 캐시에는 TTL이 있어 유효기간이 지나면 삭제됩니다. <br>
  Windows의 경우, default로 86,400(1day)만큼 DNS Cache를 저장합니다. <br>
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
  <summary>Router와 Gateway의 특징을 설명해 보세요.</summary>
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
  <summary>Switch의 동작 방식을 설명해 보세요.</summary>
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
  <summary>HTTP와 HTTPS의 차이점에 대해서 설명해 보세요.</summary>
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
  <summary>TLS/SSL에서 인증서를 검증하는 과정을 설명해 보세요.</summary>
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
  <summary>Load Balancer에 대해 설명해 보세요.</summary>
  </br>
   로드 밸런서는 서버에 가해지는 부하를 분산해주는 장치 및 기술을 말합니다. <br>
   서버에서 서비스를 하기에 트래픽이 너무 높다면 Scale-up / Scale-out 을 해야 합니다. <br>
   다만 Scale-up은 한계가 있어 결국 분산 처리를 위해 Scale-out을 합니다. <br>
   DNS서버가 로드밸런서의 IP주소를 클라이언트에게 전송하고, 클라이언트는 로드밸런서로 요청을 보냅니다. <br>
   로드밸런서는 요청을 서버로 분배하고, 서버는 로드밸런서로, 또는 클라이언트로 직접 응답을 보냅니다. <br>
   로드밸런서는, Health Check, Tunneling, NAT(Network Address Translation) 등의 기능을 합니다. 
   로드밸런서의 종류로는 4-layer / 7-layer에서 작동하는 로드밸런서가 있습니다. <br>
   l4 로드밸런서의 작동 방식중 대표적인 것은 다음과 같습니다. <br>
   Weighted Least Connections: 서버의 커넥션의 수와 가중치를 바탕으로 요청을 분배합니다. <br>
   Fastest Response Time: 서버가 응답하는 시간이 가장 빠른 서버로 요청을 분배합니다. <br>
   Source Hash Scehduling: 사용자의 IP를 해싱하고 그 결과로 서버로 요청을 분배합니다. <br>
   l7 로드밸런서의 경우 l4로드밸런서의 기능을 포함하여, 추가적으로 <br>
   URL Switching: 하위 URL들을 특정 서버로 처리합니다.<br>
   Context Swithcing: 리소스에 따라 요청을 분배합니다. (이미지/동영상 등)<br>
   Persistence with Cookies: 쿠키 정보를 바탕으로 동일한 서버에 계속 할당해주는 방식입니다. <br>
   <br>
   SLB에서 발전된 개념으로 GSLB가 있습니다. <br>
   GSLB란 DNS를 기반으로 로드밸런싱을 하는 방법입니다. <br>
   동일한 서비스를 하는 서버들이 여러 지역에 분산되어 운용 될 때 이용하는 방식입니다. <br>
   단순 DNS방식에 비해, Health Check를 하고, RTT및 지리적 위치를 고려하여 <br>
   요청을 분배한다는 장점이 있습니다. <br>
   GSLB는 Local name server와 Second Level name server사이에 위치합니다. <br>
   GSLB는 DNS Proxy로 동작하여, DNS Query를 내부 DNS서버로 전달하는 역할을 합니다. <br>
   </br>
</details>

<details>
  <summary>HTML Status Code에 대해서 설명해 보세요.</summary>
  </br>
   200: 성공 <br>
   3xx: 리다이렉션 <br>
   403: Forbidden, 권한 없음 <br>
   404: Not Found, 찾을 수 없음<br>
   500: 내부 서버 오류<br>
   503: 서비스 사용 불가 (서버 오버로드 등)<br>
  </br>
</details>

<details>
  <summary>RESTful 대해서 설명해 보세요.</summary>
  </br>
   REST란 Representational State Transfer의 약자입니다. <br>
   REST API는 URI, HTTP Method, Representation으로 이루어져 있습니다.<br>
   URI는, Resource를 뜻하는 것으로 명사적으로 구성되는 것이 좋습니다.<br>
   HTTP Method는, Verb를 뜻하는 것으로 GET, POST, PUT, DELETE등이 있습니다.<br>
   각 메소드는 CRUD에 대응되며, 그에 맞는 동작을 하도록 구성하는 것이 좋습니다. <br>
   Representation은 응답을 뜻합니다. Json을 주로 사용하나, XML, TEXT등도 사용가능합니다.<br>
   <br>
   REST의 특징으로는 6가지의 제한 조건이 있습니다. <br>
   1. Uniform Interface는, Resource에 대한 조작을 통일된 인터페이스로 수행가능해야 합니다.<br>
   HTTP를 따르는 모든 플랫폼에서 사용이 가능해야 하고, 특정 언어나 플랫폼에 종속되지 않습니다.<br>
   또한, 메세지의 내용을 읽는 것으로 무슨 요청을 판단하는지 사람이 쉽게 알 수 있습니다. <br>
   2. Stateless는, 클라이언트의 상태를 서버가 유지하지 않는다는 것을 의미합니다.<br>
   세션, 쿠키 등을 별도로 관리하지 않아, 자유도가 높아지고 구현이 단순해집니다.<br>
   3. Cacheable은, HTTP를 사용하는 덕분에 HTTP의 해싱 기능이 사용가능하다는 점입니다.<br>
   4. Layered System은, REST서버가 여러 계층으로 구성될 수 있다는 점입니다. <br>
   로드밸런싱, SSL등을 하는 계층을 추가할 수 있습니다. <br>
   5. Client-server architecture는, 클라이언트와 서버가 분리되어 의존성이 줄어든다는 점입니다.<br>
   실질적으로 Backend와 Frontend의 개발의 분리가 쉬워질 수 있습니다. <br>
   6. Code on demand(Optional)는, Server로부터 스크립트를 받아서 클라이언트에서 JS등으로<br>
   실행이 가능하다는 점입니다. <br>
  </br>
</details>

<details>
  <summary>gRPC에 대해서 설명해 보세요.</summary>
  </br>
  https://medium.com/naver-cloud-platform/nbp-%EA%B8%B0%EC%88%A0-%EA%B2%BD%ED%97%98-%EC%8B%9C%EB%8C%80%EC%9D%98-%ED%9D%90%EB%A6%84-grpc-%EA%B9%8A%EA%B2%8C-%ED%8C%8C%EA%B3%A0%EB%93%A4%EA%B8%B0-1-39e97cb3460
  </br>
</details>

<details>
  <summary>Proxy에 대해서 설명해 보세요.</summary>
  </br>
  프록시는, 클라이언트가 자신을 통해서 타 네트워크 서비스에 간접적으로 접속할 수 있게 해주는 </br>
  시스템을 뜻합니다.  보안을 목적으로, 또는 캐시를 이용한 빠른 서비스를 목적으로 주로 사용합니다. </br>
  Open Proxy(Forwarding Proxy)는, 어떤 유저라도 접속 가능한 프록시 서버를 뜻합니다. </br>
  Anonymous Proxy, Transparnet Proxy 등이 존재합니다. </br>
  Reverse Proxy(Surrogate Proxy)는, 클라이언트들이 프록시 서버를 볼 때, 원본 서버로</br>
  보이게 하는 시스템을 뜻합니다. 클라이언트는 원본 서버의 존재를 알 수 없고, 모든 원본 서버의</br>
  트래픽은 프록시를 통해 거쳐가게 됩니다. </br>
  SSL Encryption, Load balancing, Cache, Compression등의 목적으로 사용합니다. </br>
  </br>
</details>

<details>
  <summary>VPN에 대해서 설명해 보세요.</summary>
  </br>
  </br>
</details>

<details>
  <summary>OSI 7 Layer와 TCP/IP의 차이에 대해서 설명해 보세요.</summary>
  </br>
  Application Layer
  Presentation Layer
  Session Layer
  Transport Layer
  Network Layer
  Datalink Layer: Frames / 주소할당/오류감지 MAC address / ex)Ethernet
  Physical Layer: 하드웨어
  </br>
</details>

<details>
  <summary>NAT(네트워크 주소 변환)에 대해서 설명해 보세요.</summary>
  </br>

  </br>
</details>

<details>
  <summary>CORS에 대해서 설명해 보세요.</summary>
  </br>

  </br>
</details>

<details>
  <summary>세션과 쿠키에 대해서 설명해 보세요.</summary>
  </br>

  </br>
</details>

<details>
  <summary>CDN에 대해서 설명해 보세요.</summary>
  </br>

  </br>
</details>

<details>
  <summary>Flow Control과 Congestion Control에 대해서 설명해 보세요.</summary>
  </br>

  </br>
</details>


## 운영체제

<details>
  <summary>Process와 Thread의 특징에 대해서 설명해 보세요.</summary>
  </br>

  </br>
</details>

<details>
  <summary>Context Switching 과정에 대해서 설명해 보세요.</summary>
  </br>

  </br>
</details>

<details>
  <summary>Deadlock에 대해서 설명해 보세요.</summary>
  </br>

  </br>
</details>

<details>
  <summary>Critical Section에 대해서 설명해 보세요.</summary>
  </br>

  </br>
</details>

<details>
  <summary>Starvation현상에 대해서 설명해 보세요.</summary>
  </br>

  </br>
</details>

<details>
  <summary>Paging과 Segmentation에 대해서 설명해 보세요.</summary>
  </br>

  </br>
</details>

<details>
  <summary>Blocking과 Nonblocking의 특징에 대해서 설명해 보세요.</summary>
  </br>

  </br>
</details>

<details>
  <summary>Synchronous와 Asynchronous의 특징에 대해서 설명해 보세요.</summary>
  </br>
  동기 작업은, 작업을 동시에 수행하거나, 끝나거나, 끝나는 동시에 시작하는 것을 의미합니다.
  비동기 작업은, 상대방과 관계 없이 수행합니다. 
  </br>
</details>

<details>
  <summaryMemory Structure에 대해서 설명해 보세요.</summary>
  </br>
  Code, Data, Stack, Heap
  </br>
</details>

<details>
  <summary>리눅스 커널에 대해서 설명해 보세요.</summary>
  </br>

  </br>
</details>


## 자료구조와 알고리즘

<details>
  <summary>LSH에 대해서 설명해 보세요.</summary>
  </br>
  Jaccard 유사도 J(A, B) = |A∪B|/|A∪B| </br>
  min-hash </br>
  Rabin fingerprint </br>
  Locality Senesitive Hashing </br>
  </br>
</details>

<details>
  <summary>B+Tree에 대해서 설명해 보세요.</summary>
  </br>
  
  </br>
</details>

<details>
  <summary>LSM Tree에 대해서 설명해 보세요.</summary>
  </br>
  Log-Structured Merge Tree
  </br>
</details>

<details>
  <summary>Dijkstra Algorithm에 대해서 설명해 보세요.</summary>
  </br>

  </br>
</details>

<details>
  <summary>A* Algorithm에 대해서 설명해 보세요.</summary>
  </br>

  </br>
</details>

<details>
  <summary>Huffman Coding에 대해서 설명해 보세요.</summary>
  </br>

  </br>
</details>

<details>
  <summary>Red Black Tree에 대해서 설명해 보세요.</summary>
  </br>

  </br>
</details>

<details>
  <summary>Hash Collision을 처리하는 방법을 설명해 보세요.</summary>
  </br>
  1. Sepearate Chaning는, Linked List로 해시 충돌을 처리한다. </br>
  2. Open Addressing은, Liniear Probing, Double Hashing등을 사용해서</br>
  다른 버켓에 담는 것으로 해시 충돌을 처리한다.</br>
  </br>
</details>


## 컴퓨터 보안

<details>
  <summary>SQL Injection에 대해서 설명해 보세요.</summary>
  </br>

  </br>
</details>

<details>
  <summary>XSS에 대해서 설명해 보세요.</summary>
  </br>

  </br>
</details>

<details>
  <summary>CSRF에 대해서 설명해 보세요.</summary>
  </br>

  </br>
</details>

<details>
  <summary>ARP spoofing에 대해서 설명해 보세요.</summary>
  </br>

  </br>
</details>

<details>
  <summary>DNS spoofing에 대해서 설명해 보세요.</summary>
  </br>

  </br>
</details>

<details>
  <summary>DDoS, DRDos에 대해서 설명해 보세요.</summary>
  </br>

  </br>
</details>

<details>
  <summary>RSA에 대해서 설명해 보세요.</summary>
  </br>

  </br>
</details>

<details>
  <summary>Diffie–Hellman key exchange에 대해서 설명해 보세요.</summary>
  </br>

  </br>
</details>

<details>
  <summary>OAuth에 대해서 설명해 보세요.</summary>
  </br>

  </br>
</details>


## 프로그래밍 언어

<details>
  <summary>Singleton Pattern에 대해서 설명해 보세요.</summary>
  </br>

  </br>
</details>

<details>
  <summary>Java의 Overriding과 Overloading에 대해서 설명해 보세요.</summary>
  </br>

  </br>
</details>

<details>
  <summary>Java의 JVM에 대해서 설명해 보세요.</summary>
  </br>

  </br>
</details>

<details>
  <summary>Java의 Generic에 대해서 설명해 보세요.</summary>
  </br>

  </br>
</details>

<details>
  <summary>Python의 GIL에 대해서 설명해 보세요.</summary>
  </br>

  </br>
</details>

<details>
  <summary>Garbage Collection에 대해서 설명해 보세요.</summary>
  </br>

  </br>
</details>

<details>
  <summary>MVC Pattern에 대해서 설명해 보세요.</summary>
  </br>

  </br>
</details>

<details>
  <summary>JS의 Callback과 Closure에 대해서 설명해 보세요.</summary>
  </br>

  </br>
</details>


## 기타
<details>
  <summary>Docker에 대해서 설명해 보세요.</summary>
  </br>

  </br>
</details>

<details>
  <summary>Kubernates에 대해서 설명해 보세요.</summary>
  </br>

  </br>
</details>

<details>
  <summary>TDD에 대해서 설명해 보세요.</summary>
  </br>

  </br>
</details>

<details>
  <summary>CI/CD에 대해서 설명해 보세요.</summary>
  </br>

  </br>
</details>

<details>
  <summary>Git에 대해서 설명해 보세요.</summary>
  </br>

  </br>
</details>


## 참고자료
[Backend-Interview-Question](https://github.com/ksundong/backend-interview-question)

[네이버 기술 블로그](https://d2.naver.com/helloworld)

[라인 기술 블로그](https://engineering.linecorp.com/ko/blog/)

[카카오 기술 블로그](https://tech.kakao.com/blog/)

[쿠팡 기술 블로그](https://medium.com/coupang-tech/technote/home)

[우아한형제들 기술 블로그](https://woowabros.github.io/)

[NHN 기술 블로그](https://meetup.toast.com/)

[삼성 S/W Membership](http://www.secmem.org/)

[나무위키](https://namu.wiki/)

[위키백과](https://ko.wikipedia.org/wiki/)
