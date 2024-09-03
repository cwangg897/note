

### 다른 모듈에서 의존성을 가져와야할 때
루트나 다른곳에서 사용할떄는 api를 사용한다
프로젝트 외부에서도 이 의존성을 노출해야 할 때 사용합니다. 
naver에있는것을 search-api에서 사용해야하는경우


## 왜 이렇게 설정해야하나?
의존성 자체는 가져오지못한다 그러나 재사용성 클래스나 이런것은 가져올 수 있는거 같다 <br>
사용하는 모듈에서도 패키지 안에있는 것도 접근할 수 있게 한다. <br>

### naver-client
```gradle
jar.enabled = true


dependencies {
    implementation project(':common')
    // https://mvnrepository.com/artifact/org.springframework.cloud/spring-cloud-starter-openfeign
    api 'org.springframework.cloud:spring-cloud-starter-openfeign'
    // 버전간 충돌때문에 손쉽게 관리위해 의존성 관리 수단 제공해줌
}
```

### search-api
```gradle
dependencies {
    implementation project(':common')
    implementation project(':external:naver-client')
}
```
