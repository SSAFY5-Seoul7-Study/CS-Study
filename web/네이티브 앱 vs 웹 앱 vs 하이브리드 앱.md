네이티브 앱 vs 웹 앱 vs 하이브리드 앱
==================
## 네이티브 앱

![image](https://user-images.githubusercontent.com/17819249/123209566-c318e300-d4fb-11eb-9964-d724619d60ab.png)

흔히 말하는 '애플리케이션'을 의미한다.

모바일 기기에 최적화 된 언어로 개발된 앱으로 안드로이드 SDK를 이용해 Java/Kotlin 언어 그리고 iOS SDK를 이용해 Swift/Flutter 언어로 만드는 대부분의 앱.

- **장점**
    - 성능이 웹앱, 하이브리드 앱에 비해 가장 높다.
    - 네이티브 API를 사용함으로써 플랫폼과 밀착되어 있다.
    - 해당 언어에 익숙한 사용자라면 좀 더 쉽게 접근 가능하다.

- **단점**
    - 플랫폼에 한정적이다.
    - 해당 플랫폼에서 요구하는 언어에 제약적이다.

```
예) 계산기, 노트 등 폰에 기본적으로 내장되어있는 앱들, 대부분의 게임
```

#

## 웹 앱

![image](https://user-images.githubusercontent.com/17819249/123209718-fd828000-d4fb-11eb-912b-12c100ec221e.png)

모바일 웹 + 네이티브 앱을 결합한 형태.

모바일 웹의 특징을 가지면서 네이티브 앱의 장점을 갖고 있어 모바일 웹 보다는 조금 더 모바일에 최적화 된 앱을 의미한다. 

웹 앱도 일반적인 웹기술로 개발되고 풀 브라우저 방식이 아닌 단일 페이지 방식(SPA)으로 화면을 진화해 속도가 빠르다는 장점이 있다.

> 모바일 웹 : PC용 홈페이지를 모바일 스크린 크기에 맞춰 줄여 놓은 것.(반응형)

- **장점**
    - 웹 사이트를 보는 것이기 때문에 따로 설치할 필요 없다.
    - 모든 기기와 브라우저에서 접근 가능하다.
    - 별도 설치 및 승인 과정이 필요치 않아 유지보수에 용이하다.

- **단점**
    - 플랫폼 API (카메라 등) 을 사용할 수 없고 오로지 브라우저 API만을 사용할 수 있다.
    - 친화적인 터치 앱을 개발하기가 약간 번거로운 점이 있다.
    - 네이티브, 하이브리드 앱보다 실행이 까다롭다. (브라우저를 열고 URL을 검색해 들어가야 한다.)

#

## 하이브리드 앱

![image](https://user-images.githubusercontent.com/17819249/123211152-01af9d00-d4fe-11eb-9303-a843802dedcf.png)

네이티브 앱 + 웹 앱.

네이티브 앱에 웹 view를 띄워 웹 앱을 실행시키는 것이기에 양쪽 API 모두 사용 가능한 점이 큰 장점.

- **장점**
    - 네이티브 API 와 브라우저 API를 모두 이용한 다양한 개발이 가능하다.
    - 웹 개발 기술을 사용해 앱을 개발할 수 있다.
    - 한 번의 개발로 다수의 플랫폼에 대응할 수 있다.

- **단점**
    - 네이티브 기능에 접근하기 위해선 네이티브 개발 지식이 결국 필요하다.
    - 웹 view에서 앱을 실행하는 경우이기 때문에 앱의 성능이 곧 브라우저의 성능 이다.
    - UI 프레임워크 도구를 사용하지 않는다면 개발자가 UI를 제작해야 합니다.

```
예) 인스타그램, Gmail, 금융기관 앱(우리은행, 신한은행, 농협은행) 등

- 주로 은행권에서 앱을 만들 때 "하이브리드 앱"으로 만듦.
- 수시로 배포하는데 네이티브 앱으로 만들면 고객이 매번 업데이트를 새로 설치하면서 받아야하기 때문.
```

출처 : [모바일](https://m.blog.naver.com/acornedu/221012420292)
