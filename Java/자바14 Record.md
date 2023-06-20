# 자바14 Record
- Record 타입은 무슨 목적으로 사용하는가?
- Record 타입은 어떻게 구현하는가?
<br></br>

## Class를 대신하는 Record 타입
- Record란 자바 14에서 프리뷰로 도입된 클래스 타입으로, 순수하게 데이터 그 자체를 보유하기 위해 존재하는 특수한 클래스이다.

- Entity 혹은 DTO 클래스를 정의할 때 유용하다.
<br></br>

### 📌 기존 Class로 구현한 `Person` entity
-   ```
    public class Person {
        private final String name;
        private final int age;
        
        public Person(String name, int age) {
            this.name = name;
            this.age = age;
        }
        
        public String getName() {
            return name;
        }
        
        public int getAge() {
            return age;
        }
    }
    ```
<br></br>

### 📌 Record 타입으로 구현한 `Person` entity
-   ```
    public record Person(
        String name,
        int age
    ) {}
    ```
    - C의 구조체와 유사한 형태

    - static 키워드가 붙은 변수를 생성할 수 있고, static & public 메소드를 생성할 수 있다.

    - 자동으로 필드를 `private final`로 선언하여 만들어주고, **생성자**와 **getter**까지 만들어준다.

    - 단, getter는 `getXXX()`이 아닌 `필드명()` 으로 생성된다. (예: `name()`, `age()`)

    - 모든 필드를 초기화해야 하는 RequiredAllArgument 생성자가 만들어진다.

    - 별도로 명시적인 생성자를 만들 수 있으며, 간단한 validation 로직을 넣을 수도 있다.

    - `final` 클래스이기 때문에 **상속할 수 없다.**

    - `equals()`, `hashCode()`, `toString()`을 자동으로 생성하여 지원한다.
<br></br>

### 출처
- https://coding-start.tistory.com/355
- https://github.com/gyoogle/tech-interview-for-developer/blob/master/Language/%5Bjava%5D%20Record.md