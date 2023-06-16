# 고유 락(Intrinsic Lock)
- 자바에서 동기화 문제는 어떻게 해결할까?
- 자바에서 Intrinsic Lock은 어떻게 사용할까?
<br></br>

## 자바에서의 동기화
- 자바는 크게 `static`, `stack`, `heap`의 세 가지 메모리 영역을 가지고 있다. 
    - `static` 영역 : 필드, 즉 전역 변수와 static 자료형을 관리한다.

    - `stack` 영역 : 스레드마다 할당받는 영역. 메소드 내에서 정의하는 기본형 지역 변수와 메소드들의 콜 스택을 저장한다.

    - `heap` 영역 : 참조형 데이터 타입을 갖는 객체(인스턴스), 배열 등을 저장한다.

- 멀티 스레드 환경에서는 스레드들 끼리 **static 영역과 heap 영역을 공유**한다. 따라서 공유 자원의 동기화(Synchronization)를 신경써야 한다.
<br></br>

## 고유 락(Intrinsic Lock)
- 자바의 모든 객체는 락을 가지고 있고, 각 객체마다 고유하게 가지고 있기에 고유 락(Intrinsic Lock)이라고 부른다.

- `synchronized` 블록이 객체 단위로 락을 다루고, 스레드의 접근을 제어한다.
<br></br>

- **고유 락 재진입 (Reentrancy)**
    - 재진입: 이미 lock을 획득한 스레드가 같은 lock을 얻기 위해 대기할 필요 없는 것, lock의 획득이 **호출 단위가 아닌 스레드 단위로 일어나는 것.**
    
    - 특정 스레드가 `synchronized` 블록을 통해 객체의 lock을 획득했다면, 해당 객체 속의 다른 메소드들의 lock 또한 획득한다. 
        - 즉, 다음 `synchronized` 블록을 만났을 때 대기 없이 통과가 가능하다.

    - 이러한 특성이 없다면 어떤 메소드 a, b가 서로를 상호 호출 하거나 공유 자원에 대한 선점이 발생함 => Deadlock

    - 만약 static 메소드에 `synchronized` 키워드가 붙는다면 **class 단위로 lock을 획득**한다.
<br></br>

## Thread-safe 연산
-   ```
    public class Counter {
        private int count;

        public int increase() {
            return ++count;
        }
    }
    ```
    - 위 연산은 `read` (count 값 읽기) → `modify` (count 값 수정) → `write` (count 값 저장) 과정에서 **여러 스레드가 공유자원(count)에 접근**할 수 있으므로, 동시성 문제가 발생한다.
    
    - 동시성 문제를 해결하기 위해 count 변수로 접근하는 스레드를 제어해야 한다.
    <br></br>

-   ```
    public class Counter {
        private Object lock = new Object(); //모든 객체가 lock 보유
        private int count;

        public int increase() {
            synchronized(lock) {
                return ++count;
            }
        }

        // 또는 아래처럼 표현 가능
        /*
        public synchronized int increase() {
            return ++count;
        }*/
    }
    ```
    - 위와 같이 `lock`이라는 `Object`의 인스턴스를 이용해 `count` 변수로의 접근을 제어할 수 있다.
    - `increase()` 메소드는 한 번에 한 스레드만 실행시킬 수 있으며, 한 스레드가 먼저 락을 취득한 경우 다른 스레드는 대기해야 한다.
<br></br>

## 가시성 (Visibility)
- 여러 스레드가 동시에 작동하였을 때, **한 스레드가 쓴 값을 다른 스레드가 볼 수 있는지**의 여부를 가시성이라고 한다.

- Structure Lock 과 Reentrant Lock은 가시성을 보장한다.

- 하나의 스레드가 쓴 값을 다른 스레드가 볼 수 없으면 문제가 발생한다.
    - 원인
    1. 컴파일러나 CPU가 최적화를 위해 코드 재배열을 한 경우 발생
    2. CPU core의 캐시값이 메모리에 제 때 쓰이지 않은 경우 발생
<br></br>

### 출처
- https://brunch.co.kr/@kd4/156
- https://github.com/gyoogle/tech-interview-for-developer/blob/master/Language/%5BJava%5D%20Intrinsic%20Lock.md
- https://velog.io/@kimmy/CS-%EC%A7%80%EC%8B%9D-Java-%EA%B3%A0%EC%9C%A0%EB%9D%BD-Intrinsic-Lock