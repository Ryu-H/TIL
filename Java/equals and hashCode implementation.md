# equals()와 hashCode() method 구현과 Hash-Based Collection의 접근성
Hash-Based Collection들은 Object들을 넣을 때 일단 Hash Code를 이용해서 Bucket을 확인/생성하고 Object들을 넣는다.
따라서
- 두 객체들이 서로 동등(equal) 한데 Hash Code가 다르거나
- 동일(==)한 객체가 Hash Code를 구하는 데 쓰인 field가 Collection에 들어간 후 달라지거나

할 경우에 중복돼서 Collection에 들어가는 원치않는 경우가 생길 수 있다.

## 알아 둘 점
- hashCode method를 Override해 주지 않으면 기본적으로 메모리 값을 이용한다 (equals method 도 마찬가지. Override 해주지 않으면 Memory Reference 비교)
- HashSet class은 내부적으로 HashMap class 사용함
- Lombok 같이 annotation으로 저런 boilerplate 코드를 자동생성 해주는 기능을 쓸 경우에 상기한 이유때문에 주의할 필요가 있음

## 필수조건: equals가 true 일 경우 hashCode 또한 같을 것
Hash-Based Collections expect that when Object A and Object B are equal, that their hashCode to also be the same.

다르게 얘기하면 equals를 Override할 경우, equals()에서 체크하는 field의 값은 hashCode구현에도 사용되어야 함.

## 추천조건: equals가 false일 경우 hashCode 또한 다르면 좋음
This is not a requirement, but recommended to improve the accessibility of the collection.

e.g. If many objects are not equal but have the same Hash Code, a bucket would end up containing many objects and the collection will have to perform multiple equality checks.


## 기타 권장사항
- When implementing equals() and hashCode(), refrain from using fields that can be changed
- Keys used for HashMap should ideally be immutable
- If mutable keys need to be used for whatever reason, then refrain from changing the state of the objects used as the keys
- Similarly, refrain from changing the state of the objects that are already stored in a HashSet - especially for the fields that are used for hashCode()

### 상기한 내용들을 지키지 않으면 일어날 수 있는 문제사항들
- Hash-Based Collection에 어떤 객체를 집어넣고, 그 객체의 상태를 바꾸고 다시 집어넣으면 중복이 생김. 동일한 객체인데 hashCode값이 바뀌었고 따라서 Collection은 다른 Bucket에다 중복되게 집어넣음.
- 두 동등(equals)한 객체를 집어넣으면 중복되게 들어감. 대개의 경우 Collection에 동등한 객체들은 중복되서 저장되지 않기를 원하기 때문에 동등한 객체가 hashCode만 다르게 나올 경우 문제가 됨.
