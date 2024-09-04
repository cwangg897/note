### 둘의 차이점은?
Arrays.asList()와 List.of()
자바에서 보통 List로 변환하기 위해서는 Arrays.asList(array)를 사용합니다.

Java 9 버전 부터는 List.of(array)라는 새로운 팩토리 메소드가 있습니다.


### 변경 가능 여부 (Mutable / Immutable)
Arrays.asList()에서 반환된 List는 변경이 가능합니다.
하지만, List.of()에서 반환된 List는 변경이 불가능합니다.
대표적으로 set() 메서드를 사용해보면 둘의 차이를 알 수 있습니다.
```java
List<Integer> list = Arrays.asList(1, 2, null);
list.set(1, 10); // OK

List<Integer> list = List.of(1, 2, 3);
list.set(1, 10); // Fails with UnsupportedOperationException
```
이유는 Arrays.asList()는 ArrayList를 반환하고, set() 메서드가 구현돼 있습니다.
(Arrays 내부 클래스 ArrayList)

(참고) Arrays.asList()가 반환하는 ArrayList 타입은 java.util.ArrayList가 가 아니라 Arrays 내부 클래스입니다. 
add()와 remove() 메서드는 구현되어 있지 않아서, 배열의 크기 변동과 관련된 행동은 할 수 없습니다.

반면, List.of()는 ListN이라는 타입의 객체를 반환하는데, 이는 불변 객체(Immutable object)입니다. 따라서 수정할 수 없습니다.

![image](https://github.com/user-attachments/assets/5fc048d2-428c-44bf-8d40-4e3bb698ec55)
