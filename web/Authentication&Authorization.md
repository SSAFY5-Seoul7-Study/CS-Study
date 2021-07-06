# 인증과 승인

두 용어는 보안 측면에서 사용하는 언어이다.  
특히 시스템에 대한 액세스 권한을 얻을 때 서로 함께 사용되는 경우가 많습니다.

![Authentication_Authorization](https://user-images.githubusercontent.com/54837242/124547494-30ffcb80-de67-11eb-8833-d95a0b3e3fb7.jpg)

<br>

## 인증과 승인은 무슨 차이?

### Authentication(인증) cf\_ 에러가 나면 http status code 401

```
사용자를 확인하는 과정입니다. 요청(request)으로 보내온 클라이언트 정보가 DB 서버에 등록되어 있는지를 확인하여 서버가 접속한 주체를 파악합니다.
```

### Authorization(승인) cf\_ 에러가 나면 http status code 403

```
사용자가 해당 페이지에 접속할 권한을 가지고 있는지 확인합니다. 예를 들어 관리자, 일반 사용자, 일회성 게스트 등 유저의 등급에 따라 접속 권한을 부여했을 때 이 권한을 확인하는 작업을 말합니다.

```

<br>

## web에서 인증은 왜 필요한가?

<br>
우리가 이용하는 대부분의 웹 어플리케이션은 HTTP를 통해 통신합니다.
그런데 HTTP는 무상태성(Stateless) 프로토콜이기 때문에, 상태(State)를 유지하고 기억하지 않습니다.

그렇기 때문에 어떤 클라이언트가 보내온 요청인지 서버는 구분하지 못하고, 과거의 정보에 기반하여 클라이언트를 판단할 수도 없습니다.

따라서 서버는 쿠키(Cookie)를 이용해 사용자를 구분하고 확인하는 작업(➡️ 인증)을 하게되었고, 클라이언트로부터 본인만 알 수 있는 등록된 정보를 받아 확인하는 작업을 통해 사용자를 구분하게 되었습니다. 이러한 원리를 기반으로 보안 및 서비스의 특징에 따라 다양한 인증시스템이 만들어지게 되었습니다.

## web Server에 사용처

## API Key

서비스들이 거대해짐에 따라 기능들을 분리하기 시작하였는데 이를위해 Module이나 Application들간의 공유와 독립성을 보장하기 위한 기능들이 등장하기 시작했다.
그 중 제일 먼저 등장하고 가장 널리 보편적으로 쓰이는 기술이 API Key이다.

### 동작방식

1. 사용자는 API Key를 발급받는다. (발급 받는 과정은 서비스들마다 다르다. 예를들어 공공기관 API같은 경우에는 신청에 필요한 양식을 제출하면 관리자가 확인 후 Key를 발급해준다.
2. 해당 API를 사용하기 위해 Key와 함께 요청을 보낸다.
3. Application은 요청이 오면 Key를 통해 User정보를 확인하여 누구의 Key인지 권한이 무엇인지를 확인한다.
4. 해당 Key의 인증과 인가에 따라 데이터를 사용자에게 반환한다.

### 문제점

API Key를 사용자에게 직접 발급하고 해당 Key를 통해 통신을 하기 때문에 통신구간이 암호화가 잘 되어 있더라도 Key가 유출된 경우에 대비하기 힘들다.
그렇기때문에 주기적으로 Key를 업데이트를 해야하기 때문에 번거롭고 예기치 못한 상황(한쪽만 업데이트가 실행되어 서로 매치가 안된다는 등)이 발생할 수 있다. 또한, Key한가지로 정보를 제어하기 때문에 보안문제가 발생하기 쉬운편이다.

## OAuth2

API Key의 단점을 메꾸기 위해 등작한 방식이다. 대표적으로 페이스북, 트위터 등 SNS 로그인기능에서 쉽게 볼 수 있다. 요청하고 요청받는 단순한 방식이 아니라 인증하는 부분이 추가되어 독립적으로 세분화가 이루어졌다.

### 동작방식

1. 사용자가 Application의 기능을 사용하기 위한 요청을 보낸다. (로그인 기능, 특정 정보 열람 등 다양한 곳에서 쓰일 수 있다. 여기에서는 로그인으로 통일하여 설명하겠다.)
2. Application은 해당 사용자가 로그인이 되어 있는지를 확인한다. 로그인이 되어 있지 않다면 다음 단계로 넘어간다.
3. Application은 사용자가 로그인되어 있지 않으면 사용자를 인증서버로 Redirection한다.
4. 간접적으로 Authorize 요청을 받은 인증서버는 해당 사용자가 회원인지 그리고 인증서버에 로그인 되어있는지를 확인한다.
5. 인증을 거쳤으면 사용자가 최초의 요청에 대한 권한이 있는지를 확인한다. 이러한 과정을 Grant라고 하는데 대체적으로 인증서버는 사용자의 의지를 확인하는 Grant처리를 하게 되고, 각 Application은 다시 권한을 관리 할 수도 있다. 이 과정에서 사용자의 Grant가 확인이 되지않으면 다시 사용자에게 Grant요청을 보낸다.
   > _Grant란?_
   > Grant는 인가와는 다른 개념이다. 인가는 서비스 제공자 입장에서 사용자의 권한을 보는 것이지만, Grant는 사용자가 자신의 인증정보(보통 개인정보에 해당하는 이름, 이메일 등)를 Application에 넘길지 말지 결정하는 과정이다.
6. 사용자가 Grant요청을 받게되면 사용자는 해당 인증정보에 대한 허가를 내려준다. 해당 요청을 통해 다시 인증서버에 인가 처리를 위해 요청을 보내게 된다.
7. 인증서버에서 인증과 인가에 대한 과정이 모두 완료되면 Application에게 인가코드를 전달해준다. 인증서버는 해당 인가코드를 자신의 저장소에 저장을 해둔다. 해당 코드는 보안을 위해 매우 짧은 기간동안만 유효하다.
8. 인가 코드는 짧은 시간 유지되기 떄문에 이제 Application은 해당 코드를 Request Token으로 사용하여 인증서버에 요청을 보내게된다.
9. 해당 Request Token을 받은 인증서버는 자신의 저장소에 저장한 코드(7번 과정)과 일치하지를 확인하고 긴 유효기간을 가지고 실제 리소스 접근에 사용하게 될 Access Token을 Application에게 전달한다.
10. 이제 Application은 Access Token을 통해 업무를 처리할 수 있다. 해당 Access Token을 통해 리소스 서버(인증서버와는 다름)에 요청을 하게된다. 하지만 이 과정에서도 리소스 서버는 바로 데이터를 전달하는 것이 아닌 인증서버에 연결하여 해당 토큰이 유효한지 확인을 거치게된다. 해당 토큰이 유효하다면 사용자는 드디어 요청한 정보를 받을 수 있다.

### 문제점

기존 API Key방식에 비해 좀 더 복잡한 구조를 가진다. 물론 많은 부분이 개선되었다.
하지만 통신에 사용하는 Token은 무의미한 문자열을 가지고 기본적으로 정해진 규칙없이 발행되기 때문에 증명확인 필요하다. 그렇기에 인증서버에 어떤 식이든 DBMS 접근이든 다른 API를 활용하여 접근하는 등의 유효성 확인 작업이 필요하다는 공증 여부 문제가 있다. 이러한 공증여부 문제뿐만 아니라 유효기간 문제도 있다.

## JWT

JWT는 JSON Web Token의 줄임말로 인증 흐름의 규약이 아닌 Token 작성에 대한 규약이다. 기본적인 Access Token은 의미가 없는 문자열로 이루어져 있어 Token의 진위나 유효성을 매번 확인해야 하는 것임에 반하여, JWT는 인증여부 확인을 위한 값, 유효성 검증을 위한 값 그리고 인증 정보 자체를 담고 있기 때문에 인증서버에 묻지 않고도 사용할 수 있다.
토큰에 대한 자세한 내용과 인증방식은 [JWT문서](<https://github.com/kim6394/tech-interview-for-developer/blob/master/Web/JWT(JSON%20Web%20Token).md>)를 참조하자.

### 문제점

서버에 직접 연결하여 인증을 학인하지 않아도 되기 때문에 생기는 장점들이 많다. 하지만 토큰 자체가 인증 정보를 가지고 있기때문에 민감한 정보는 인증서버에 다시 접속하는 과정이 필요하다.

### 참고 사이트

- https://medium.com/@audira98/authorization-and-authentication-cd0a7c994278
- https://auth0.com/docs/flows/authorization-code-flow
- https://auth0.com/docs/flows

### cf\_...

1. 자격증명
   ```
   자격증명은 제 3자로(보통 인증기관)부터 개인에게 발행된 자격 허가 증명서입니다.
   ```
   ![auth-sequence-auth-code](https://user-images.githubusercontent.com/54837242/124550476-aa012200-de6b-11eb-962e-5c6e792d3177.png)