# 4. 전송계층 서비스 (Transport Layer Services)
## 4 - 1) 전송 계층 서비스 (Transport Layer services)
* 용어정리
> * 프로그램 
>   > 디스크에 저장된 실행파일.  
> * 프로세스 
>   > 프로그램을 실행한 어떤 Instance. 하나의 프로그램으로 여러 프로세스를 띄울 수 있음.  
>   > 각각의 프로세스는 각각의 사이트에 접속해서 정보를 가져 오는 역할을 함. 
> * 스레드(thread) 
>   > 프로세스가 동작하는 여러가지 일들이 있는데 이 일을 하나의 프로그램으로 짜면 동시에 운영하기가 어렵기 때문에 이것을 몇 개의 블록으로 나눈 것이 스레드다.   
>   > 카카오톡으로 치면은 내가 타이핑하는걸 받아들이는 쓰레드, 그리고 카톡을 화면에 띄우는 쓰레드 등등 이것들이 나눠져 있음.
> * frame, datagram, packet, segment 는 다 비슷한 의미다. 전송계층에서의 정보 단위는 segment라고 한다.  

<br>  

* **전송 규약 (Transport protocol)은 여러가지가 있지만 인터넷에서 사용하는 것은 TCP와 UDP가 대표적이다.**
> **TCP**
>   > -	Reliable하고 in-order delivery다. 전송하는 사람이 보낸 순서 그대로 송신자에게 도착한다.  
>   > 이는 응용 프로그램의 입장에서 본 것이며 실제로 컴퓨터에 순서대로 도달한다는 뜻은 아니다.
>   > -	Connection-oriented service.
>   > -	에러 수정, 데이터 흐름 제어 등 안정적인 서비스를 위함

> **UDP**  
>   > -	Unreliable. 에러가 섞여 있을 수도 있고, 패킷이 빠져있을 수도 순서가 좀 어긋나 있을 수도 있음. 
>   >좀 간단하게 전달하는 것이 UDP 라고 보면 됨.
>   > -	Connectionless service
>   > -	에러 수정, 데이터 흐름 제어 같은 기능이 없음. 대신 TCP보다 빠른 속도를 제공 할 수 있음.

<br>

## 4 - 2)	Multiplexing and Socket
* 용어정리
> * 다중화(Multiplexing) 
>   > 여러 서비스들을 동시에 하나의 링크로 내보내는 작업.
> * 역 다중화(Demultiplexing) 
>   > 섞여서 쭉 날아온 데이터들이 목적지 컴퓨터에 도달하게 되고 각각에 맞는 프로세스로 나뉘어서 전달 되는 작업  
>
>  #### 다중화, 역 다중화 모두 전송 계층에서 제공 함.  
>  
>  * 포트 번호(Port Number) 
>   > 어떤 클라이언트가 보낸 데이터인지 전송계층이 구별할 수 있게끔 하는 정보    
>  * Socket 
>   > API들의 집합. 전구를 소켓에 끼우기만 하면 불이 들어오듯이 우리도 API가 제공하는 parameter 규격에 맞게끔 데이터를 넣어주면 데이터가 전달 됨.  
<p align="center"><img src="https://user-images.githubusercontent.com/76995452/110374969-af548880-8094-11eb-9581-34e0c58629c7.png"></p>  
  
<br>
  
## 4 - 3)	User Datagram Protocol (UDP)
> 부가적인 기능 제공 x. 다중화, 역 다중화만 제공. connectionless service.  
>  UDP는 congestion control 기능이 없기 때문에 어플리케이션이 보내려고 하는 데이터가 있으면 눈치 보지 않고 원하는 만큼 보냄.  
<p align="center"><img src="https://user-images.githubusercontent.com/76995452/110374972-b085b580-8094-11eb-9e2e-3dec235791b8.png"></p>     

* Checksum :  전체 UDP segment에 에러가 포함되어 있는지 있지 않은 지를 판단하는 근거를 제공하는 필드. 16bit의 integer 값  
  > * Sender와 receiver가 만들어낸 checksum 사이에 차이가 없다면 문제가 발생하지 않았다는 것.  
  >   차이가 있다면? 전달 되는 동안에 데이터나 헤더의 일부가 변경되었다는 뜻  
  > * checksum 생성 순서
  >   >  *1*. 맨 첫번째 소스포트부터 16bit 단위로 sender가 일단 자른다.   
  >   >   *2*. 첫번째 16bit 와 두번째 16bit를 합산을 한다.  
  >   >   *3*. 이를 1의 보수를 취한다. 1의 보수를 취하는 까닭은 checksum과 sum을 더했을 때 1이 되게끔 하려는 의도다.  
  >   >   

<br>

