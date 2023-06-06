# 직렬화(Serialization)
- 직렬화란 무엇일까?
- 직렬화는 언제 사용하는 게 좋을까?
<br></br>

## 의미
- Java 언어로 정의된 객체를 순차적인 **Byte 데이터로 변환**하는 기술.

- 본래 OS마다 서로 다른 가상 메모리 주소 공간을 갖기 때문에, `Reference` 타입의 데이터는 인스턴스를 전달할 수 없다.
    - 하지만 직렬화를 하면 *서로 다른 OS의 자바 시스템에서도 데이터를 사용*할 수 있다.
    - 이렇게 직렬화된 데이터는 모두 `Primitive` 타입이 되는데, 이는 파일 저장이나 네트워크 전송 시 파싱이 가능한 형태이다.

- 반대로 직렬화된 데이터를 읽어서 객체 상태로 복구하는 것을 역직렬화(Deserialization)라고 한다. 
<br></br>

## 직렬화 방법
- `java.io.Serializable` 인터페이스를 구현하여 직렬화/역직렬화 한다.

- `Serializable` 인터페이스를 상속 받은 객체, `Primitive` 타입의 데이터가 주요 직렬화 대상이며, `Reference` 타입처럼 주소값을 지닌 객체들은 Byte 변환을 위해 `Serializable` 인터페이스를 필수로 구현해야 한다.
<br></br>

## 그 외
- `serialVersionUID`는 개발자가 직접 선언하여 관리하는 게 좋다.

- 변경이 많거나, 개발자가 직접 컨트롤 할 수 없는 클래스 등은 직렬화 사용을 지양한다.

- 그러나 JSON 포맷이 직렬화 데이터 포맷보다 더욱 효율적이며, 트래픽 증가와 비용 문제 해소를 위해 JSON 포맷을 사용하는 것이 좋다.
<br></br>

### 출처
- 천인국, \<Power Java Compact\>, 인피니티 북스 (2019)
- https://github.com/gyoogle/tech-interview-for-developer/blob/master/Language/%5BJava%5D%20%EC%A7%81%EB%A0%AC%ED%99%94(Serialization).md 