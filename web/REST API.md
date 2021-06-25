### API ( Application Programming Interface )

- 어플리케이션에서 사용할 수 있도록, 운영체제나 프로그래밍 언어가 제공하는 **기능을 제어**할 수 있게 만든 인터페이스

### REST API

---

REST(REpresentational State Transfer)

- 자원의 표현을 통해 상태(정보)를 주고받는 모든 것을 의미
- URI를 통해서 자원을 명시하고, HTTP Method를 통해 동작(CRUD)을 처리

#### 1. REST (<u>RE</u>presentational <u>S</u>tate <u>T</u>ransfer) 기본

- REST의 요소

  - Method

    | Method | 의미   | Idempotent |
    | ------ | ------ | ---------- |
    | POST   | Create | No         |
    | GET    | Select | Yes        |
    | PUT    | Update | Yes        |
    | DELETE | Delete | Yes        |

    > Idempotent : 한 번 수행하냐, 여러 번 수행했을 때 결과가 같나?

    <br>

  - Resource

    - http://myweb/users와 같은 URI
    - 모든 것을 Resource (명사)로 표현하고, 세부 Resource에는 id를 붙임

    <br>

  - Message

    - 메시지 포맷이 존재

      : JSON, XML 과 같은 형태가 있음 (최근에는 JSON 을 씀)

      ```text
      HTTP POST, http://myweb/users/
      {
      	"users" : {
      		"name" : "terry"
      	}
      }
      ```

    <br>

* Restful API

  - REST 기반으로 서비스 API를 구성하는 것, (확장성, 재사용성, 유지 보수) <br><br>

* REST 특징

  - 6가지 원칙

    - Uniform Interface : URI로 지정한 리소스에 대한 조작을 인터페이스로 수행

      - 예) REST API 정의를 HTTP + JSON로 하였다면, C, Java, Python, IOS 플랫폼 등 특정 언어나 기술에 종속 받지 않고, 모든 플랫폼에 사용이 가능한 Loosely Coupling 구조 <br><br>

    - Stateless: 무상태성 (세션, 쿠키를 저장하고 관리하지 않음)

      - 즉, HTTP Session과 같은 컨텍스트 저장소에 **<u>상태 정보 저장 안함</u>**
      - **<u>Request만 Message로 처리</u>**하면 되고, 컨텍스트 정보를 신경쓰지 않아도 되므로, **<u>구현이 단순해짐</u>**.
      - 따라서, REST API 실행중 실패가 발생한 경우, Transaction 복구를 위해 기존의 상태를 저장할 필요가 있다. (POST Method 제외)<br><br>

    - Caching: HTTP의 캐싱기능 적용 가능 (GET)
    - Self-descriptiveness: 자체 표현 구조 (메시지만 보고도 이를 쉽게 이해할 수 있는 자체 표현 구현 구조)
    - Client-Server: 클라이언트와 서버의 역할이 구분
    - Hierachical System: 다중 계층으로 구성

  - Resource 지향 아키텍쳐 (ROA : Resource Oriented Architecture)

    - Resource 기반의 복수형 명사 형태의 정의를 권장.(url이 곧 정의)

### 아직 모르는 것들

      * Resource Identification In Requests

      * Resource Manipulation Through Representations

      * Code On Demand(Optional)