## 4 - 4)	Reliable Data Transfer Principles 
>  * 신뢰성 있는 전송?
>   > 하위에 있는 에러가 응용 프로그램에서 보이지 않도록 감춰주는 것이 신뢰성 있는 전송의 역할이라고 볼 수 있다.   
>   > ex) 회사 내 모든 결재 건을 사장이 담당하지 않고 비서나 중간 관리자가 체크를 해서 문제가 없는 것만 결재를 올리는 것이다. 
>  * 인터넷에서 발생 할 수 있는 에러 타입은 크게 **비트 에러(bit error)와 패킷 로스(packet loss)** 이다.
>  

* #### 비트 에러 (bit error)
> * 비트 에러는 checksum을 활용하여 검증함.   
> 비트 에러가 없다고 하면 수신자가 송신자한테 ACK(ACKnowledge)를 보내게 되고, 이 ACK를 받지 못하면 제대로 도착하지 않았다고 판단하게 됨.  
* #### 패킷 손실 (packet loss)
> * 패킷 손실의 경우 아예 둘 사이의 패킷이 사라졌기 때문에 수신자 측에서는 알 방법이 없음. 
>   > - 그래서 도입된 개념이 타임아웃(timeout)
>   <p align="center"><img src="https://user-images.githubusercontent.com/76995452/110374979-b11e4c00-8094-11eb-9106-0fb92b3e9101.png"></p>  
> * Reliable한 데이터 전송 프로토콜들은 정해진 시간을 초과하게 되면 패킷이 중간에 분실되었다고 판단하고 패킷을 재전송 하게 됨.
>   > - 그런데 데이터가 정상적으로 도달했는데 ACK 신호가 전달되는 과정에서 손실된 경우 똑같은 메시지를 두 번 보내고 받는 경우가 발생함.  
>   > --> 그래서 패킷마다 일련번호가 있음.  
>   > - 원래 데이터 중복을 막으려고 만들어진건 아니고 큰 사이즈의 데이터가 생겨나다보니 여러 개의 segment에 나눠 보내야해서 도입된 개념. 근데 이게 중복도 막을 수 있는 것을 발견.
>   <p align="center"><img src="https://user-images.githubusercontent.com/76995452/110374981-b1b6e280-8094-11eb-90c6-408fdd0c54b6.png"></p>  
> * 이렇게 패킷을 재전송하는 방식을 ARQ (Automatic Repeat reQuest)라고 함.
>   > + **stop and wait** : 한번에 하나씩 segment를 보내고 검사 받고 보내고 검사받고 하는 방식
>   >   ><p align="center"><img src="https://user-images.githubusercontent.com/76995452/110374983-b24f7900-8094-11eb-9dd6-fe566a721758.png"></p>     
>   >   >
>   >   >* RTT(Round Trip Time)이 30ms고 그 중에 데이터가 전달되는 전송지연 시간은 8μs 라고 한다면 U 는 0.00027  
>   >   >* 0.027% 정도만 데이터를 전송하는데 사용한다는 이야기           
>   >   > --> stop and wait 방식은 물리 자원을 굉장히 낭비하게 되는 문제가 있음    
>   > 
>   > - **pipelining method** : 여러 데이터를 한꺼번에 보내고 한꺼번에 검사받는 방식
>   >   > <p align="center"><img src="https://user-images.githubusercontent.com/76995452/110374984-b24f7900-8094-11eb-89e6-c0a277bd80f4.png"></p>  
>   >   > 
>   >   >   > 이렇게 pipelined protocol을 사용하면 효율이 늘어남. 30개 300개 를 하면 30배 300배 효율이 증가함.  
>   >   > 
>   >   > - go-back-N
>   >   > - selective repeat
>   >   > 

### Go-back-N과 selective repeat의 차이점
*	Go-back-N
> * cumulative ACK
>   > 송신자 입장에서 데이터를 전달하다가 중간에 수신자가 판단했을 때 n번째 데이터가 잘못 됐다고 한다면 n번부터 그 이후까지 모두 재전송 함.  
> * 개별적인 타이머가 필요 없이 가장 먼저 보낸 패킷에 대해서 타이머가 설정되어 있음.
>   > 타임 아웃이 일어난 패킷부터 재전송하면 됨.
>  <p align="center"><img src="https://user-images.githubusercontent.com/76995452/110374985-b2e80f80-8094-11eb-8ff9-eff23060b816.png"></p>   

* Selective repeat
> * 개별적인 ack를 사용
>   > n번째만 재전송하는 것이 가능함.
> * 모든 패킷에 대해서 별도의 개별적인 타이머를 갖고 있음
>   > --> 타임 아웃이 일어난 패킷만 재전송하면 됨.
>  <p align="center"><img src="https://user-images.githubusercontent.com/76995452/110374986-b2e80f80-8094-11eb-9373-e10141c2703e.png"></p>
>  

### Window size와 sequence number
<p align="center"><img src="https://user-images.githubusercontent.com/76995452/110374989-b380a600-8094-11eb-9a07-6fc10c0bb129.png"></p>
