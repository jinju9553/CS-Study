# Bean Scope
- 스프링에서 Bean의 사용 범위는 어떻게 될까?
<br></br>

## Bean이란?
- Bean이란 스프링에서 사용하는 **POJO 기반 객체**이다.

- Bean은 **Spring IoC 컨테이너**가 인스턴스화, 관리, 생성을 담당한다.

- Bean은 컨테이너에 공급하는 **설정 메타 데이터(XML 파일)를 따라 생성**된다.

- Bean의 사용 범위(Scope)는 개발자가 각종 목적에 맞게 설정할 수 있다.
    - 별도의 설정이 없다면 Spring Bean은 JVM 안에서 `Singleton`으로 생성된다.
    - 이러한 경우 싱글톤 패턴처럼 특정 타입 Bean을 딱 하나만 만들고, 모두가 공유한다.
    - 스프링을 통해 Bean을 제공받는다면, 언제나 주입받은 Bean이 동일한 객체라는 가정 하에 개발한다.
<br></br>

## Scope의 종류
1. `singleton`
    - 해당 Bean이 **IoC 컨테이너**에서 단 한 번 생성된다.
    - 하나만 생성되기 때문에 객체를 참조할 때에는 늘 동일한 것을 참조한다.

2. `prototype`
    - 해당 Bean이 다수의 객체로 존재할 수 있다.
    - 즉, Bean의 모든 요청에서 **새로운 객체(인스턴스)를 생성**하며, 참조되지 않을 때에는 GC가 제거한다.

3. `request`
    - 해당 Bean이 **HTTP Request 라이프사이클** 안에서 단 한 번 생성된다.
    - Spring MVC Web Application에서만 사용된다.

4. `session`
    - 해당 Bean이 **HTTP Session 라이프사이클** 안에서 단 한 번 생성된다.
    - Spring MVC Web Application에서만 사용된다.

5. `global session`
    - 해당 Bean이 **Global HTTP Session 라이프사이클** 안에서 단 한 번 생성된다.
    - Spring MVC Web Application에서만 사용된다.

<br></br>

## Singleton 활용
1. 싱글톤으로 적합한 객체
    - 상태가 없는 공유 객체
        - 동기화 비용이 없기 때문에 새로 생성할 필요 X

    - 읽기용으로만 상태를 가진 공유 객체
        - 읽기 전용이므로 역시나 동기화 비용이 들지 않음.

    - 공유가 필요한 상태를 지닌 공유 객체

    - 쓰기가 가능한 상태를 지니면서도, 사용 빈드가 매우 높은 객체

2. 비(非)싱글톤으로 적합한 객체
    - 쓰기가 가능한 상태를 지닌 객체
        - 동기화 비용이 객체 생성 비용보다 큰 경우 싱글톤에 적합하지 않음.

    - 상태가 노출되지 않는 객체
        - 내부의 상태를 외부로 노출하지 않는다면 다른 의존객체와 독립적으로 작업 수행.
        - 따라서 비 싱글톤 객체를 사용하는 것이 좋음. (동기화 X)
<br></br>

## Scope 등록
- Bean으로 등록하려는 클래스에 **어노테이션**으로 Scope를 설정해줄 수 있다.
-   ```
    @Scope("prototype")
    @Component
    public class UserController {
        /*...*/
    }
    ```
<br></br>

### 출처
- https://github.com/gyoogle/tech-interview-for-developer/blob/master/Web/Spring/%5BSpring%5D%20Bean%20Scope.md
- https://gmlwjd9405.github.io/2018/11/10/spring-beans.html