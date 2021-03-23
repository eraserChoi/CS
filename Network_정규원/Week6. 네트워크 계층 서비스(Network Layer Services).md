# Week6. 네트워크 계층 서비스(Network Layer Services)

## 6 - 1 ) Overview
>  - 전송 계층은 원격에 있는 두 개의 프로세스가 서로를 구별하게 해주는 역할  
>  - 네트워크 계층 프로토콜의 역할은 원격에 있는 호스트를 구별하게 해주는 역할  
>  - TCP, UDP가 만드는 패킷은 segment, IP프로토콜이 만드는 패킷은 datagram이라고 부른다.   
>     두 단어 다 패킷을 나타내며 계층별로 만들어내는 패킷을 구별하려고 이름을 다르게 부른다.  
>  - 네크워크 계층의 역할은 datagram에 적혀있는 IP 주소를 보고 패킷이 목적지 컴퓨터까지 도달하게 하는 것이다.

#### 네트워크 계층의 핵심적인 기능
> - 라우팅 : 출발지부터 목적지 까지의 길을 설정해주는 것. 어떻게 가야할 지 거쳐가야하는 길까지 설정함.  
> - 포워딩 : 결정되어있는 라우터를 따라서 패킷을 옮겨주는 역할. 패킷을 다음 node로 전달해주는 기능.
> 

#### 기존 네트워크와 SDN(Software-Defined Networking)의 차이
> - 기존 네트워크 : 라우팅과 포워딩이 하나의 동일한 시스템 내에서 이루어짐  
> - SDN : 라우팅과 포워딩이 분리되어 있음.
>   > 각각의 라우터들은 포워딩 기능만 하고 길을 설정해주는 것은 라우팅 알고리즘만을 따로 떼어낸 중앙 집중적인 시스템이 있음
>   > 

## 6 - 2 ) Inside of Router
> 크게 Input port, fabric, output port로 나누어짐
> 
#### Input port Functions
> -  Physical layer : 데이터를 (1 or 0) 구별해주는 역할  
> -  Data link layer : 에러 체크 등 2계층의 프레임으로 만듦  
> -  Input Queue(buffer) : Switching fabric이 처리해야 될 데이터가 많으면 한꺼번에 처리할 수 없기 때문에 중간에 잠깐 저장하는 곳  
> 

> - **Queueing이 일어나지 않기 위해선 Switching fabric의 처리 속도가 모든 input port에서 들어오는 데이터를 합친 것보다 빨라야 함.**
> - **Input port Queuing**
> > - HOL(Head-of-the-Line) Blocking 지연
> > <p align="center"><img src="https://user-images.githubusercontent.com/76995452/112134169-c7d5ae80-8c0f-11eb-82ed-0b6b78ea51c7.png">
> > 

#### Switching Fabric Functions
> - Input buffer에 있는 패킷을 적절한 Output buffer로 내보내는 기능.
> - 메모리(memory), 버스(bus), 크로스바(crossbar) 방식이 있다.
> > 1. 메모리(memory) 방식 : 컴퓨터에 도착한 데이터를 주 메모리를 거쳐서 복사함. 비용적으로나 구현적으로나 간단함. 대신 처리속도가 매우 느림.   
> > 2. 버스(bus) 방식 : 메모리 방식의 속도제약을 완화하기 위해 나옴.   
> > Input port에 있는 버퍼와 output port에 있는 버퍼 간에 바로 직접 복사가 일어 날 수 있음.   
> > 특정 Input buffer와 쌍을 이루는 Output buffer가 특정 시간에 버스를 독점적으로 점유해야 하는 제약이 있음.   
> > 그래서 라우터, 스위치의 속도를 제약함.  
> > 3. 크로스바(crossbar) 방식 : 모든 input과 output쌍들이 동시에 전송이 가능함. 속도가 훨씬 향상되는 효과  
> > <p align="center"><img src="https://user-images.githubusercontent.com/76995452/112134175-c906db80-8c0f-11eb-9fb6-cd4e86a3ed73.png">
> > 

