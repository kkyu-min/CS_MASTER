# CS_MASTER

기술 면접 대비를 위한 CS정리 Repository입니다.

### ❤️ fork, Star 환영합니다.

### 📕 Contents

---

# 1. 운영체제

<details>
  <summary>프로세스와 스레드의 차이를 설명해보세요.</summary>
  </br>
  <p>프로세스는 실행중인 프로그램을 의미합니다. 스레드는 실행 제어만 분리한 것을 의미합니다.</p>
  <p>프로세스는 운영체제로부터 자원을 할당받지만, 스레드는 프로세스로부터 자원을 할당받고, 프로세스의 코드/데이터/힙영역을 공유하기 때문에 좀 더 효율적으로 통신할 수 있습니다. 또한 컨텍스트 스위칭도 캐시 메모리를 비우지 않아도 되는 스레드쪽이 빠릅니다. 그리고, 스레드는 자원 공유로 인해 문제가 발생할 수 있으니 이를 염두에 둔 프로그래밍을 해야합니다.</p>
  <p>한 프로세스 안에 여러개의 스레드가 생성될 수 있습니다.</p>
</details>

<details>
  <summary>컨텍스트 스위칭에 대해 설명해보세요.</summary>
  </br>
  <p>컨텍스트 스위칭은 한 Task가 끝날 때까지 기다리는 것이 아니라 여러 작업을 번갈아가며 실행해서 동시에 처리될 수 있도록 하는 방법입니다.</p>
  <p>인터럽트가 발생하면 현재 프로세스의 상태를 PCB에 저장하고 새로운 프로세스의 상태를 레지스터에 저장하는 방식으로 동작합니다. 이 때, CPU는 아무런 일을 하지 않으므로 잦은 컨텍스트 스위칭은 성능저하를 일으킬 수 있습니다.</p>
  <p>스레드와 프로세스의 동작방식이 약간 상이한데, 스레드는 캐시메모리나 PCB에 저장해야하는 내용이 적고, 비워야 하는 내용도 적기때문에 상대적으로 더 빠른 컨텍스트 스위칭이 일어날 수 있습니다.</p>
</details>

<details>
   <summary> 운영체제란 </summary>
    <a href="https://github.com/kkyu-min/CS_MASTER/tree/main/OS/OS">[1. 운영체제란]</a>
<br />
</details>

<details>
   <summary> 프로세스 vs 스레드 </summary>
    <a href="https://github.com/kkyu-min/CS_MASTER/tree/main/OS/ProcessAndThread">[2. 프로세스 vs 스레드]</a>
<br />
</details>

<details>
   <summary> 프로세스 주소 공간 </summary>
    <a href="https://github.com/kkyu-min/CS_MASTER/tree/main/OS/ProcessAddressSpace">[3. 프로세스 주소 공간]</a>
<br />
</details>

<details>
   <summary> 인터럽트(Interrupt)와 시스템 콜(System Call) </summary>
    <a href="https://github.com/kkyu-min/CS_MASTER/tree/main/OS/InterruptAndSystemCall">[4. 인터럽트(Interrupt)와 시스템 콜(System Call)]</a>
<br />
</details>

<details>
   <summary> PCB와 Context Switching </summary>
    <a href="https://github.com/kkyu-min/CS_MASTER/tree/main/OS/ContextSwitching">[5. PCB와 컨텍스트 스위칭]</a>
<br />
</details>

<details>
   <summary> IPC(Inter Process Communication) </summary>
    <a href="https://github.com/kkyu-min/CS_MASTER/tree/main/OS/IPC">[6. IPC]</a>
<br />
</details>

<details>
   <summary> CPU 스케줄링 </summary>
    <a href="https://github.com/kkyu-min/CS_MASTER/tree/main/OS/CPU-Scheduling">[7. CPU 스케줄링]</a>
<br />
</details>

<details>
   <summary> 데드락 </summary>
    <a href="https://github.com/kkyu-min/CS_MASTER/tree/main/OS/DeadLock">[8. 데드락]</a>
<br />
</details>

데드락(DeadLock)
Race Condition
세마포어(Semaphore) & 뮤텍스(Mutex)
페이징 & 세그먼테이션 (PDF)
페이지 교체 알고리즘
메모리(Memory)
파일 시스템
<br>

# 2. 네트워크

<details>
   <summary> OSI 7계층  </summary>
<br />
</details>
<details>
   <summary> TCP/IP의 개념  </summary>
<br />
</details>
<details>
   <summary> TCP와 UDP  </summary>
<br />
</details>
<details>
   <summary> TCP와 UDP의 헤더 분석  </summary>
<br />
</details>
<details>
   <summary> TCP의 3-way-handshake와 4-way-handshake   </summary>
