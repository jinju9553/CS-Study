# AOP
- Spring AOP는 무엇이고 어떻게 동작할까?
- AOP는 어떻게 구현할까?

<br>

## AOP란?
- 핵심 관심 사항(core concern)과 공통 관심 사항(cross-cutting concern)의 분리
  
- 예를 들어, 어떤 일련의 기능들에 공통적으로 적용되는 보안 모듈(공통 관심 사항)이나 시간 측정 모듈(start time, end time 측정), 로깅 모듈 있다고 하자.
    - 이것들을 각 기능에 적용하려면 중복된 코드를 많이 작성하게 된다. (클래스를 분리하더라도 호출을 꼬박꼬박 해주어야 한다.) 
    - 특히 시간 측정의 경우 시작 전&후를 모두 처리해야 한다.
    - AOP는 문제를 해결하기 위한 핵심 관심 사항과 전체에 적용되는 공통 관심 사항을 기준으로 프로그래밍함으로써 공통 모듈을 손쉽게 적용할 수 있다.
  
- AOP는 **어플리케이션 단에서만 필요한 로직**을 구현하는 데에만 써야 한다. 로그인 처리 등의 핵심 비즈니스 로직을 AOP로 구현하지 않도록 유의하자.
    - 반면에 `Filter`는 **Presentation Layer** 상의 기능을 다룬다.

<br>

### 📌 관련 용어
- **Target**
    - 부가 기능을 부여할 대상. 핵심 기능을 담고 있는 모듈이다.
  
- **Advice**
    - 어느 시점(예 : 메소드의 수행 전/후, 예외 발생 후 등…)에 어떤 공통 관심 기능을 적용할지 정의한 것.
  
- **JoinPoint**
    - 정규표현식이 적용되는 시점.
    - 즉, Aspect가 적용될 수 있는 지점 (메소드 또는 필드 변수)
    - Target 객체가 구현한 인터페이스의 모든 메소드는 JoinPoint로써 기능할 수 있다.
  
- **Pointcut**
    - 공통 관심 사항이 적용될 JoinPoint.
    - Advice를 적용할 target의 **메소드를 선별하는 표현식**이다. 이 표현식은 `execution`으로 시작하고, **메소드의 시그니처를 비교**하는 방법을 이용한다.
  
- **Aspect**
    - Aspect = Advice + Pointcut
    - 여러 객체에서 공통으로 적용되는 공통 관심 사항. **(트랜잭션, 로깅, 보안 등등…)**
    - AOP의 기본 모듈을 가리키며, Aspect는 언제나 싱글톤 객체로 존재한다.
  
- **Advisor**
    - Advisor = Advice + Pointcut
    - Advisor는 Spring AOP에서만 사용되는 특별한 용어일 뿐, Aspect와 같은 의미이다.
  
- **Weaving**
    - 정규표현식을 실제로 적용하는 일.
    - 어떤 Advice를 어떤 Pointcut(핵심사항)에 적용시킬 것인지에 대한 설정(Advisor) 과정
    - 즉, Pointcut에 의해서 결정된 타겟의 JoinPoint에 **부가기능(Advice)을 삽입하는 과정**을 뜻한다. 핵심기능(Target)의 코드에 영향을 주지 않으면서도 필요한 부가기능(Advice)을 추가할 수 있도록 해주는 과정이다.

<br>

## Spring AOP의 특징

- 부가 서비스를 모듈화시키기 위해, 즉 Cross Concern을 구분하기 위한 목적으로 활용된다. `Interceptor`와는 조금 **다르다.**
- Spring은 프록시 기반의 AOP를 지원한다.
    - Target 객체에 대한 Proxy를 만들어 제공한다.

- 프록시가 호출을 가로챈다. (Intercept)
    - 전처리 Advice : Target 객체의 호출을 가로챈 다음 부가 기능 로직을 먼저 수행한다. 그 후 Target의 핵심 기능 로직을 호출한다.
    - 후처리 Advice : Target의 핵심 기능 로직 메소드를 호출한 후에, 부가 기능(Advice)를 수행하는 경우도 있다.

- Spring AOP는 메소드의 JoinPoint만 지원한다. (다른 곳에서는 필드 JoinPoint도 가능하지만 스프링은 예외.)

<br>

## Spring AOP의 구현 방법

```
1. POJO 기반 구현
2. Spring API를 이용한 구현
3. Annotation을 이용한 구현
```

### 📌 POJO 기반 구현
 - XML Schema 확장 기법을 통해 설정 파일을 작성하거나, POJO 기반 Advice 클래스를 작성한다.
  
 - `Before Advice`
     - 대상 객체의 메소드가 실행되기 전에 실행시킨다.
     - 리턴 타입 : void
     - 인자 : 없거나, JoinPoint만 전달한다.
 - `After Returning Advice`
     - 대상 객체의 메소드 실행이 정상적으로 끝난 후에 실행된다.
     - 리턴 타입 : void
     - 인자 : 없거나, JoinPoint만 **첫 번째 인자로** 전달한다.
 - `After Throwing Advice`
     - 대상 객체의 메소드 실행 중, 예외가 발생한 경우 실행한다.
     - 리턴 타입 : void
     - 인자 : 없거나, JoinPoint만 **첫 번째 인자로** 전달한다.
 - `After Advice`
     - 대상 객체의 메소드 실행이 끝난 뒤, 예외 발생 여부와 상관 없이 공통으로 실행
     - 리턴 타입 : void
     - 인자 : 없거나, JoinPoint만 **첫 번째 인자로** 전달한다.
 - `Around Adivce`
     - 위 **네 가지를 다 구현**할 수 있는 Advice
     - 리턴 타입 : `Object`
     - 인자 : `ProceedingJoinPoint`를 반드시 **첫 번째 인자로** 넘긴다.

<br>

### 출처
- 개인 필기