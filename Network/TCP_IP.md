## TCP/IP의 개념

TCP/IP는 패킷 통신 방식의 인터넷 프로토콜인 IP와 전송 제어 프로토콜인 TCP로 이루어져 있다.
IP는 패킷 전달 여부를 보증하지 않고, 패킷을 보낸 순서와 받는 순서가 다를 수 있다.
반면, TCP는 IP위에서 동작하는 프로토콜로 데이터의 전달을 보증하고 보낸 순서대로 받게 해준다.

따라서,
## 데이터의 정확성 확인은 TCP가 수행하고 패킷을 목적지까지로 전송은 IP가 담당한다.

그러면 TCP와 IP의 수행방식은 무엇일까??
TCP는 전송제어 프로토콜로 신뢰성이 없는 인터넷을 통해 종단간에 신뢰성 있는 바이트 스트림을 전송하도록
특별히 설계되었다. TCP는 송신자와 수신자 모두가 소켓이라고 부르는 종단점을 생성함으로써
이루어진다. TCP에서 연결 설정은 3-way handshake를 통해 이루어진다.

TCP는 가상 회선을 만들어 신뢰성을 보장하도록(흐름 제어, 혼잡 제어, 오류 제어) 하는 프로토콜로 
따로 신뢰성을 보장하기 위한 절차가 없는 UDP에 비해 속도가 느린편입니다.

## TCP의 특징
1. point - to - point : 한 쌍의 소켓끼리의 통신을 책임진다.
2. reliable, in-order byte stream: 신뢰성있고, 순서가 보장된다.
3. pipelined: window (한번에 쏟아붓기)
4. 양방향 통신
5. flow-controlled: receiver가 받을 수 있는 능력만큼 sender가 send
6. conjection control

데이터의 전송 단위
1. APPLICATION 계층 - Message
2. TCP 계층 - Segment(TCP Header + Data) (여기서 Data는 Application의 Message)
3. IP 계층 - Packet(IP Header + Data) (여기서 Data는 TCP계층의 Segment)
4. Link 계층 - Frame(Link Header + Data) (여기서 Data는 IP계층의 Packet)

## TCP 세그먼트의 구조
![img.png](img.png)


## TCP의 동작
![img_1.png](img_1.png)
TCP헤더의 Seq번호의 의미: 현재 세그먼트의 데이터의 가장 첫번째 byte의 번호
TCP헤더의 ACK번호의 의미: 예를들어 79라면 78번까지는 잘 받았고, 79번 byte를 기다릴꺼야.

데이터 유실 판단 ? TIME OUT
FEEDBACK이 오면 OK
아니면 데이터 유실 판단

그러면 TIMEOUT VALUE를 어느정도로 설정?
작게하면 reaction은 빠른대신 overhead
역은 반대

적당히 잘 잡아야함.

Round Trip Time : 어떤 세그먼트가 송신자로부터 출발해서 다시 돌아오는데 걸리는 시간 RTT
RTT보다 시간이 더 걸리면 유실, 아니면 ok

timeout = RTT로 판단?
RTT는 다 다름 (지나가는 경로가 다 다르기 때문에, 큐잉딜레이)

대표할만한 RTT값을 측정해 평균. EstimatedRTT  
실제로 사용하는 timeout 값: EstimatedRTT + DevRTT*4

- TCP reliable data transfer
1. timer 1개 씀
2. 파이프라인 segments
3. Cumulative ACKs

- fast retransmit 매커니즘
receiver의 ack가 연속으로 3번 같은 번호를 보내면 데이터 유실 판단 가능하다고 보는 매커니즘(총 4번임)
더 빠르게(효율적으로) 동작하게끔 하는 옵션 기능
























