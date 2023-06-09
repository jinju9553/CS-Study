# 자동 형변환(Promotion) & 강제 형변환(Casting)
- 자동 형변환과 강제 형변환은 각각 어느 상황에 일어나는가?
- 자동 형변환과 강제 형변환의 차이는 무엇인가?
<br></br>

## 자동 형변환(Promotion)
- 프로그램 실행 도중에 자동적으로 형변환(타입 변환)이 일어나는 것.

- **작은 크기의 데이터 타입을 큰 크기의 데이터 타입으로** 변환하는 과정을 가리킴. 
    - 예: `byte` 타입 변수 a를 `int` 타입 변수 b에 저장함
    - 이러한 과정에서는 별다른 문법이 없이도 형변환이 일어남.

- 주의
    - `byte` 타입 데이터는 `char` 타입으로 자동 형변환 불가.

    - `float` 타입 데이터는 `long` 타입으로 자동 형변환 불가.

    - `long` 타입 데이터는 `float` 타입으로 형변환 가능. (`long` 타입의 메모리 크기가 `float` 타입보다 크지만, `float`가 `long`보다 표현할 수 있는 값의 범위가 큼.)

    - `short`와 `char` 모두 `int`로 형변환 가능.
<br></br>

## 강제 형변환(Casting)
- 자동 형변환이 일어나지 않을 때 강제로 타입을 변환시키는 과정. 즉, 큰 크기의 데이터 타입을 작은 크기의 데이터 타입에 대입하는 과정.

- 캐스팅을 하지 않으면 컴파일 에러가 난다.
    - 예를 들어, int 타입(4byte) 데이터를 byte 타입(1byte) 데이터로 저장하려면 그 차이(3byte)만큼의 데이터가 삭제됨.
    - 일부 메모리가 유실되므로 정상적인 값을 얻을 수 없음.

- 따라서, 형변환 하고 싶은 변수 앞에 다음과 같은 형식으로 괄호 안에 타입을 표기함.
    - `int n = (int) doubleNumber`
<br></br>

## 형변환 연산
- +, -, *, / 등의 기본 사칙연산 연산자로 계산하면, **두 피연산자 중 크기가 큰 타입을 기준으로 자동 형변환**이 일어난 후 연산이 수행된다.

- 예를 들어, `int` 타입 피연산자와 `double` 타입을 더하면 `int` 타입 데이터가 `double` 타입으로 자동 형변환 된다. 연산의 결과도 `double` 타입이 된다.

- `int` 타입 연산 결과를 얻고 싶다면, 강제 형변환을 이용한다.
<br></br>

## 그 외
- Primitive type의 캐스팅은 원칙적으로 **데이터 손실**을 막는 데 그 목적이 있다.
- 캐스팅의 개념은 Reference type을 형변환 하는 **업 캐스팅**과 **다운 캐스팅**에서 응용된다.
- OOP의 **다형성**과도 관련이 있다.
<br></br>

### 출처
- https://github.com/GimunLee/tech-refrigerator/blob/master/Language/JAVA/Promotion%20%26%20Casting.md#promotion--casting
- https://mommoo.tistory.com/40
- https://velog.io/@sezzzini/Java-Casting