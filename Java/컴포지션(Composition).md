# 컴포지션(Composition)
- 컴포지션의 의미는 무엇인가?
- 컴포지션은 어느 상황에 사용할까?
<br></br>

## 정의
- 컴포지션이란, 기존의 클래스가 **새로운 클래스의 구성요소**가 되는 것을 말한다. forwarding이라고도 부른다.

- 상속처럼 기존의 클래스를 확장(extend)하지 않고, **새로운 클래스를 생성**하여 **private 필드로 상속하고 싶은 클래스의 인스턴스를 참조**한다.

- 새로운 클래스를 생성하는 것이기 때문에 **기존의 클래스에 전혀 영향을 주지 않으며,** 상속의 단점을 보완하여 보다 유연한 프로그램을 작성할 수 있다.
<br></br>

- **상속** : 하위 클래스가 상위 클래스의 특성을 재정의 한 것 → `IS-A 관계`
- **컴포지션** : 기존 클래스가 새로운 클래스의 구성요소가 되는 것 → `HAS-A 관계`

### 📌 상속이란?
- 하위 클래스가 상위 클래스의 특성을 재정의하는 일. 부모 클래스의 메서드를 오버라이딩하여 자식 클래스의 특성에 맞게 재사용할 수 있다.

- 그러나 상속을 올바르게 사용하지 않으면 코드의 유연성을 해칠 수 있다.
<br></br>

### 📌 구현 상속의 단점
1. 캡슐화를 위반한다.
2. 설계가 유연하지 못하다.
3. 다중 상속이 불가능하다.
<br></br>

## 컴포지션을 통한 코드 개선
- `ForwardingSet` 클래스
    ```
    public class ForwardingSet<E> implements Set {
        private final Set<E> set;

        public ForwardingSet(Set<E> set){
            this.set=set;
        }

        //이하로 메소드 Override
    }
    ```
    - `CustomHashSet` 을 만들 준비단계로 Set 인터페이스를 상속한 `ForwardingSet`을 생성한다. 

    - 전달 클래스(Forwarding Class)의 역할을 한다.
<br></br>

- `CustomHashSet` 클래스
    ```
    public class CustomHashSet<E> extends ForwardingSet {
        private int addCount = 0;

        public CustomHashSet(Set<E> set){
            super(set);
        }

        //이하로 메소드 Override
    }
    ```
    - Set에 요소가 추가된 횟수를 세는 `add()`, `addAll()`이 정의된 Custom한 HashSet 클래스를 작성한다. 기존의 `HashSet` 메소드에 count를 세는 부분이 추가된다.

    - Set 인터페이스를 구현함으로써 Set 객체를 인자로 받는 생성자를 가지게 되었다.

    - 이 클래스는 어떤 Set 객체를 인자로 받아, 필요한 기능을 가지고 있는 Set 객체로 변환시켜주는 역할을 한다. 즉, **Wrapper Class 의 역할**을 수행하고 있다.

    - 이러한 디자인 패턴을 **데코레이터 패턴**이라고 한다. (GoF)
<br></br>

### 출처
- https://github.com/gyoogle/tech-interview-for-developer/blob/master/Language/%5BJava%5D%20%EC%BB%B4%ED%8F%AC%EC%A7%80%EC%85%98(Composition).md
- https://dev-cool.tistory.com/22