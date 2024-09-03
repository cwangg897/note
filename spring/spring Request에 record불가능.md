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
아마도 aop를 사용하나?..
