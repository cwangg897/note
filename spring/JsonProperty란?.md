### 왜 사용할까?
외부api연동을 하면서 자바의 카멜케이스나 변수명을 다르게 사용하고싶은경우 사용하게 된다 <br>
JSON키값이 매핑이 가능하다. <br>
```java
@JsonProperty("pubdate")
    private String pudDate;
```

### 번외
만약 필드가 너무 길어지게되고 상대편이 스네이크 케이스면 <br>
@JsonNaming을 붙여주면 편해진다 <br>
![image](https://github.com/user-attachments/assets/d8df283c-8f16-402c-a21e-0e748ae0f04e)

### JSON값 변환시켜서 넣을려면
그리고 바로 넣을려면 Getter필수
