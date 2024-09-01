### @SpringBootTest(classes = value)는 어떤 역할인가?
```java
@SpringBootTest(classes = NaverClientTest.TestConfig.class)
@ActiveProfiles("test")
class NaverClientTest {

    @ComponentScan(basePackageClasses = NaverClient.class)
    static class TestConfig{}
```

```
TestConfig.class가 왜 중요한가?
필요한 빈만 로드: 전체 애플리케이션 컨텍스트를 로드하는 대신, 테스트에 필요한 최소한의 빈들만 로드할 수 있게 해줍니다. 이렇게 하면 테스트의 속도와 효율성이 향상됩니다.
테스트 환경 구성: TestConfig는 테스트에 필요한 빈만 포함하거나, 특정 컴포넌트만 스캔하도록 설정할 수 있습니다. 이렇게 하면 테스트 시 불필요한 빈들이 로드되지 않으며, 더 간결한 테스트 컨텍스트를 유지할 수 있습니다.
```


### application.yml test환경에서 사용하려면 test패키지에 만들면 되는것인가?
src/test/resources
application-test.yml 파일은 src/test/resources 폴더에 만들어야 합니다.
이 위치에 파일을 두면, @ActiveProfiles("test")를 사용해 테스트 환경에서 해당 설정이 자동으로 적용됩니다.

```
즉 test폴더이든 main폴더이든 둘다 찾는단느것이야?
ChatGPT의 말:
ChatGPT
네, 맞습니다! Spring Boot는 활성화된 프로파일에 따라 설정 파일을 찾을 때, **src/main/resources**와 src/test/resources 두 경로 모두를 확인합니다.

테스트 환경에서는 src/test/resources 경로에 있는 설정 파일이 src/main/resources 경로의 파일보다 우선적으로 적용됩니다.
따라서 테스트 환경에서는 src/test/resources/application-test.yml의 설정이 적용되지만,
이 파일이 없으면 src/main/resources/application-test.yml이 적용됩니다.
```
