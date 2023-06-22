# 리스트 (ArrayList & LinkedLists)
- `Array`, `ArrayList`, `LinkedList`의 차이는?
- `Array`, `ArrayList`, `LinkedList`는 각각 언제 사용하는 게 좋을까?
<br></br>

## 각 자료구조의 비교
- `Array`는 index로 빠르게 값을 찾을 수 있다.
- `ArrayList`는 index로 데이터를 빠르게 찾을 수 있지만, 삽입 및 삭제가 느리다.
- `LinkedList`는 데이터의 삽입 및 삭제가 빠르다.
<br></br>

## Array의 특징
- 선언할 때 **크기와 데이터 타입을 지정**해주어야 한다.
    
    - 메모리 공간에 할당할 사이즈를 미리 정해놓고 사용하는 자료구조이다.
    
- 계속 데이터가 늘어나면서도, 최대 사이즈를 가늠할 수 없을 때는 부적합하다.
    
    - 중간에 자료의 길이를 늘려서 새 데이터를 삽입하거나 삭제할 때도 비효율적이다.

- **index**로 값의 위치를 곧바로 찾을 수 있다.
<br></br>

## ArrayList의 특징
- 선언할 때 **크기를 정해주지 않아도 된다.** 그러나 데이터의 **삽입 순서**가 중요하게 작용한다.

- 크기가 정해져 있지 않기 때문에, 데이터의 추가나 삭제가 용이하다.

    - 그러나 데이터의 추가 및 삭제 연산의 시간이 오래 걸린다. (더하고 삭제할 때마다 인덱스가 앞으로 당겨지거나 뒤로 밀려나는 등...)

- **index**로 값의 위치를 곧바로 찾을 수 있다.
<br></br>

## LinkedList의 특징
- 한 노드에 연결되는 다른 노드의 포인터를 저장한 자료구조.

    - 데이터가 중간에 삽입되거나 삭제되더라도 리스트 전체의 인덱스를 밀지 않고, 이전 값과 다음 값이 가리켰던 주소만 수정하여 연결하면 된다.

    - 따라서 데이터의 삽입과 삭제에 용이하다.

- 그러나 리스트에서 *k번째 값을 찾는 연산* 등을 수행할 때에는 비효율적이다.

    - 이러한 연산은 Array나 ArrayList에서 쉽게 수행할 수 있다.
<br></br>

### 출처
- https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Data%20Structure/Array%20vs%20ArrayList%20vs%20LinkedList.md