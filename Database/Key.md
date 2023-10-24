# Key (기본키, 후보키, 슈퍼키)
- 데이터베이스의 Key란 무엇일까?
- 데이터베이스의 Key에는 어떤 종류가 있을까?

<br>

## Key의 개념
- 데이터베이스에서 조건을 만족하는 튜플을 찾거나 순서대로 정렬할 때, 다른 튜플들과 구별할 수 있는 유일한 기준이 되는 속성(Attribute).
- 튜플이란?
  - 릴레이션을 구성하는 각각의 행, 속성의 모임으로 구성된다. 파일 구조에서는 '레코드'와 유사한 개념이다.
  - 튜플의 수 = 카디널리티 = 기수 = 대응 수

## 종류
### 📌 기본키 (Primary Key)
- 개체에서 각 인스턴스를 **유일하게 식별**하는 Key. 여러 개의 후보키 중에서 하나 선정한다. 
- 개체 무결성의 조건
    1. Null값을 가질 수 없다.
    2. 동일한 값을 중복해서 저장할 수 없다.
- 기본키 설정 시 고려할 사항으로 해당 실체를 대표할 수 있고, 업무적으로 활용도가 높은(=**where 조건절**에서 자주 사용하는) 것을 PK로 선정한다.
- 클러스터링 인덱스가 자동 생성되므로 참조 시 효율성이 올라간다.
  
<br>

### 📌 후보키 (Candidate Key)
- 개체 내에서 각각의 인스턴스(혹은 튜플)를 유일하게 구분할 수 있는 속성의 부분집합으로, 기본키가 될 수 있는 모든 후보 속성을 가리킨다.
- 다음의 두 조건을 만족해야 한다.
    1. 유일성 : Key로 하나의 튜플을 유일하게 식별할 수 있어야 한다.
    2. 최소성 : 꼭 필요한 속성으로만 구성되어야 한다.

<br>

### 📌 대체키 (Alternate Key)
- 후보키가 둘 이상일 때, 그중에서 기본키로 선정되지 않은 속성을 가리킨다.

<br>

### 📌 슈퍼키 (Super Key)
- 유일성은 만족하지만, 최소성은 만족하지 못하는 키이다.
- Key로 하나의 튜플을 식별할 수는 있지만 불필요한 속성들이 포함되어 있을 수 있다.

<br>

### 외래키 (Foreign Key)
- 릴레이션 R1, R2가 관계를 맺고 있을 때, 릴레이션 R1이 참조하고 있는 R2의 기본키 속성.
- 외래키로 지정된 컬럼은 참조하는 테이블(R2)의 기본키에 없는 값을 입력할 수 없다.
  - 예: 한 회원이 관심 상품을 등록할 때, 존재하지 않는 회원의 관심 상품 정보를 등록할 수는 없다.

<br>

### 📌 복합키 (Composite Key)
- 하나의 속성으로 기본키가 될 수 없는 경우, 둘 이상의 컬럼을 묶어서 식별자로 정의하는 경우.

<br>

### 📌 대리키
- 식별자가 너무 길거나 여러 개의 속성으로 구성되어 있는 경우, 인외적으로 추가하는 식별자를 가리킨다.
  
<br>

### 출처
- 개인 필기
- https://gyoogle.dev/blog/computer-science/data-base/Key.html
- https://limkydev.tistory.com/108