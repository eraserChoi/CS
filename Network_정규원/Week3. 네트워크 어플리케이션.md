# 네트워크 어플리케이션
## 3-1) Principle Application  
어플리케이션? == 응용프로그램

#### 네트워크 응용프로그램
> - 이메일
> - 웹 프로그램(웹 서버, 브라우저 등)
> - P2P 파일 공유 프로그램
> - SNS 프로그램
> - 메신저
> - 온라인 게임
> - 유튜브, 넷플릭스 등 스트리밍 프로그램  

#### 특징
> - End System에서 돌아가며 다른 End System과 통신을 함.
> -	중간에 있는 라우터 같은 인터넷 토킹 장비에서 실행할 필요가 없음.

### 네트워크 어플리케이션의 구조
> **1. 클라이언트 서버 모델**  
> **2. P2P 모델**   
<center><img src="https://user-images.githubusercontent.com/76995452/108051573-66f60c00-708e-11eb-9176-03dff1282ee9.png"></center>
  

#### 클라이언트 서버 모델의 특징
> - 서버가 항상 켜져있어야 함.
> - 서버는 고정된 IP 주소를 갖고 있어야 함.
> - 클라이언트는 인터넷에 연결만 되면 가능 + 서버와 다르게 주소가 변동되어도 됨.
> - 항상 클라이언트가 먼저 통신 시도, 데이터 요청.

#### P2P 모델의 특징
> -	특정한 서버가 존재하지 않음.
> -	모든 디바이스가 서버가 될 수도, 클라이언트가 될 수도 있음.
> -	서로 직접적으로 연결되어 통신을 함
> -	Self scalability (클라이언트 수가 많아지더라도 서비스를 지속적으로, 안정적으로 할 수 있다.)   
피어의 수가 늘어나는 만큼 데이터 요구량도 늘어나지만, 거기에 맞춰 데이터 용량도 늘어남. 항상 scalable 함.


#### 인간의 의사소통과 네트워크 어플리케이션의 프로토콜은 서로 닮아있다.
> - **Syntax**  
주어나 서술어가 어디에 위치해야 된다 등 문법적인 내용   
  -->	전체 메시지에 어떤 필드들이 존재 하는지, 몇 byte를 요구하는 데이터를 명시하는 필드가 필요하다든지
> - **Semantics**  
의미론. What time is it이면 시간을 물어본다는 의미고, time 대신에 다른 게 들어가면 다른 걸 물어본다는 의미. 이렇게 단어마다 가지는 의미를 Semantics라고 함.  
-->	실제 필드에 담기는 데이터를 어떻게 해석할 것인가.
> - **Pragmatics**  
화용론. 말의 순서. 질문을 받고 대답을 한다 등의 규칙.  
-->	어떻게 응답할 것인지, 어떤 순서로 응답할 것인지.

