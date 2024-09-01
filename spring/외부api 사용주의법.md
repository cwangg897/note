### 코드
```java
@Override
    public Exception decode(String methodKey, Response response) {
        // 여기에 로직 적어두면 에러발생하면 여기서 처리하게 된다.
        try {
            //이 코드는 HTTP 응답의 본문을 InputStream으로 읽고, 이 스트림의 모든 바이트를 byte[] 배열로 변환한 후,
            // UTF-8 인코딩을 사용하여 이 바이트 배열을 문자열로 변환하는 작업을 수행합니다.
            String body = new String(response.body().asInputStream().readAllBytes(),
                StandardCharsets.UTF_8);
            NaverErrorResponse naverErrorResponse = objectMapper.readValue(body,
                NaverErrorResponse.class);// 여기서 이렇게 매핑하면 NaverErrorResponse이 나온다
            throw new RuntimeException(naverErrorResponse.getErrorMessage());
        } catch (IOException e) { // 파싱 실패시에도
            throw new RuntimeException(e);
        }
    }
```


### 주의 1: 외부 api에서 보내는 에러 형식
```
네이버 외부 api를 사용하면서 느낀점은 따로 디코더를 만들어야한다는 점과
이에대해 예외가 발생할 경우 처리하는것을 따로 만들어주어야하는게 매우중요하다
오류코드를 보고 어떻게 예외메시지를 보내주는지 알아야한다
외부api마다 다르니까 여기에 맞는 api를 만들기위해서 NaverErrorDecoder로 만들어서 예외처리하는거
```

### 주의 2. 파싱실패시 보내는거
파싱실패시에도 에러 처리해줘야하는데 이부분도 추가해야한다.
