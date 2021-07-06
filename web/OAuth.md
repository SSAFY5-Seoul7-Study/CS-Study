OAuth
==================
> Open Authentification

인증을 위한 오픈 스탠더드 프로토콜로, 사용자가 Facebook이나 트위터 같은 인터넷 서비스의 기능을 다른 애플리케이션(데스크톱, 웹, 모바일 등)에서도 사용할 수 있게 한 것.

```
배경

- 서비스 중에서 사용자가 일부 필요한 것만 사용할 수 있게 한다는 것.
- 로그인해야 하는 것이 아니라, 별도의 인증 절차를 거치면 다른 서비스에서 Facebook과 트위터의 기능을 이용할 수 있게 되는 것.
```

### 기억해야할 점!

* Facebook, 트위터, 아마존 등 애플리케이션마다 제각각인 인증방식을 표준화한 인증방식이다.

* OAuth를 이용하면 이 인증을 공유하는 애플리케이션끼리는 별도의 인증이 필요없어 여러 애플리케이션을 통합하여 사용하는 것이 가능하게 된다.

### OAuth1.0 동작 방식

|용어|설명|
|------|---|
|User|Service Provider에 계정을 가지고 있으면서, Consumer를 이용하려는 사용자|
|Consumer|OAuth를 사용하는 Open API를 제공하는 서비스|
|Service Provider|OAuth 인증을 사용해 Service Provider의 기능을 사용하려는 애플리케이션이나 웹 서비스|
|Request Token|Consumer가 Service Provider에게 접근 권한을 인증받기 위해 사용하는 값. 인증이 완료된 후에는 Access Token으로 교환|
|Access Token|인증 후 Consumer가 Service Provider의 자원에 접근하기 위한 키를 포함한 값|

![image](https://user-images.githubusercontent.com/17819249/124583203-c1e99d80-de8d-11eb-99a2-fc0452c5b13c.png)

1. Consumer가 Service Provider에게 Request Token을 요청한다.
2. Service Provider가 Consumer에게 Request Token을 발급해준다.
3. Consumer가 User를 Service Provider로 이동시킨다. 여기서 User 인증이 수행된다.
4. Service Provider가 User를 Consumer로 이동시킨다.
5. Consumer가 Access Token을 요청한다.
6. Service Provider가 Access Token을 발급한다.
7. 발급된 Access Token을 이용하여 Consumer에서 User 정보에 접근한다.

### 예시
![스크린샷 2021-07-06 오후 7 17 37](https://user-images.githubusercontent.com/17819249/124584127-d8442900-de8e-11eb-8ff8-f3bf5ba6fb68.png)

**방문증으로 사전에 허락된 공간에만 출입이 가능하다.**

즉, Access Token(방문증)을 갖고 있는 Consumer는 사전에 호출이 허락된 Service Provider의 오픈 API를 호출할 수 있는 것이다!

### OAuth2.0

OAuth1.0의 여러 단점들을 개선한 것으로 최종안은 없지만 여러 인터넷 서비스(페이스북, 구글, 아마존 등)에서 사용하고 있다.

**특징**
- 웹 애플리케이션이 아닌 애플리케이션 지원 강화
- 암호화가 필요 없음 HTTPS를 사용하고 HMAC을 사용하지 않는다.
- Siganature 단순화 정렬과 URL 인코딩이 필요 없다.
- Access Token 갱신 OAuth 1.0에서 Access Token을 받으면 Access Token을 계속 사용할 수 있었다. OAuth 2.0에서는 보안 강화를 위해 Access Token의 Life-time을 지정할 수 있도록 했다.

![image](https://user-images.githubusercontent.com/17819249/124584644-746e3000-de8f-11eb-84a8-890eefe9e8a0.png)

### 참고
[네이버 D2 - OAuth와 춤을](https://d2.naver.com/helloworld/24942)

[OAuth](https://ko.wikipedia.org/wiki/OAuth)
