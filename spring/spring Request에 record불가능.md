### 문제상황
저는 dto는 record타입으로 만들면 보일러플레이트로 편한 줄 알았다.
그래서 @RequestParam도 record로 만들려고했다. 그러나 불가능하다. 
왜냐하면 Spring 동작 메커니즘은 아래와 같다.

### Spring Boot @RequestParam메커니즘
Spring Boot에서 @RequestParam을 사용하여 HTTP 요청의 쿼리 파라미터를 클래스(DTO)로 바인딩할 때,  <br>
Java의 record 타입을 사용하는 것이 불가능하거나 적합하지 않은 이유는 다음과 같습니다 <br>
Spring의 바인딩 메커니즘 <br>
Spring에서는 @RequestParam을 사용하여 쿼리 파라미터를 메소드 파라미터에 직접 바인딩하거나, DTO로 바인딩할 수 있습니다. <br>
이 바인딩 과정에서 Spring은 기본적으로 기본 생성자와 Setter 메서드를 사용하여 파라미터 값을 객체에 할당합니다. <br>

### 궁금증
```
Spring의 데이터 바인딩 메커니즘은 다음과 같은 과정을 거칩니다:
객체 생성: 먼저 바인딩 대상이 되는 객체가 생성됩니다. 이때 주로 기본 생성자가 사용됩니다.
객체 생성 후, Spring은 리플렉션(Reflection)이나 Setter 메서드를 사용하여 HTTP 요청의 파라미터 값을 해당 필드에 할당합니다.
Setter 메서드가 없고, 리플렉션을 통한 필드 접근을 피하고 싶을 때, Spring은 생성자 주입 방식을 사용할 수 있습니다.
이를 위해 기본 생성자가 필요합니다. 매개변수를 요구하는 생성자가 있으면, Spring은 그 생성자를 통해 객체를 생성하기 어렵고, 따라서 기본 생성자를 선호합니다.
```

### 정리 @RequestParam과 @RequestBody는 주입방법이 다르다
@RequestBody는 로는 기본생성자를 이용하며 setter나 리플렉션이나을 사용하지만 생성자 주입을 주로 사용한다. <br>
그래서 record타입이 사용가능하다 <br>
<br>
@RequestParam은 기본적으로 Setter 메서드를 통해 파라미터 값을 객체에 주입합니다.<br>
만약 Setter 메서드가 없으면, Spring은 리플렉션을 통해 필드에 직접 접근하지 않으며, 그래서 dto로 @Requestparam을 사용하면 @Setter를 달아주어야한다 <br>
그래서 record타입을 사용 불가능하다  <br>

### 이렇게 가능하다
```java
public PageResult<SearchResponse> search(@Valid SearchRequest request){
        return bookQueryService.search(request.getQuery(), request.getPage(), request.getSize());
    }
```

