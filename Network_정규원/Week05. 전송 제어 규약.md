# 전송 제어 규약 (Transmission Control Protocol)

## 5 - 1) Transmission Control Protocol 
> -	Connection-oriented service
> -	Pipelined transmission
> -	Full-duplex connection
>   > sender 와 receiver가 지정되면 그 상태로 쭉 결정되는 것이 아니라 양쪽에서 서로 데이터를 주고 받을 수 있음을 의미함.  
>   > Bi-directional connection

* #### MSS
> Segment 가 너무 크게 되면 하부레벨에서도 TCP 자체에서도 통신 간에 공평성이라든지 이런 것을 제공하기 어려워져서 연결을 수립할 때 segment의 최대 사이즈를 결정하게 됨.  
> 이걸 Maximum Segment Size. MSS라고 함. 
> 

### TCP segment 구조
> <p align="center"><img src="https://user-images.githubusercontent.com/76995452/110386309-7839a380-80a3-11eb-8286-0d4b7379cf53.png"></p>  
> 
> * 다중화, 역다중화를 하기 위해 필요한 것이 포트 넘버
> * Data offset 
>   > udp length와 비슷하나, udp length는 헤더 길이 + 데이터 길이 이고, data offset은 데이터가 어디서부터 시작하는 지 알려주기만 함. 즉 header length랑 같음.
> * Res
>   > reserve // 다음에 또 필요하면, TCP에 담을 정보가 있다면 여기에 담겨짐.
> * Sequence number
>   > 현재 segment가 담고 있는 데이터가 전체에서 어느 부분에 해당하는지를 가리킴.
> * Acknowledgement number 
>   > receiver가 다음에 받아야 되는 segment의 Sequence number을 전달함.
> <p align="center"><img src="https://user-images.githubusercontent.com/76995452/110386310-78d23a00-80a3-11eb-86cb-0289490b5b6e.png"></p>     
> 
>   > - Go-back-N과 비슷해 보일 수는 있지만 순서에 맞지 않게 도착한 패킷을 버리지 않고 버퍼에 보관한다는 의미에서 차이가 있다.
> * Window size
>   > 수신버퍼의 잔여 크기를 여기에 담아서 보내면 sender는 이보다 큰 데이터를 보내지 않는다. 보통 4kb 정도다.
> * flags
>   > * URG, ACK, PSH, RST, SYN, FIN 이렇게 6개
>   > * URG, PSH는 잘 사용하지 않고, ACK는 Acknowledgement에 유용한 값이 들어있는지를 나타내기 위한 flag이다.
>   > * SYN
>   >   > <p align="center"><img src="https://user-images.githubusercontent.com/76995452/110386316-7a036700-80a3-11eb-8faf-19591d5ff95b.png"></p>    
>   >   > 
>   >   > SYN flag는 connection-oriented인 TCP의 3-way handshake에 사용된다.
>   > * FIN
>   >   > 연결을 끊고 싶을 때 사용됨. 주의할 점은 클라이언트가 연결을 끊었어도 서버에서는 클라이언트에게 줄 데이터가 남아있어 계속 연결하고 있을 수도 있다.   
>   >   > 양쪽에서 모두 FIN flag를 1로 해서 보내야 양방향 통신이 종료된다.
>   > * RST
>   >   > 송신자가 특정 포트 번호를 호출했으나, 해당 포트가 없는 경우 다시 수정해서 보내라는 뜻으로 사용된다.

### Timeout
>  <p align="center"><img src="https://user-images.githubusercontent.com/76995452/110386312-796ad080-80a3-11eb-997f-a9bf1c95bff6.png"></p>   
>  
>  *  TimeoutInterval은 RTT보다는 길어야 함.  
>  * #### 위 방식대로 설정한 타임아웃이 길어서 Throughput이 낮아진다면?
>  > --> 3 duplicate ACKs 메커니즘을 통해 이를 방지한다.
>  > <p align="center"><img src="https://user-images.githubusercontent.com/76995452/110386313-796ad080-80a3-11eb-9f52-a9bbecb50784.png"></p>
>  > 

## 5 - 2) Congestion Control
> * Congestion
>   > 너무 많은 전송자가 너무 많은 데이터를 너무 빠르게 전송해서 네트워크가 감당하지 못하는 현상.
> * flow control이랑 congestion control의 차이
>   > Flow control은 송 수신자간의 관계에서 receive buffer를 알려주면 해결이 됐는데 congestion control은 네트워크를 공유하는 모든 node들이 서로 양보를 해야 함.
> * End-to-end 방식과 network-assisted 방식이 있다.
>   >  * End-to-end  
>   >   > + 라우터가 관여하지 않고, 호스트들이 자기가 보낸 데이터가 얼마나 잘 도달하는 지를 관찰해서 네트워크 혼잡을 판단하고 맞는 동작을 취함.   
>   >   > + 대표적으로 TCP가 이 방식을 채택함.
>   >  * Network-assisted
>   >   > + 여러 개의 src는 중간의 라우터를 거치게 되는데 이 라우터가 호스트들한테 혼잡도를 말하고 송수신하는 데이터 양을 줄이라고 하는 방식.  
>   >   > + 대표적으로 ATM기기가 이 방식을 채택함.
>   >   > 

