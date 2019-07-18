Socket 이란?
===

Socket은 TCP/IP로 통신하는 네트워크 내에서 일어나는 통신 방법이다.

IP주소와 PORT번호로 생성되는 네트워크 주소를 통해, 클라이언트와 서버가 통신되도록 하는 것

![그림](./socket1.JPG)

이렇게 두 프로그램 또는 두 클라이언트가 네트워크를 통하여 서로 통신을 수행할 수 있도록 

**양쪽**에 생성되는 링크의 단자이다.

두 소켓이 연결되면 서로 다른 프로세스끼리 데이터를 송/수신 할수있따.

자 위 그림에서 보면, SERVER와 CLIENT로 입장이 나뉘어 있는데

무슨 차이가 있느냐면,

 - 서버 : 연결을 수동적으로 기다린다.....
 
 - 클라이언트 : 능동적으로 연결한다!!
 
 요 정도 차이가 있다고 보면 되겠다.
 
 ![그림](./socket2.jpg)
 
 결론적으로
 ---
 
 소켓은 TCP/IP와 APPLICATION 사이의 창구 역할을 한다고 보면 되겠다!
 
 소켓을 이용하면, 인터넷의 복잡한 하부구조에 대한 세부적인 지식이 없어도 손쉽게 네트워크를 이용한 프로그램을 개발 할 수 있다.
 
 TCP/IP 4계층 응용계층 바로 아래에 소켓을 제작하여, 응용계층만 신경쓰고 네트워크를 개발 할 수 있다.
 
 호오오오
 
 자 그럼 소켓을 어떻게 C#에서 사용하느냐 ??
 ---
 
 사실 대부분의 언어에서 소켓은 비슷한 원리로 동작한다.
 
 마치 DATA BASE를 쓰는것처럼 ..
 
 .NET 에서는 이 SOCKET을 이미 클래스로 만들어 놓았다 !!
 
 ~~~
 using System.Net.Sockets;
 
 Socket userSocket = new Socket(,,,);
 ~~~
 
 이러면 소켓 객체가 생성되었다 .. !
 
 wow
 
 사실 실제로 사용하려면 매개변수를 넣어야 하지만 일단 지금은 이렇게 넘어가도록 하자..
 
 
 서로 다른 두 소켓의 연결!
 ---
 
 통신이라는 것은 불특정 대상과 무언가를 하는 것이므로,
 
 혼자하는 것은 통신이라고 할 수 없다.
 
 소켓도 동일하게 client와 server로 분리 해 볼수 있는데,
 
 아까 위에 올렸던 그림을 다시 불러와 보자.
 
 ![그림](./socket1.JPG)

기본적으로 두개의 소켓을 연결 할 때 이러한 과정을 따른다.

server와 client는 각각 하는 일이 다르기 때문

SERVER
---

이놈은 대기를 하는 소켓이다. 

계속 listen 상태에 있으면서 requset에 response를 해준다.

> 계속 listen 상태이다 .. ? TCP ! 3-way HandShaking의 느낌이 올라오지 않는가 ??

누가 Requset를 보낼지는 모르지만, 그냥 계쏙 대기해 본다...

아무튼 누가 Request를 보내면 이때다 싶어서 Response를 보내준다.

제작 순서!

1. **Bind()** 메소드를 통해 소켓에 IP주소와 프로토콜 등을 할당한다. 
> 사실상 이때부터 진정한 소켓이 된다고 볼 수 있다.

2. **Listen()** 메소드를 통해 계속하여 대기하도록 한다.

3. 외부의 접근이 발생하면 **accept()** 메소드를 호출하고 연결한다.

4. 통신한다 **Read() & Write()** 
> 실제로 데이터를 공유하는 부분이다.

Client Socekt
--

client는 서버에 요청을하는 역할을 한다.

능동적으로 언제든 요청을 할 수 있으며, Bind작업을 필요로하지 않는다.

**Connect()** 메소드를 통해 **Listen()**중인 Server의 소켓에 접근, 

**Accept()**를 서버로 하여금 이끌어 낸다.

Server에 비해 매우 간단하다.