#### Output port Functions
> - **Buffering** : 유/무선 링크로 나가는 것보다 fabric으로부터 도착하는 Datagram이 많은 경우 발생  
> > - 이러한 현상을 **Output Queuing** 이라고도 한다.
> > - 버퍼 오버플로우가 일어나면 데이터 패킷 drop이 일어난다. drop이 일어나는 방식은 다음과 같다.
> > > - Tail drop : 버퍼가 가득차면 나중에 들어온 것 삭제  
> > > - Priority : 우선순위를 두고 우선순위에 따라 삭제  
> > > - Random drop : priority는 특정 사용자만 특혜를 보게되므로 아예 랜덤으로 삭제  
> - **Scheduling** : Buffering 된 데이터를 어떤 순서대로 처리할 것인지 판단하는 기능. 스케줄링 방식은 다음과 같다.    
> > - FIFO : 먼저들어온거 먼저 처리  
> > - Priority : 우선순위에 따라 처리  
> > - RR(Round-Robin) : 우선순위가 높은 버퍼, 그렇지 않은 버퍼를 번갈아가며 처리  
> > - WFQ(Weighted Fair Queuing) : 가중치가 있는 RR방식  


## 6 - 3)	Internet Protocol Overview  
> 라우팅 프로토콜, 라우팅 알고리즘들이 일을 하기 위해서는 결국 IP 프로토콜이 제공하는 정보가 필요함.  
> - IP가 발명된 계기 : 전세계 곳곳에 퍼져있는 미군과 통신하려고 하는데, 각 국의 통신 방식이 다르니까 이걸 하나로 아우를 수 있는 하나의 가상 네트워크를 만들자!  
> - IP는 소프트웨어적인 가상의 네트워크라고 볼 수 있다.

#### ICMP (Internet Control Message Protocol)   
<p align="center"><img src="https://user-images.githubusercontent.com/76995452/112138813-4d0f9200-8c15-11eb-96bd-5a6d666536a9.png">  
  
> - Ver (version) : 4비트, IP 버전을 뭘 사용하는지?   
> - Header length : 옵션 때문에 헤더의 길이가 8byte 이상이 될 수도 있어서 이를 명시할 목적으로 생김
> - Type of service : 데이터의 종류를 뜻하려고 구성했으나 잘 사용하지 않음.  
> - Length : 전체 데이터 그램의 길이  
> - **16-bit Identifier, flags, Fragment off set : 분할&재조립(Fragmentation & Reassembly)에 필요한 데이터**  
> - TTL(Time To Live) : 목적지에 도착할 때까지 최대 몇 hop을 거칠 수 있는지?   
> > hop수가 다 떨어졌는데도 목적지에 도달하지 못했다면 해당 데이터그램을 버리게 됨. 물론 계속 살아있다면 언젠간 목적지에 도착할 테지만 네트워크 효율성이 너무 떨어진다.   
> - Upper layer : 트랜스포트 계층의 프로토콜이 무엇인지 묻는 것 TCP냐 UDP냐? 이걸 묻는다고 생각하면 됨. 
> - Header checksum : CRC방식으로 이 곳에 데이터를 담아서 전달하면 헤더가 정확한지 아닌지를 알 수 있음.
> 

#### 분할&재조립(Fragmentation & Reassembly)  
- Fragmentation ID : 큰 데이터그램을 잘게 나누었을 때 동일한 ID를 부여해야 같은 목적지로 감.  
- Fragmentation offset : 잘게 나눈 데이터그램의 순서를 결정함.   
- Flag : 3bit를 차지하고 첫번째는 사용하지 않고 두번째는 자르지 말라는 표시 DF (Don’t Fragment), 세번째는 MF(More Fragment) 로써 이 뒤에 fragment가 더 있는지 없는지를 나타냄.  


## 6 - 4)	IP Addressing
> - IP 주소는 어떤 형식으로 만들어져 있으며 어떤 규칙에 의해 부여되는가? 
> - IP 주소는 계층화 되어있다.
> - ICANN(Internet Corporation for Asdsigned Names and Numbers) : 전 세계의 IP주소를 관리하는 기관.
> 

