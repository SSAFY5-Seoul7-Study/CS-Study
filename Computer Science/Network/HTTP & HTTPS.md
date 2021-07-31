# HTTP & HTTPS

### HTTP

- Hypertext Transfer Protocol 기초적인 통신 규약
- 클라이언트가 자원을 서버에 요청하고 서버에서 응답하여 정보를 제공할 때 사용

#

### HTTP 프로토콜 특징

- 비연결성(Connectionless) : 클라이언트와 서버가 한 번 연결을 맺은 후, 클 라이언트 요청에 대해 서버가 응답을 마치면 맺었던 연결을 끊어 버리는 성질

```
Why? 서버와 다수의 클라이언트를 연결을 유지하기 위한 리소스 발생!
-> 연결 유지를 위한 리소스를 줄이면 더 많은 연결이 가능! But, 연결/해제에 대한 오버헤드 발생 (KeppAlive 속성 사용)

```

- 무상태(stateless) : 서버가 클라이언트를 식별할 수 없음.

```
상태 저장
쿠키(Cookie) : 클라이언트에 저장
세션(Session) : 서버에 저장
```

텍스트 기반으로 네트워크에서 보안에 취약 -> HTTPS

### HTTPS

- Hyper Text Transfer Protocol Secure, HTTP에 데이터 암호화가 추가된 프로토콜 (SSL - Secure Socket Layer)
- 네트워크 상에서 중간에 제3자가 정보를 볼 수 없도록 암호화 방식 이용

![image](https://i.imgur.com/tq9mmGg.png)

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FOKcog%2FbtqK71fM8a4%2Fg1HmcDOR7MVRRz7pSKKJWk%2Fimg.png)

### HTTPS 동작 과정

- 공인된 '인증 기관'에게 내 서버의 '주민등록증'(SSL인증서)을 발급받고, '브라우저'와 통신할 때마다 제시하며 "나 인증받은 서버야." 라고 알리는 방식(HTTPS)이다.
- SSL : SSL 인증서를 통해 서버의 신원을 확인하고 데이터를 암호화 하여 통신하는 보안 방식

출처: https://curryyou.tistory.com/207 [카레유]

- 공개키 암호화 방식과 대칭키 암호화 방식 함께 사용

![image](https://t1.daumcdn.net/cfile/tistory/99F0FA445C456BB809)
웹브라우저 : 인증기관 공개키(인증서 복호화)
<br>
인증서 : 사이트 정보, 공개키
![image](https://t1.daumcdn.net/cfile/tistory/993364345C457AED30)
![image](https://t1.daumcdn.net/cfile/tistory/9997354E5C457AF229)

[출처: HTTP 특성(비연결성, 무상태)과 구성요소 그리고 Restful API](https://victorydntmd.tistory.com/286)

[출처 : [Web] HTTP와 HTTPS 및 차이점](https://mangkyu.tistory.com/98)
