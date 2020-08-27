# 네트워크

컴퓨터로부터 다른 컴퓨터로 데이터를 전송하는 것.

사람간의 Network -> 연결 관계, 인맥

사람들이 서로 Networking -> 상호작용, 대화



## OSI 7 Layer

https://www.youtube.com/watch?v=laBzCcF1414

A <-- 상호작용 --> B

​			(수단)

L4						대화

L3						언어

L2						말,글

L1						3M이내

OSI 7 Layer : 성공적인 상호작용을 위한 7가지 전제조건!

| User   | HTTP     |                                                     |
| ------ | -------- | :-------------------------------------------------: |
|        |          |                                                     |
|        | SSL      |                                                     |
| Kernel | TCP, UDP |                 Prot 번호, Process                  |
|        | IP       |    WAN <- Virtual, IPv4 주소(Host에 대한 식별자)    |
| H/W    | Ethernet | LAN = Private Network, Mac 주소 (NIC에 대한 식별자) |
|        |          |                                                     |



Socket = File + @(IP주소, Port ...)



## 연결지향, 비연결 프로토콜

연결지향 - 이미 연결되어 있기 땜누에 어떤 사람이 질의를 보냈는지 연결을 이용해 알 수 있음.

비연결 - 매번 새롭게 연결이 되기 때문에 필요한 경우 매 연결시 자신이 누구인지 알려줘야함. 



## 전송 계층

목적지 까지 데이터를 잘 도착하도록 하는 역할을 함.

대표적으로 TCP와 UDP



### TCP 프로토콜

TCP의 기능

- 신뢰성 있는 데이터 전송

- 연결 제어

- 흐름 제어

- 혼잡 제어.

  

#### Multiplexing / Demultiplexing

응용 프로그램이 소켓을 통해 데이터를 전송하는 것부터 TCP 프로토콜이 시작 됨.

한 컴퓨터에 여러 소켓과 프로세스가 존재할 수 있기 때문에 OS에서는 소켓과 프로세스를 식별하기 위해 **포트 번호**를 따로 둠.

보통 컴퓨터에 연결된 통신 링크는 하나이기 때문에 하나의 링크를 통해 여러 소켓의 데이터를 주고 받아야 함. 

이를 위해 출발지 포트 번호와 목적지 포트 번호를 따로 둠. 이러한 작업을 Multiplexing.

목적지에 도착한 세그먼는 헤더를 확인해 Demultiplexing 된 뒤 대상 소켓에게 데이터를 전달.



#### 신뢰성 있는 통신

잘못된 데이터를 전송받지 않고, 데이터의 순서 또한 보장되는 통신



#### 연결 제어

TCP에서 통신이 이뤄지기 위해서는 먼저 서로 연결이 되어야 하고, 서로 임의의 시작 순서 번호를 알려줘야 함. 이 과정을 3-way handshaking.

![image-20200724141615632](/Users/kakao/Library/Application Support/typora-user-images/image-20200724141615632.png)

연결 종료를 위한 4-way handshaking

![image-20200724141802694](/Users/kakao/Library/Application Support/typora-user-images/image-20200724141802694.png)



#### 흐름 제어와 혼잡 제어

흐름 제어: 송신량과 수신 처리량을 일치시키는 것.

수신 측이 처리할 수 있는 양만큼만 전송하도록 제어하는 서비스가 흐름제어.

이를 위해 수신 측에서 송신 측에게 데이터를 다 처리하고 있지 못하다는 피드백을 줄 수 있는 방법이 필요. 대표적으로 Stop and Wait 방식과 Sliding Window방식이 사용됨.

혼잡 제어: 네트워크가 혼잡하다고 판달될 때 데이터 송신량을 떨어뜨리는 것.

혼잡 상태가 일어났을 땐 보통 라우터의 버퍼가 **오버플로우 되어 패킷이 유실**되거나 라우터의 버퍼에 대기함으로 인해 **평소보다 큰 딜레이가 발생**.



### UDP 프로토콜

TCP에 기능들을 제공하지 않는 프로토콜. 그래서 부하가 매우 적다. 그렇기 때문에 많은 요청을 처리하고 신뢰성이 떨어져도 괜찮은 서비스에서 사용.



## 네트워크 계층

전송 계층에서 보내려는 패킷을 목적지 노드까지 도착시키는 역할.

중간 라우터를 통한 라우팅과 포워딩, 필요하다면 연결 설정을 담당.

- 라우터: 또 다른 라우터들과 물리적으로 연결 되어 있음. 라우팅은 현재 라우터에서 연결된 라우터 중 어떤 라우터로 보내는 것이 목적지로 가는데 최적인지 결정하는 것.

정적 라우팅

- 정적 라우팅이란 수동으로 라우팅 테이블을 만드는 방법
- 목적지 네트워크와 넥스트 홉을 하나하나 설정
- 정적 라우팅은 네트워크를 구성하는 모든 라우터에 대해 라우팅 설정이 필요
- 설정을 알기 쉽고 관리하기 쉽기 때문에 소규모 네트워크 환경에서 주로 사용

동적 라우팅

- 동적 라우팅이란 인접하는 라우터들이 라우팅 정보를 서로 교환하여 라우팅 테이블을 자동으로 만드는 방법
- 라우팅 정보를 교환하기 위한 프로토콜을 라우팅 프로토콜이라고 함
- 네트워크 환경의 변화대응과 장애 내구성 향상이 가능하기 때문에 중간부터 대규모 네트워크 환경에서 주로 사용