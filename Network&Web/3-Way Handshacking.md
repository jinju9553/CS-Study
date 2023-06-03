# 3-Way Handshacking
- 3-Way Handshacking 과정은 어떻게 이루어질까? 
<br></br>

## 의미
- TCP는 신뢰성 있는 연결을 보장해야 한다.
- 이 때 TCP 연결을 성립하고 해제하는 과정을 '3-Way Handshacking'이라고 한다.
<br></br>

## 과정
- TCP 소켓 연결은 아래와 같이 3단계에 걸쳐 진행된다.

1. 연결 요청을 위해 클라이언트가 서버에게 **SYN(x)** 패킷을 전송한다.
    - 헤더의 SYN 플래그 비트가 1로 세팅되며, 클라이언트 측이 순서 번호를 임의로 선택(x)하고 이 순서 번호를 담은 SYN 패킷과 Sequence Number가 전달된다.
2. 서버는 SYN 메시지에 대한 응답으로 **ACK(x + 1)** 메시지와 **SYN(y)** 패킷을 보낸다.
    - 클라이언트의 Sequence Number에 따라 서버 소켓도 순서 번호(y)를 선택한다.
    - 서버는 클라이언트로부터 추가 세그먼트를 수신하기 위해 TCP 연결에 필요한 소켓 자원을 OS안에 생성한다.
3. 클라이언트에게 ACK(x + 1)과 SYN(y)이 도착하면 **ACK**(y + 1)을 서버로 보낸다.
    - 클라이언트 측에서도 TCP 연결에 사용할 자원을 할당한다.
<br></br>

## TCP 연결 해제(4-Way Handshacking)
- TCP 연결 성립 후, 모든 통신이 끝났다면 연결을 해제한다.

1. 클라이언트가 서버에게 연결을 종료한다는 FIN 플래그(1bit)를 보낸다. Sequence Numeber(x)도 함께 전송된다.
2. 서버는 FIN을 받고, 확인의 표시로 ACK(x + 1)을 클라이언트에게 보낸다.
    - 이때, 서버는 `CLOSE_WAIT` 상태이다.
3. 데이터를 모두 보냈다면 연결 종료의 의미로 FIN 플래그(1bit)를 클라이언트에게 보낸다. Sequence Numeber(y)도 함께 전송된다.
4. 클라이언트가 FIN을 받고, 확인의 표시로 ACK(y + 1)을 서버에게 보낸다.
    - 서버가 ACK 메시지를 받으면 소켓을 닫는다. (Close()를 호출)
    - 클라이언트의 `TIME_WAIT` 시간이 끝나면 클라이언트도 닫는다. 
<br></br>

### 참고
- 개인 필기
- https://gyoogle.dev/blog/computer-science/network/TCP%203%20way%20handshake%20&%204%20way%20handshake.html