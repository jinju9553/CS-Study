# 자바의 Garbage Collection
- Garbage Collection은 어떤 원리로 동작할까? 
<br></br>

## stop-the-world
- GC을 실행하기 전에 JVM 애플리케이션이 실행을 멈추는 것.
- GC 튜닝에 있어서 stop-the-world에 소모되는 시간을 줄이는 게 중요하다.
<br></br>

## Garbage Collection
- C/C++과 달리 개발자가 명시적으로 객체를 해제할 필요가 없으며, GC이 알아서 사용하지 않는 객체를 메모리에서 삭제한다.

- JVM은 5가지 영역(class, stack, heap, native method, PC)으로 나눌 수 있는데, 이 중 GC은 힙 메모리에만 관여한다.

- 다음과 같은 경우에 GC의 대상이 된다.
    1. 객체가 `NULL`인 경우 (`String str = null`)
    2. 블럭 실행 종료 후, 블럭 안에서 생성되었던 객체
    3. 부모 객체가 `NULL`인 경우, 이를 포함하는 자식 객체 

- GC은 약한 세대 가설(Weak Generational Hypothesis)에 기반하므로, 이를 최적화 하기 위해 메모리를 세대 단위로 관리한다.
<br></br>

## GC의 메모리 해제 과정 3단계
1. Marking
    - GC이 어떤 메모리가 사용되고 있는지 아닌지를 찾아낸다. 모든 객체를 스캔해야 하기 때문에 소모 시간이 크다.

2. Normal Delection 
    - 마킹을 끝내면 참조되지 않는 객체를 제거하고, 메모리를 반환한다. 반환되고 남은 블럭의 참조 위치는 따로 저장해두고, 새로운 객체가 선언되면 그곳에 할당되도록 한다. 

3. Compacting
    - 퍼포먼스 향상을 위해, 참조되지 않는 객체를 제거하고, 남은 객체들을 묶는다. 메모리 공간을 한 데 묶음으로서 더 많은 공간이 생기고, 새로운 메모리를 더욱 빠르게 할당할 수 있다.
<br></br>

## Weak Generational Hypothesis 
- 신규로 생성한 객체의 대부분은 금방 사용하지 않는 상태가 되고, 오래된 객체에서 신규 객체로 참조하는 경우가 적다는 가설.
- 이 가설을 기반으로 자바는 메모리를 Young 영역과 Old 영역으로 분할하여 관리한다.
<br></br>

## GC의 세대 관리
1. Young 영역
    - 새롭게 생성한 객체가 자리하는 부분. 이 영역에서 객체가 사라질 때 **Minor GC**가 발생한다고 말한다.

2. Old 영역
    - Young 영역에서 살아남은 객체, 즉 일정 횟수 이상 참조된 객체가 이곳으로 복사된다. 크기가 큰 만큼 Young 영역보다는 GC이 적게 발생하며, 이 영역에서 객체가 사라질 때 **Major GC**(Full GC) 가 발생한다고 말한다.

3. Permanet 영역
    - Method Area라고도 한다. JVM이 사용하는 메타 데이터들을 포함하며, JDK8 부터는 Metaspace로 교체되어 운영된다.
<br></br>

## Generational Garbage Collection 과정
1. 어떤 새로운 객체가 들어오면 Eden Space에 할당한다.

2. Eden Space가 가득 차면 Minor GC이 실행된다.

3. 참조되는 객체들은 첫 번째 Survivor(S0) 영역으로 이동되고, 참조되지 않는 객체는 Eden Space가 clear 될 때 같이 반환된다.

4. 그 다음 Minor GC에서도 같은 일이 일어난다. 그런데 이 때에는 새롭게 참조되는 객체는 두 번째 Survivor 영역(S1) 영역으로 이동되고, S0 영역에 있던 객체들도 age가 증가하면서 S1으로 이동된다. 그리고 S0와 Eden Space는 clear 된다.

5. 그 다음 Minor GC에서도 똑같은 일이 반복된다. Survivor Space가 전환되어 다시 S1에 있던 객체들이 S0로 이동된다. (참조되는 객체들을 계속 두 공간이 주고 받음)

6. age가 증가한 객체들이 일정한 참조수(age threshold)를 넘게 되면 Young 영역에서 Old 영역으로 복사되는데, 이를 Promotion 이라고 한다.

7. 위 과정이 반복되며 지속적으로 참조되는 객체들이 Old 영역으로 이동되고, 그렇지 않은 객체들은 제거된다. Major GC이 발생되면 Old 영역 또한 clear되고 공간이 확보된다.
<br></br>

### 출처
- https://gyoogle.dev/blog/computer-language/Java/Garbage%20Collection.html
- https://brorica.tistory.com/entry/%EC%9E%90%EB%B0%94-gc
- https://d2.naver.com/helloworld/1329