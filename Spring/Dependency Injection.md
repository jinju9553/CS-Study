# Dependency Injection
- DI의 의미는 무엇일까?
- 스프링에서 DI는 어느 상황에서 발생할까?
<br></br>

## 의존성이란?
- 단순하게 표현하면 `new` 키워드 자체라고 볼 수 있다.

- 아래의 코드는 `Car`가 `Tire`에 의존하는 예시이다. `Car`가 직접 `Tire`를 주입하고 있으며, `Tire`의 종류를 `KoreaTire`에서 다른 것으로 바꿔야 할 때마다 코드의 수정이 계속해서 일어난다.

-   ```
    public class Car {
        private Tire tire;

        public Car() {
            this.tire = new KoreaTire();
        }
    }
    ```
    - 이 경우 객체 간 **강한 결합**이 생긴다.
<br></br>

## 외부에서 주입 받기
- 내부에서 `new` 키워드로 인스턴스를 주입하는 것이 아닌, **외부에서 주입**을 해주는 것을 **의존성 주입**이라고 할 수 있다. 

- 즉 `new` 키워드를 쓰지 않고 **외부로부터 객체의 인스턴스를 주입받는 과정**을 말하며, 객체 간의 의존성이 줄어들고 코드의 불필요한 수정을 막을 수 있다는 장점이 있다. 

- GoF 디자인 패턴 중 Strategy 패턴에 응용할 수 있는 방법이다.

-   ```
    public class Car {
        private Tire tire;

        public Car(Tire tire) { //생성자를 통해 인스턴스를 제공받는다.
            this.tire = tire;
        }
    }
    ```
    - 이 경우 객체 간 **느슨한 결합**이 생긴다.
<br></br>

## 스프링의 IoC 컨테이너
- 위처럼 의존성 주입을 직접할 수도 있지만, 스프링은 객체를 Bean으로 등록만 하면 **IoC 컨테이너가 자동으로 의존성을 주입**해준다.

- IoC 컨테이너의 역할
    - Bean 설정 소스로부터 Bean의 정의를 읽어들여 Bean을 구성하고, 객체를 제공한다.
    - Bean 들의 의존 관계를 설정한다. (객체 생성 & 의존성 주입)
    - `BeanFactory`, `ApplicationContext` 등의 인터페이스를 통해 위 내용을 수행한다.

### 📌 컨테이너란?
- 본래 컨테이너는 어떤 것들을 담는 용기를 뜻하는데, 여기서 IoC 컨테이너는 **Bean으로 등록된 객체들을 담고 있는** 용기라고 볼 수 있다.

![image](https://github.com/jinju9553/CS-Study/assets/69393506/e979ebd2-981a-42a7-805a-e52393c78a79)

- 그림과 같이 Bean으로 등록된 객체들을 IoC 컨테이너가 의존성을 만들어 외부에서 주입해준다.
<br></br>

## 의존성 주입을 사용하는 이유?
- 재사용성을 높여준다.

- 테스트가 용이해진다. 외부에서 주입을 하면 본인이 원하는 주입을 외부에서 만들어 넣은 후 테스트할 수 있다.

- 객체간의 결합도를 낮춰준다. → 변경에 민감하지 않고, 유연성과 확장성을 향상시킨다.
<br></br>

## Java의 관련 어노테이션
- **Component-Scan 방식**(`@ComponentScan`)으로 아래의 어노테이션을 스캔하고, 관련 작업을 처리한다.
    - `@SpringBootApplication` 어노테이션이 존재하는 파일의 패키지와 같거나 하위 패키지에 존재하는 어노테이션을 모두 스캔한다.

- `@Configuration`
    - 해당 파일에 Bean 설정이 포함되어 있음을 알린다.

- `@Bean`
    - 해당 POJO 객체나 메소드를 Bean으로서 컨테이너에 등록한다.
<br></br>

### 출처
- https://github.com/wjdrbs96/Gyunny_Spring_Study/blob/master/spring/2%EC%A3%BC%EC%B0%A8/1.%20%EC%9D%98%EC%A1%B4%EC%84%B1%20%EC%A3%BC%EC%9E%85%EC%9D%B4%EB%9E%80%3F.md
- https://github.com/wjdrbs96/Gyunny_Spring_Study/blob/master/spring/2%EC%A3%BC%EC%B0%A8/2.%20%EC%8A%A4%ED%94%84%EB%A7%81%EC%97%90%EC%84%9C%20%EC%9D%98%EC%A1%B4%EC%84%B1%20%EC%A3%BC%EC%9E%85.md