#### IP 주소 클래스
<p align="center"><img src="https://user-images.githubusercontent.com/76995452/112139918-af1cc700-8c16-11eb-9f83-2e382497cac5.png">    
  
  - 네트워크에 부여하는 주소는 클래스 A, B, C로 나눌 수 있는데, 공통점은 네트워크 파트와 호스트 파트로 나뉜다는 점이다.  
  > 네트워크 파트는 대한민국 IP 처럼 호스트 집단 전체를 대표하는 아이디이고, 호스트 아이디는 네트워크 관리자가 그 안에서 각각 자기 컴퓨터들에게 할당하는 ID이다.  
- 맨 앞이 0 이면 A, 10이면 B, 110이면 C
> A는 전세계에 128개, B는 전세계에 2^14개, C는 전세계에 2^21개 존재


#### 서브넷 (Subnet)
> - 클래스 B 주소를 받았다 하더라도 2^16개 정도의 node들을 하나의 네트워크로 관리하는 것은 너무 비효율적.    
> 그래서 이것을 임의로 나누어서 재무, 경영, 인사 담당 네트워크 등등등 논리적으로 나눌 수 있다는 개념이 바로 sub networking이다.   
> --> Divide and conquer  
> > 방법 : 호스트 넘버를 쪼개서 상위부분은 subnet Number, 하위는 Host Number 로 사용한다.    
> - 각 단체의 전산실 정책에 따라 몇 bits를 subnet Number로 쓸 것인지가 달라진다.   
> > ex1) 255.255.254.0 이라고 되어있는 것은 앞에 7bit를 서브넷 ID로 쓰겠다는 이야기  
> > ex2) 255.255.255.0이면 앞 8bits를 서브넷 ID로 쓰겠다는 이야기  
> > Q. 255.255.248.0 이면 총 몇 bit가 네트워크 ID로 간주가 되는 걸까요? 그 중 서브넷 ID는 몇 bit인가요? 
> > 
> - 클래스 C같은 경우에는 네트워크 자체가 하나의 서브넷 마스크로 사용되는 형태도 있을 수 있음.
> 

#### CIDR(Classless Inter-Domain Routing)   
> - 발명 계기 : '클래스 주소 C를 뭉쳐서 클래스 B에 가까운 형태로 쓸 수 있지 않을까?'  
> - 서브넷하고 반대되는 개념. Supernetting이라고 부르기도 함.   
> - 낮은 레벨의 작은 네트워크 여러 개를 모아서 하나의 네트워크처럼 보이게 하는 것.  
> --> 좀 더 많은 호스트를 한꺼번에 수용할 수 있게 된다.  
> - 
> <p align="center"><img src="https://user-images.githubusercontent.com/76995452/112140832-df189a00-8c17-11eb-86eb-d880911c8051.png">  
>    
> > --> 이렇게 하면 클래스 C도 2^10개 의 호스트를 가질 수 있게 된다. 그래서 각각 서브넷 1~4 해서 쓰면 된다.
> > 


## 6 - 5)	Datagram Forwarding
> 크게 Destination-based forwarding과 Generalized forwarding 이 있다.
> 

#### Destination-based forwarding
> - 목적지 주소를 보고 목적지 주소에 따라 적합한 node를 다음 node로 결정해서 보내는 것.
> - 기존 네트워크의 포워딩 방식이다.
> 40억개가 넘는 IP주소가 있기 때문에 모든 IP주소를 담지 않고 네트워크 아이디만 담아서 전달한다.  
> 근데 클래스 C같은 경우는 네트워크도 2^21개다. 그래서 destination address를 range를 둔다.  
>  > <p align="center"><img src="https://user-images.githubusercontent.com/76995452/112142416-eb055b80-8c19-11eb-87e3-a0d8f26e301d.PNG">   
>  > 
> - Longest prefix matching 
>  > <p align="center"><img src="https://user-images.githubusercontent.com/76995452/112142592-1f791780-8c1a-11eb-85c1-55cd662fbb8f.png">   
>  > 
>  > 첫번째 DA를 가진 것은 2번으로 두번째 DA를 가진 것은 1번으로 갈 것이다.

#### Generalized forwarding
> - 정책적인 것들이나 상황적인 것들을 고려해서 포워딩을 한 것을 일반화된 포워딩. Generalized forwarding이라고 한다.
> - SDN의 포워딩 방식이다.