#### 네트워크 어플리케이션이 요구하는 특성들  
> ![그림2](https://user-images.githubusercontent.com/76995452/108051578-69586600-708e-11eb-9c47-1ff55d6fa0a3.png)  
> **이러한 requirement를 누가? --> Transport layer protocols가 만족시켜준다.**  
> **대표적으로 TCP/UDP**

#### TCP
> -	Error control : 에러가 있는 데이터는 재전송을 계속 요구하여 에러가 없는 데이터가 도착했을 때 애플리케이션 레이어에 전달을 해준다.  
> -	Flow control : 리시버가 받을 수 없는 용량 이상의 데이터를 보내지 않도록 함.  
> -	Congestion control : 라우터나 스위치 등 인터넷 토킹장비들에 데이터가 쌓이지 않도록 제어하는 것.  
> -	Reliable

#### UDP
> -	Error, Flow, Congestion 등의 control 능력은 없지만 트랜스포트 레이어 프로토콜의 기본적인 기능을 함. 
> -	오디오나 비디오는 에러가 있을 때 긴 지연시간이 발생할 수 있는데, UDP는 그냥 화면이 깨지더라도 전달을 함. 
> -	TCP보다 전반적으로 속도가 빠름.  

<br>
<br>  

## 3-2) 웹과 HTTP
> 웹(WWW) – 팀 버너스 리 가 1990년에 처음 제안하여 만들어 짐.  
> HTTP (HyperText Transfer Protocol)  


![그림3](https://user-images.githubusercontent.com/76995452/108051586-6a899300-708e-11eb-8263-cd4fdd5665df.png)  
> TCP 연결을 하는 데 RTT 한번, file requesting에 RTT 한번 해서 총 두번  
> 2RTT + file transmission time => **total response time**


### HTTP 버전  
> - **HTTP/1 : non-persistent HTTP**  
이미지, 텍스트, 동영상 오브젝트를 전달하는 데 TCP 연결이 별도로 하나씩 필요했음.  
> - **HTTP/1.1 : persistent HTTP**  
TCP 연결을 끊지 않고 열어두었다가 다음 오브젝트가 요청되면 그 TCP 연결을 또 사용함.  
response 와 request가 순서대로 날아가고 순서대로 날아옴. 앞선 request에 대한 response가 안왔다면 지연시간이 약간 더 발생  
> - **HTTP/2 : Asynchronous order를 허용**  
한 페이지 안에 여러 오브젝트가 있더라도 이들을 한꺼번에 요청 가능  
  
### HTTP 메시지의 구조  

> ![그림5](https://user-images.githubusercontent.com/76995452/108051607-6f4e4700-708e-11eb-9604-e90f61c656a4.png)  

### response code
> ![그림6](https://user-images.githubusercontent.com/76995452/108051608-6fe6dd80-708e-11eb-8db2-525cc67e650e.png)  
> 200 : ok  
> 301 : user가 요구한 오브젝트는 다른 곳으로 옮겨졌고, 그 오브젝트로 이동하겠다.  
> 400 : user가 요청한 request를 이해하지 못하겠다.  
> 404 : 요청한 request를 찾지 못했다. 없다.  
> 505 : HTTP 버전이 달라서 user와 통신할 수 없다.    

### REST (REpresentational State Transfer)
> 서버는 클라이언트에 대한 상태를 저장하지 않아도 HTTP request message에 다 담겨있다. 이런 구조를 따르는 서비스를 RESTful이라고 한다.
  
  #### REST 구조의 유의사항
> -	클라이언트 서버구조 : 실제 데이터와 유저에 대한 정보가 분리되어 있어야 함.
> -	Statelessness : 클라이언트의 상태(state)를 서버에 저장하지 않는(less) 것(ness)
> -	Cacheability : 서버의 response가 클라이언트 or 중간의 웹 캐시 같은 데에 저장할 수 있어야 함.
> -	Layered system : 클라이언트가 접속할 때 서버에 직접 접속이 된 상태인지 중간의 웹 프록시 서버에 접속된 건지 구별할 수 없어야 함. ➡ 서비스를 이용하는 데 차이가 없어야 함.
> -	Code on demand (optional) : 데이터를 해석하고 사용할 수 있는 응용프로그램까지 전달 해준다는 개념.
> -	Uniform interface : 특정한 아키텍쳐에 제약받지 않아야 한다.  

<br>
<br>  

## 3-3) 쿠키와 웹 캐싱  
### 쿠키(Cookies)
> HTTP는 로그인 정보 등 상태가 저장되지 않기 때문에 쿠키(Cookies)를 개발함.  

![그림7](https://user-images.githubusercontent.com/76995452/108051610-6fe6dd80-708e-11eb-85f0-19db8ca6ad0b.png)  

### 웹 캐싱 (Web Caching)  
 > - 클라이언트가 request하고 서버가 이에 대해 보낸 데이터를 중간의 프록시 서버가 저장하고 있음.   
   ➡ Server로 가는 오버헤드를 줄여줌. 
 > - 클라이언트의 request가 직접 서버에 갈 필요 없기 때문에 응답시간이 매우 짧아짐.  
 > - 서버 입장에서는 프록시 서버가 어느정도 처리를 하기 때문에 용량이 작더라도 서비스를 잘 할 수 있음.  
 > - 로컬 ISP에서 인터넷으로 연결되는 부분에서 response와 request가 쌓이면 병목현상이 초래되는데 프록시 서버가 이를 방지해줘서 전체적으로 서비스가 원활해짐.  

## 3-4) SSL/TLS
> TCP연결에 암호화를 제공하는 방법에는 SSL 또는 TLS가 있다.  

- **SSL(Secured Socket Layer)** : 애플리케이션 레이어에 해당하는 프로토콜. TCP에 얹혀져서 HTTP에 암호화 기능을 제공하는 프로토콜    
![그림8](https://user-images.githubusercontent.com/76995452/108051612-707f7400-708e-11eb-8cc6-ff1baf341c3e.png)

- **TLS(Transport Layer Security)** : SSL이 발전된 형태. 강력한 보안을 제공하나 SSL보다 속도는 느림.    

<br>
<br>  

## 3-5) E-Mail  

### 구성요소 
> -	User agents : 우리가 메일을 작성하는 프로그램  
> -	Mail servers : g-mail이나 네이버 등  
> -	Protocols : SMTP, POP3, IMAP   


#### Mail server 구성요소  
> -	Mail box : 외부에서 받은 데이터가 저장되는 곳. User가 접속할 때 그 데이터를 전달해준다.  
> -	Message queue : 외부로 보낼 메시지가 여기에 저장됨. 연결이 성립되면 그 때 메시지를 보냄.  
> 각 메일 서버는 SMTP(Simple Mail Transfer Protocol)라는 프로토콜을 써서 통신을 함.    
> 서버에서 메일을 가져올 때는 **Mail Access Protocol** 사용  

#### Mail Access Protocol  
> POP3, IMAP, HTTP 등이 있다.    
> - POP3는 데이터를 가져오면 서버에 있던 데이터를 다 지우게 됨.  
> - IMAP은 Internet Mail Access Protocol의 약자로 POP3와 다르게 데이터를 서버에 온전히 남겨두고 이 메일박스에 있는 내용들을 폴더처럼 정리할 수 있음.  
➡ 언제 어떠한 디바이스를 가지고 접속을 해도 항상 똑 같은 형태를 볼 수 있는 Synchronization 기능이 제공됨.   
주기적으로 메일을 다운 받을 수 있음.  
서버의 오버헤드는 좀 클 수 있으나 사용자 입장에선 편리  
> - HTTP는 ‘웹 기반’으로 이메일 쓸 때 유저에서 서버로 가거나 서버에서 유저로 데이터를 보내는 경우 쓰게 됨.  

<br>
<br>  

## 3-6) Domain Name System    
> 서버의 이름을 기억하지 주소는 기억하기 힘듦. 그렇기 때문에 이름만 알고도 접속할 수 있게끔 만들자 해서 나온게 DNS. 도메인 네임 시스템  
> - 효과 : 각각 클라이언트에 요구하는 로드를 분산 시킬 수 있음. (load distribution)    
> - 어떻게? : 요즘은 데이터 센터에 서버가 여러대. 그러므로 각각의 서버는 IP주소가 다름. 근데 같은 도메인 네임을 사용한다. (ex. 구글)   
> ➡ 구글에 대한 어떤 request를 받았을 때 DNS 서비스는 여러 서버에 대한 IP 주소를 번갈아서 주게 되면 결국 request load가 분산되는 효과를 얻을 수 있음.

#### 왜 DNS를 중앙 집중하지 않는지?
-	Single point of failure : 한 군데에 몰려있으면 하나 고장나면 전체가 다 고장.   
일부 유저는 가깝고 많은 유저들은 멀리 있음. ➡ 지연시간이 길어짐 / 트래픽이 한군데에 몰리면 서비스가 원활하지 않음.   


#### TLD (Top-Level Domain) Servers
> - Authoritative Server : 한 기관에서 내부에 있는 서버들의 IP주소를 관리할 필요가 있을 때 따로 만들어 두는 데이터 베이스  
> - Local DNS Server : 클라이언트 입장에서 처음 접속하는 서버. 이 DNS 서버에게 내가 원하는 IP주소를 물어보고 Local이 모르면 root나 TLD로 가서 알아옴.  
> - 왼쪽은 Iterated query, 오른쪽은 recursive query.  
> Recursive query는 root에 오버헤드가 심해질 수 있어서 DoS 공격에 취약. 추천되지 않음.  
> ![그림1515](https://user-images.githubusercontent.com/76995452/108058139-ee477d80-7096-11eb-9e89-6d70991dd27c.PNG)

#### DNS 공격 유형
> Root는 로컬 DNS들이 TLD를 알고 있기 때문에 굳이 root를 통과하지 않아서 DDoS 어택이 성공하지 못하나, TLD는 공격 당할 수 있다.  
> 대표적으로 DDoS, Amplification Attack, Pharming Attack 등이 있다.  

> - **Amplification Attack**  
>  1. 다른 컴퓨터들을 감염시켜서 DNS서버에게 ‘특정한 서버의 주소를 알려달라’ 라고 보냄. 
>  2. 보낼 때 본인들의 주소가 아니라 공격대상의 주소를 담아서 보냄.   
>  3. 서버는 공격대상에게 모든 response를 보내게 되고 그렇게 victim이 발생함.
> - **Pharming Attack**  
>> Private data + Farming. Domain hijacking을 통해 단순히 데이터를 가로챌 뿐만 아니라 자기가 키움.  
>  1. 공격자가 로컬 DNS에 침투해서 은행 IP주소에다가 실제 은행 주소 대신 본인이 만든 가짜 웹사이트 주소를 넣어둠.  
>  2. user가 은행의 IP주소를 요청했을 때, 가짜 웹사이트 주소에 접속하게 됨.  
>  3. 이 때 보안카드나 공인인증서 ID 등을 다 입력하면 다 공격자에게 넘어감.  

## 3-7) Peer-to-Peer (P2P)   
> end system들(각각의 peer들)끼리 직접적으로 통신함. 서버로도 동작하고 클라이언트로도 동작함.  
> ➡ 클라이언트-서버 구조에 비해 훨씬 Scalable함.  
> BitTorrent, Skype 등이 P2P 방식이다. 

> ![그림11](https://user-images.githubusercontent.com/76995452/108051620-72493780-708e-11eb-865c-5beec50945df.png)

### BitTorrent의 작동 원리 (= P2P의 작동 원리)  

> - 특정 사용자가 BitTorrent에 접속했을 때 누구와 연결을 해야할 지 모르므로 Tracker가 존재.   
> Tracker라는 서버에는 어떤 데이터가 필요하고, 이 데이터를 얻으려면 누구에게 접속해야 하는 지에 대한 정보가 저장되어있음.  
> - Chunk는 하나의 전체 파일을 한 peer에서 받지 않음. Why? 시간도 오래걸리고, 해당 peer가 날 위해 쭉 접속해준다는 보장이 없음.  
>  그래서 주기적으로 User 가 전체 파일의 Chunk를 쭉 나누어서 특정 chunk를 누가 갖고있는 지를 조사함.   
>> ex. 첫번째 chunk는 5개의 peer가, 두번째 chunk는 2개의 peer가, 세번째 chunk는 10개의 peer가 갖고있다.  
>> 그러면 User 입장에서는 2개의 peer만 갖고 있는 두번째 chunk를 미리 받아놓는게 유리함.   
>> 네트워크 입장에서도 훨씬 rare(희귀)한 chunk를 많은 peer들이 다운 받아서 널리 퍼지는게 좋음.  
>> ➡	Rarest first 정책으로 데이터를 받게 됨.  

> - Free rider : P2P사이트에서 데이터를 받기만하고 본인의 자원을 써가며 데이터를 제공하려고 하진 않는 사람.
이를 방지하기 위해 tit-for-tat 이라는 방식이 고안됨.
> - tit-for-tat
>> 1. 각각의 peer들은 주기적으로 자신한테 데이터를 잘 주는 top4 peer를 선정함.   
>> 2. 이렇게 되면 고착화가 될 수 있으므로 매 30초마다 랜덤하게 하나의 peer를 선정해서 서비스를 제공.
>> 3. B가 자신만의 top4 peer가 있는 상태에서 A에게 30초 주기로 랜덤하게 데이터를 보내는데 기존의 peer들보다 잘 돌아온다?   
>> ➡ 제일 낮은 peer 끊고 그 자리에 A가 들어옴.  
>> - 이런 식으로 관찰해보면 업로드를 많이 하면 할수록 좋은 파트너를 얻어서 다운로드도 더 많이 받을 수 있는 효과가 있음.  
>> - 각각의 peer들이 자신이 free-rider가 되면 데이터를 못 받으니까 남한테 데이터를 잘 제공해서 자기도 잘 받을 수 있도록 하더라는게 tit for tat의 기본 아이디어.  

## 3-8) 비디오 스트리밍 & CDN  
> 점점 데이터가 text에서 멀티미디어(동영상 등)로 바뀌는 만큼 Scalability가 문제점으로 떠오른다.  
> 이를 해결하기 위해 나온 것이 CDN (Content Distribution Networks) 전세계에 분산된 서버를 둬서 유저들은 가장 근처에 있는 서버로부터 서비스를 지속적으로 받는다.  

- 넷플릭스는 아래 과정에 의해 돌아감.
1.	넷플릭스 계정관리 서버에 로그인
2.	아마존 클라우드에 접속해서 보고 싶은 영화를 검색함. 
3.	검색한 영화에 대한 manifest file을 받게 됨. 
4.	사용자의 위치와 환경을 고려해서 가장 적합한 서버의 위치를 알려주면 특정한 서버의 HTTP를 통해서 영화 파일을 가져오도록 요청하게 됨.
5.	스트리밍

![그림12](https://user-images.githubusercontent.com/76995452/108051606-6f4e4700-708e-11eb-8e0f-ad636bb3cc60.png)

