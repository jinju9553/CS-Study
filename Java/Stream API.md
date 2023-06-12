# Stream API
- 자바의 Stream은 어떻게 사용할까?
- 자바의 Stream은 언제 사용하는 게 적합할까?
<br></br>

## Collection과 Stream
- 두 자료는 **데이터의 계산 시점**에서 차이가 존재한다.

- Collection
    - 모든 값을 메모리에 저장하는 자료구조. `Collection`에 추가하기 전에는 미리 계산이 완료되어 있어야 함.
    - 외부 반복문(`for-each`)을 통해 사용자가 직접 요소를 가져올 수 있음.

- Stream
    - **람다식**으로 간결하고 깔끔하게 요소를 처리할 수 있는 기술.
    - 요청이 있을 때에만 요소를 계산하고, 내부적인 반복을 사용하므로 추출할 요소만 선언해준다면 알아서 반복을 처리한다.
    - 스트림에 요소를 따로 추가하거나 제거하는 작업은 불가능하다.
<br></br>

## 외부 반복과 내부 반복
- 외부 반복은 명시적으로 컬렉션 내부의 항목을 하나씩 가져와서 처리하며, 최적화에 불리하다.

- `Collection`에서 병렬성을 이용하려면 `synchronized`를 통해 관리해야 한다.

- 내부 반복은 작업을 병렬 처리하면서 자체적으로 **최적화된 순서**로 처리를 진행한다.
<br></br>

## Stream 연산
- 중간 연산
    - 파이프라이닝이 가능한 연산을 가리킨다.
    - 반환 타입이 `Stream` 이기 때문에 최종 연산을 필요로 한다.
    - `filter`, `map`, `limit` 등이 해당한다.

- 최종 연산
    - 스트림을 닫고 최종 결과물을 산출하는 연산이다.
    - 실질적인 `Collection` 객체를 리턴받을 수 있다.
    - `count`, `collect` 등이 해당한다.

- 예제
    - Item 중에서 가격이 1000 이상인 상품의 이름 5개 선택
    -   ```
        List<String> items = item.stream()
                                .filter(d -> d.getPrice() >= 1000)
                                .map(d -> d.getName())
                                .limit(5) //최종 연산
                                .collect(tempList());
        ```
<br></br>

## Optional 클래스
- `null`이 발생할 수 있는 값을 감싸는 `Wrapper` 클래스로, 불필요한 `null` 처리를 줄일 수 있다.

- `Stream`의 `findAny()`로 발견한 값들 또한 `Optional` 타입으로 반환된다.
    - 따라서 `Optional<T>.get()`으로 안에 들어있는 내용물을 가져와주어야 한다.
<br></br>

### 출처
- 개인 필기
- https://dpdpwl.tistory.com/81
- https://mangkyu.tistory.com/70
- https://github.com/gyoogle/tech-interview-for-developer/blob/master/Language/%5Bjava%5D%20Stream.md