### AIMD (Additive Increase Multiplicative Decrease)
> * Congestion control 의 철학 AIMD
> * Additive Increase 
>   > cwnd (congestion window) size를 문제가 없을 때는 천천히 1씩 증가 시키다가
> * Multiplicative Decrease 
>   > 혼잡을 감지했다면 절반으로 줄여버린다.
>   > 

* #### Slow Start
 > 1MSS로 시작해서 이 segment에 대한 ack를 잘 받으면 이것을 두 배로 늘림.
 > <p align="center"><img src="https://user-images.githubusercontent.com/76995452/110386317-7a036700-80a3-11eb-802f-b69142e4e64e.png"></p>
* #### Congestion Avoidance
> congestion이 일어나기 전까지의 cwnd size의 절반을 Slow start threshold로 설정함.
> 

## 5 - 3) TCP Congestion Control Algorithm
> <p align="center"><img src="https://user-images.githubusercontent.com/76995452/110386318-7a9bfd80-80a3-11eb-8141-aab6dba5559c.png"></p>
> 
> * 이 중에서 Standard로 지정된 4개를 알아보자.
> 

1. #### TCP Tahoe(1988)  
>  * Slow start, congestion avoidance, fast retransmit 
>  * congestion avoidance 때 congestion window를 1로 확 줄여버림. 그래서 throughput이 확 줄어듦
>  * timeout이랑 fast retransmit이랑 구별이 없었음.
>  <p align="center"><img src="https://user-images.githubusercontent.com/76995452/110386320-7a9bfd80-80a3-11eb-8612-64ca0941a92f.png"></p>
>  
>   > SS : Slow Start, CA : Congestion Avoidance

2. #### TCP Reno(1990)
>  * Congestion이 timeout만큼 심한 상황이 아니라는 것을 반영함. 
>  > 3 duplicate ACK는 error가 발생한 특정 패킷을 제외하고 다음 패킷들은 여전히 잘 가고 있다는 뜻이기 때문.
>  * Timeout이 일어날 때는 cwnd size를 1로 줄이되, fast retransmit의 경우에는 cnwd size를 절반으로 줄임.
>  <p align="center"><img src="https://user-images.githubusercontent.com/76995452/110398092-7af1c400-80b6-11eb-8512-7d4156f6897b.png"></p>
>  
>   > FR : Fast Recovery phase
>   >   > Cwnd size를 반으로 줄이고 loss를 발견하기 까지의 non-duplicate ACK이외에 새로운 ACK를 받을 때까지 대기 하는 것.
>   >   >  <p align="center"><img src="https://user-images.githubusercontent.com/76995452/110386300-766fe000-80a3-11eb-8d28-4544c30008eb.png"></p>
3. #### TCP NewReno(1999)
> * network에서의 error는 개별적으로 발생하기 보다는 연속적으로 발생하는 경우가 많음
> * 그러다 보니 기존 TCP Reno에서는 첫번째 error 때문에 1/2로 줄인걸 두번째 error때문에 또 1/2. 즉, 1/4로 줄이게 된다. 
> * 이를 막기 위해 TCP Reno의 FR 메커니즘을 개선한 것이 TCP NewReno다.
> <p align="center"><img src="https://user-images.githubusercontent.com/76995452/110398678-ab862d80-80b7-11eb-88cb-da05effa2351.png"></p>
4. #### TCP SACK(1996)
> * SACK : Selective ACK
> <p align="center"><img src="https://user-images.githubusercontent.com/76995452/110398798-e8eabb00-80b7-11eb-87f6-b72864106187.png"></p>
> 

<br>

## 5 - 4) TCP vs UDP 
> <p align="center"><img src="https://user-images.githubusercontent.com/76995452/110399107-9067ed80-80b8-11eb-9e4f-dc3a3e6f55a9.png"></p>

***

#### Keyword
> - 연결지향(connection-oriented)
> > 송/수신기 사이의 물리적인 연결이 아닌 논리적인 연결을 의미하는 개념
> - 핸드셰이크(handshake)
>  > 통신 관련 분야에서 둘 이상의 장치가 연결/단절을 위해 선행하는 약속된 협상 과정
> - 최대 세그먼트 크기(Maximum Segment Size, MSS)
> > TCP가 세그먼트 한 개로 보낼 수 있는 최대 데이터 크기
> - 전이중 통신(full-duplex)
> > 송신과 수신이 동시에 가능한 통신 방식
> - 혼잡 윈도우(congestion window)
> > 송신측에서 ACK 수신 없이 연속적으로 전송할 수 있는 최대 데이터 양
>  - AIMD (Additive Increase and Multiplicative Decrease)
> > 혼잡 윈도우(congestion window)를 증가시킬 때는 선형적으로, 감소시킬 때는 지수적으로 감소시키는 TCP 혼잡제어의 기본 원칙 