<br />
</details>
<details>
   <summary> TCP의 연결 설정 과정(3단계)과 연결 종료 과정(4단계)이 단계가 차이나는 이유?</summary>
<br />
</details>
<details>
   <summary> 만약 Server에서 FIN 플래그를 전송하기 전에 전송한 패킷이 Routing 지연이나 패킷 유실로 인한 재전송 등으로 인해 FIN 패킷보다 늦게 도착하는 상황이 발생하면 어떻게 될까? </summary>
<br />
</details>

<details>
   <summary> 초기 Sequence Number인 ISN을 0부터 시작하지 않고 난수를 생성해서 설정하는 이유?  </summary>
<br />
</details>
<details>
   <summary>HTTP와 HTTPS  </summary>
<br />
</details>
<details>
   <summary>HTTP 요청/응답 헤더  </summary>
<br />
</details>
<details>
   <summary>HTTP와 HTTPS 동작 과정  </summary>
<br />
</details>
<details>
   <summary>CORS란  </summary>
<br />
</details>
<details>
   <summary>GET 메서드와 POST 메서드  </summary>
<br />
</details>
<details>
   <summary> 쿠키(Cookie)와 세션(Session) </summary>
<br />
</details>
<details>
   <summary> DNS </summary>
<br />
</details>
<details>
   <summary> REST와 RESTful의 개념 </summary>
<br />
</details>
<details>
   <summary>소켓(Socket)이란  </summary>
<br />
</details>

<details>
   <summary> Socket.io와 WebSocket의 차이 </summary>
<br />
</details>
<details>
   <summary>Frame, Packet, Segment, Datagram </summary>
<br />
</details>

<br>

# 3. JAVA

<details>
   <summary> JVM의 구조와 Java의 실행방식을 설명해주세요. </summary>
<br />
</details>

<details>
   <summary> GC가 무엇인지, 필요한 이유는 무엇인지, 동작방식에 대해 설명해주세요. </summary>
    <a href="https://github.com/kkyu-min/CS_MASTER/tree/main/JAVA/GC/README.md">[GC]</a>
<br />
</details>
<details>
   <summary> 컬렉션 프레임워크에 대해서 설명해주세요. </summary>
<br />
</details>
<details>
   <summary> 제네릭에 대해서 설명해주세요. </summary>
<br />
</details>
<details>
   <summary> 애노테이션에 대해서 설명해주세요. </summary>
<br />
</details>
<details>
   <summary> 오버라이딩과 오버로딩이 무엇이며 어떤 차이가 있을까요? </summary>
<br />
</details>
<details>
   <summary> 인터페이스와 추상클래스의 차이점에 대해 설명해주세요. </summary>
<br />
</details>
<details>
   <summary> 클래스는 무엇이고 객체는 무엇인가요? </summary>
<br />
</details>
<details>
   <summary> 정적(static)이란 무엇인가요? </summary>
<br />
</details>
<details>
   <summary> 자바의 원시타입들은 무엇이 있으며 각각 몇 바이트를 차지하나요? </summary>
<br />
</details>
<details>
   <summary> 접근 제어자의 종류와 이에 대해 설명해주세요. </summary>
<br />
</details>
<details>
   <summary> 객체지향에 대해서 설명해주세요. </summary>
<br />
</details>
<details>
   <summary> SOLID(객체지향 5대원칙)에 대해서 설명해주세요. </summary>
<br />
</details>
<details>
   <summary> 동일성(identity)와 동등성(equality)에 대해 설명해주세요. (equals(), ==) </summary>
<br />
</details>
<details>
   <summary> 원시타입과 참조타입의 차이에 대해 설명해주세요. </summary>
<br />
</details>
<details>
   <summary> String, StringBuilder, StringBuffer 각각의 차이에 대해 설명해주세요. </summary>
<br />
</details>
<details>
   <summary> Checked Exception과 Unchecked Exception에 대해 설명해주세요. 스프링 트랜잭션 추상화에서 rollback 대상은 무엇일까요? </summary>
<br />
</details>
<details>
   <summary> Java8에서 추가된 기능에 대해서 설명해주세요. </summary>
<br />
</details>
<details>
   <summary> try-with-resource에 대해서 설명해주세요. </summary>
<br />
</details><details>
   <summary> 강한 결합과 느슨한 결합이 무엇인지 설명해주세요. </summary>
<br />
</details>
<details>
   <summary> 직렬화와 역직렬화에 대해서 설명해주세요. </summary>
<br />
</details>
<details>
   <summary> 자바의 동시성 이슈(공유자원 접근)에 대해 설명해주세요. </summary>
<br />
</details>
<details>
   <summary> Mutable 객체와 Immutable 객체의 차이점에 대해 설명해주세요. </summary>
<br />
</details>
<details>
   <summary> 자바에서 null을 안전하게 다루는 방법에 대해 설명해주세요. </summary>
<br />
</details>
