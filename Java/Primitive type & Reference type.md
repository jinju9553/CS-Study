# Primitive type & Reference type
- Primitive type과 Reference type의 차이는 무엇일까?
<br></br>

## Primitive type
![image](https://github.com/jinju9553/CS-Study/assets/69393506/9e47f3b7-e6d7-4bf2-ac55-8f806c632d30)
- 자바에서 사용되는 **기본 자료형**으로, 사용하기 전에 선언되어야 함.
- OS에 따라 자료형의 길이가 변하지 않는다.
- `==` 연산자로 비교한다.
- **비객체** 타입이기 때문에 `null` 값을 가질 수 없다. `null`값을 넣고 싶을 때에는 `Wrapper Class`를 이용.
- **스택 메모리**에 저장되어 사용함.
<br></br>

## Reference type
- 자바에서 Primitive type을 제외한 타입이 모두 Reference Type임. **참조형 타입**이라고도 부름. 
- `.equals()` 메소드로 비교한다.
- Reference type은 자바에서 최상위인 `java.lang.Object` 클래스를 상속하는 모든 클래스를 지칭한다. 
- **클래스**(class) 타입, **인터페이스**(interface) 타입, **배열**(array) 타입, **열거**(enum) 타입 등이 존재.
- `null` 값을 가질 수 있으며, 빈 객체를 의미한다.
- new 키워드를 통해 **힙 영역**에 메모리가 생성되고, GC로 해제한다.
<br></br>

## String 클래스
- Reference type에 속하지만 이례적으로 Primitive type처럼 사용한다. Reference type이기 때문에 `.equals()` 메소드로 비교한다.
- 불변(immutable) 객체라는 특징이 있다. 가변(mutable) 객체를 사용하고 싶다면 `StringBuilder` 등을 사용한다.
- `String` 클래스의 메소드를 이용해서 값을 변경해도, 새로운 `String` 객체를 만들어내는 것에 불과하다.
<br></br>

### 출처
- 천인국, \<Power Java Compact\>, 인피니티 북스 (2019)
- https://gyoogle.dev/blog/computer-language/Java/Primitive%20type%20&%20Reference%20type.html
