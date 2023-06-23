# JPA
- Java Persistence API란 무엇인가?
- Java Persistence API는 어떻게 사용할까?
<br></br>

## 개념
- 자바 *ORM 기술*에 대한 표준 명세로, 자바 어플리케이션에서 RDBS를 사용하는 방식을 정의한 **인터페이스**이다. 스프링의 API가 아닌 자바 제공 API다.

- 개발자가 직접 SQL을 작성하지 않아도, JPA를 활용해 DB에 데이터를 저장하고 관리할 수 있다.
<br></br>

## Object Relational Mapping(ORM) 이란?
- ORM 프레임워크는 자바 객체와 관계형 DB를 매핑하는 프레임워크이다. 객체가 DB 테이블이 되도록 만들어준다.
    - 사용자가 직접 SQL을 작성하지 않아도 직관적인 메소드로 데이터를 조작할 수 있다.

- 종류로는 `Hibernate`, `EclipseLink`, `DataNucleus` 가 있다.
<br></br>

### 📌 스프링 부트의 ORM
- 스프링 부트에서는 `spring-boot-starter-data-jpa`로 패키지를 가져와 사용하며, `Hibernate` 프레임워크를 활용한다.

- JPA는 **애플리케이션과 JDBC 사이**에서 동작한다.

    - 사용자가 직접 JDBC API를 사용하는 것이 아니며, 사용자가 JPA 메소드를 호출하면 JDBC API를 거쳐 SQL을 전송하게 된다.

    - 이후 DB로부터 반환받은 결과는 JDBC API를 거쳐 매핑되고, JPA 측(JAVA 어플리케이션 단)에 결과 객체로 반환된다.

    - JPA가 쿼리를 생성해주기 때문에 객체와 RDB간의 패러다임 불일치를 해소할 수 있다.
<br></br>

## JPA의 특징
1. 객체 중심의 개발이 가능하다.
    - 하나의 테이블이나 객체를 생성할 때, 불필요한 CRUD 작업의 반복을 줄여준다. 

    - 컬럼이나 객체가 수정되면 SQL문을 모두 수정해야 하는 번거로움을 해소한다.

2. 생산성이 증가한다.
    - SQL 쿼리를 직접 작성하지 않고, 만들어진 자바 객체에 JPA 메소드를 활용해 DB에 접근하기 때문에 편리성이 보장된다.

3. 유지보수가 용이해진다.
    - 쿼리의 수정이 필요할 때, DTO 필드도 모두 변경해야 하는 불상사를 막을 수 있다. **엔티티 클래스의 정보만 수정**하는 것으로 해결된다.

4. 성능이 증가한다.
    - 사용자가 직접 짠 SQL과 비교해서, JPA는 **동일 쿼리의 캐시 기능**을 지원해주기 때문에 비교적 성능 효율이 높다.

- 그러나 JPA는 복잡한 쿼리보다는 실시간 쿼리에 최적화되어있다.

    - 따라서 **통계 처리**와 같은 복잡한 작업은 `MyBatis` 등의 `Mapper` 방식이 효율적일 수 있다.
<br></br>

## Spring Data JPA
- JRA가 ORM을 위한 자바 EE 표준이라면, `Spring Data JPA`는 JPA를 쉽게 사용할 수 있도록 스프링에서 제공하는 프레임워크이다.

    - `JpaRepository` 인터페이스만 구현하면 실행 시점에 Spring Data JPA가 구현 객체를 동적으로 생성해서 주입한다. 

- 추상화 정도는 `Spring Data JPA` → `Hibernate` → `JPA` 이다.

- `JpaRepository` 를 상속받으면 사용할 수 있는 주요 메서드

    - `save(S)` : 식별자 값이 없으면 `em.persist()`, 있으면 `em.merge()`를 호출 (새로운 엔티티는 저장하고 기존의 엔티티는 수정)

    - `delete(T)` : 내부에서 `em.remove()` 호출

    - `findOne(ID)` : 내부에서 `em.find()` 호출

    - `getOne(ID)` : 내부에서 `em.getReference()` 호출
    
    - `findAll(..)` : sort 또는 pageable 조건을 파라미터로 제공
<br></br>

### 출처
- https://github.com/gyoogle/tech-interview-for-developer/blob/master/Web/Spring/JPA.md
- https://velog.io/@modsiw/JPAJava-Persistence-API%EC%9D%98-%EA%B0%9C%EB%85%90
- https://data-make.tistory.com/621