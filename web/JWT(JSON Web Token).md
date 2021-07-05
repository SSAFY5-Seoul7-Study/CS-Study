# JWT

## 쿠키 & 세션 복습

![image](https://user-images.githubusercontent.com/24283422/124378316-a47cce00-dceb-11eb-9552-f88d01405eb6.png)

- 장점
  - HTTP 요청이 노출되더라도 유저 정보가 아닌 세션 ID만 노출됨 (= 쿠키보다 보안상 이점)
  - 별도의 확인 없이 세션 저장소를 통해 클라이언트의 고유 ID로 식별 가능
- 단점
  - 하이재킹 공격 : HTTP 요청을 가로채서 훔친 세션 ID로 서버와 통신하여 유저 정보를 가져옴 (해결책 : HTTP Request 정보 암호화, 세션 유효시간 부여)
  - 서버에서 추가적인 저장 공간(세션 저장소) 필요 -> 부하 ↑

<br/>

## 서버 기반 인증 vs 토큰 기반 인증

### 서버 기반 인증

![image](https://user-images.githubusercontent.com/24283422/124378897-ee1ae800-dcee-11eb-98c6-579417a6b25a.png)

- = 세션 기반 인증
- 서버 측에서 유저들의 정보 기억(저장)
- 단점
  - 메모리 과부화
  - 확장성 문제
  - CORS(Cross-Origin Resource Sharing)

<br/>

### 토큰 기반 인증

![image](https://user-images.githubusercontent.com/24283422/124378902-f83ce680-dcee-11eb-963d-26430d23cb76.png)

- 유저의 정보를 서버나 세션에 담아두지 않는다(stateless)
  - 메모리 과부화, 확장성 문제 해결
- 특징
  - 무상태(stateless) & 확장성(scalability)
  - 보안성
  - 확장성(Extensibility)
  - 여러 플랫폼 및 도메인

<br/>

## JWT

- JSON 포맷을 이용하여 사용자에 대한 속성을 저장하는 Claim 기반의 Web Token
- 토큰 자체를 정보로 사용하는 Self-Contained 방식으로 정보를 안전하게 전달
- JWT는 서버와 클라이언트 간 정보를 주고 받을 때 HTTP Request Header에 JSON Token을 넣은 후 서버는 Header에 포함되어 있는 JWT 정보를 통해 인증하는 방식
- 서버에서 유저 세션을 유지할 필요가 없고 가볍게 데이터를 주고받을 수 있다.

<br/>

## JWT 구조

![image](https://user-images.githubusercontent.com/24283422/124471617-0c104780-ddd8-11eb-925c-67adda04cab1.png)

- Header, Payload, Signature의 3 부분으로 이루어짐
- Base64로 인코딩되어 표현(전달)
- 각각의 부분을 이어 주기 위해 . 구분자를 사용하여 구분

<br/>

### Header(헤더)

- JWT 토큰을 어떻게 해석해야 하는지를 알려주는 부분
- alg, typ로 구성
- alg: 해싱 알고리즘 방식, 서명(Signature) 및 토큰 검증에 사용 ex) HS256(SHA256) 또는 RSA
- typ: 토큰 타입 ex) JWT

```
{
   "alg": "HS256",
   "typ": JWT
}
```

<br/>

### Payload(내용)

- 토큰에서 사용할 정보의 조각들인 클레임(Claim)이 담겨 있음
- 페이로드에 있는 속성들을 클레임 셋(Claim Set)이라고 함
- JSON 형태로 다수의 정보를 넣을 수 있음
- 등록된 클레임, 공개 클래임, 비공개 클래임으로 구분

<br/>

> 등록된 클레임(Registered Claim)

토큰 정보를 표현하기 위해 이미 정해진 종류의 데이터

- `iss`: 토큰 발급자(issuer)
- `sub`: 토큰 제목(subject)
- `aud`: 토큰 대상자(audience)
- `exp`: 토큰 만료 시간(expiration), NumericDate 형식으로 되어 있어야 함 ex) 1480849147370
- `nbf`: 토큰 활성 날짜(not before), 이 날이 지나기 전의 토큰은 활성화되지 않음
- `iat`: 토큰 발급 시간(issued at), 토큰 발급 이후의 경과 시간을 알 수 있음
- `jti`: JWT 토큰 식별자(JWT ID), 중복 방지를 위해 사용하며, 일회용 토큰(Access Token) 등에 사용

<br/>

> 공개 클레임(Public Claim)

사용자 정의 클레임

- 공개용 정보를 위해 사용
- 충돌 방지를 위해 URI 포맷을 이용

```
{
    "https://klydata.tistory.com": true
}
```

<br/>

> 비공개 클레임(Private Claim)

사용자 정의 클레임

- 서버와 클라이언트 사이에 임의로 지정한 정보를 저장
- 충돌이 일어날 수 있으므로 조심해서 사용해야 함

```
{
    "token_type": access
}
```

<br/>

### Signature(서명)

- 토큰을 인코딩하거나 유효성 검증을 할 때 사용하는 고유한 암호화 코드
- 헤더(Header)와 페이로드(Payload)의 값을 각각 BASE64로 인코딩하고, 인코딩한 값을 비밀 키를 이용해 헤더(Header)에서 정의한 알고리즘으로 해싱을 하고, 이 값을 다시 BASE64로 인코딩하여 생성

<br/>

## JWT 인증과정 ⭐⭐⭐

### Access Token만 사용

![image](https://user-images.githubusercontent.com/24283422/124477084-8fcd3280-ddde-11eb-8020-1347e26516fb.png)

1. 사용자가 로그인을 한다.
2. 서버에서는 계정정보를 읽어 사용자를 확인 후, 사용자의 고유한 ID값을 부여한 후, 기타 정보와 함께 Payload에 넣습니다.
3. JWT 토큰의 유효기간을 설정합니다.
4. 암호화할 SECRET KEY를 이용해 ACCESS TOKEN을 발급합니다.
5. 사용자는 Access Token을 받아 저장한 후, 인증이 필요한 요청마다 토큰을 헤더에 실어 보냅니다.
6. 서버에서는 해당 토큰의 Verify Signature를 SECRET KEY로 복호화한 후, 조작 여부, 유효기간을 확인합니다.
7. 검증이 완료된다면, Payload를 디코딩하여 사용자의 ID에 맞는 데이터를 가져옵니다.

> 단점

이미 발급된 JWT에 대해서는 돌이킬 수 없다. 따라서 악의적인 사용자는 유효기간이 지나기 전까지 정보들을 털어갈 수 있다. 즉, 제 3자에게 탈취당할 경우 보안에 취약하다.

> 해결책

기존의 Access Token의 유효기간을 짧게 하고 Refresh Token이라는 새로운 토큰을 발급한다. 이렇게 되면 Access Token을 탈취당해도 상대적으로 피해를 줄일 수 있다.

<br/>

### Access Token + Refresh Token 사용 ⭐⭐⭐

**Refresh Token**

- Access Token과 똑같은 형태의 JWT
- 처음에 로그인을 완료했을 때 Access Token과 동시에 발급
- 긴 유효기간을 가지면서 Access Token이 만료됐을 때 새로 발급해주는 열쇠의 역할
- Access Token의 유효기간을 짧게 줄여 노출되는 시간을 줄이고 만료시 Refresh Token으로 갱신

![image](https://user-images.githubusercontent.com/24283422/124478122-d0797b80-dddf-11eb-9f22-8876a670f7f8.png)

1. 사용자가 ID , PW를 통해 로그인한다.

2. 서버에서는 회원 DB에서 값을 비교한다.

3~4. 로그인이 완료되면 Access Token, Refresh Token을 발급한다. 이때 일반적으로 회원DB에 Refresh Token을 저장해둔다.

5. 사용자는 Refresh Token은 안전한 저장소에 저장 후, Access Token을 헤더에 실어 요청을 보낸다.

6~7. Access Token을 검증하여 이에 맞는 데이터를 보낸다.

8. 시간이 지나 Access Token이 만료됐다.

9. 사용자는 이전과 동일하게 Access Token을 헤더에 실어 요청을 보낸다.

10~11. 서버는 Access Token이 만료됨을 확인하고 권한없음을 신호로 보낸다.

12. 사용자는 Refresh Token과 Access Token을 함께 서버로 보낸다.

13. 서버는 받은 Access Token이 조작되지 않았는지 확인한 후, Refresh Token과 사용자의 DB에 저장되어 있던 Refresh Token을 비교한다. Token이 동일하고 유효기간도 지나지 않았다면 새로운 Access Token을 발급해준다.

14. 서버는 새로운 Access Token을 헤더에 실어 다시 API 요청을 진행한다.

#

## 참고

- https://mangkyu.tistory.com/56
- https://tansfil.tistory.com/58
- https://velog.io/@djaxornwkd12/%EC%84%B8%EC%85%98-%EA%B8%B0%EB%B0%98-%EC%9D%B8%EC%A6%9D-%EB%B0%A9%EC%8B%9D-vs-%ED%86%A0%ED%81%B0-%EA%B8%B0%EB%B0%98-%EC%9D%B8%EC%A6%9D
