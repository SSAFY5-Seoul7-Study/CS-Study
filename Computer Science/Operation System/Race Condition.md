# Race Condition

## Race Condition (경쟁상태)

<br>

- 두 개 이상의 프로세스가 공통 자원에 동시에 접근할 때, 공용 데이터에 대한 접근 순서가 실행 결과에 영향을 주는 상태
- 하나의 자원을 놓고 서로 사용하려고 경쟁하는 상황
- 교착상태(DeadLock)의 종류 중 하나

```
DeadLock : 프로세스가 자원을 얻지 못해 다음 처리를 하지 못하는 상태
```

## 왜 Race Condition이 발생할까?

<br>

```
1. 프로세스 : IPC(Inter Process Communication)
    -> 2개의 CPU가 동시에 커널 내부의 공유 데이터에 접근하여 조작하는 경우
2. 스레드 : 한 프로세스 내부에서 data영역에 동시 접근할 수 있는 2개 이상의 스레드
    -> 멀티 스레드 환경에서 공통 자원을 병행하여 작업할 때

=> 동시 접근 시 자료의 일관성을 해치는 결과가 나타날 수 있음
```

## Race Condition에서 문제 해결에 필요한 조건

<br>

```
임계구역(Critical Section) : 여러 프로세스가 데이터 공유를 할 때, 공유 데이터를 접근하는 코드부분
```

- 상호배제 (Mutual Exclusion) : 한번에 하나의 프로세스만 독점적으로 임계구역에 접근해야한다
- 진행 (Progress) : 경쟁하는 프로세스가 없으면 바로 임계구역에 들어갈 수 있도록 보장
- 한정된 대기 (Bounded Waiting) : 한 프로세스가 임계구역 진입 요청 후에는 무한정 기다리지 않는다

<br>

## 이러한 문제들 해결 방법

```
각 공유 데이터에 접근 할 때마다
그 데이터에 대한 lock/unlock을 하는 방법
-> Semaphore / Mutex로 해결
```

## 동기화기법

- 두 개 이상의 프로세스를 한 시점에서는 동시에 처리할 수 없으므로 각 프로세스에 대한 처리 순서를 결정하는 것으로 상호배제함.

<br>

### Semaphore (세마포어)

- 공유 데이터에 여러 프로세스가 접근하는 것을 막는 것
- 현재 공유자원에 접근할 수 있는 스레드, 프로세스 수를 나타내는 값을 두어
- 비교적 긴 시간을 확보하는 리소스에 대해 이용
- 운영체제의 리소스를 경쟁적으로 사용하는 다중 프로세스에서 행동을 조정하거나 또는 동기화 시키는 기술

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbDhIrM%2Fbtq74EQfeTs%2FJxCHMj7iLcBjuKpY892f6k%2Fimg.png)

<br>

### Mutex (뮤텍스)

- 공유 데이터에 여러 스레드가 접근하는 것을 막는 것
- 다중 프로세스들이 공유 리소스에 대한 접근하는 것을 조율하기 위해 locking과 unlocking 사용
- 두 쓰레드가 동시에 사용할 수 없음
  ![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FqIr0n%2Fbtq74aosXsv%2F8bUjzWTlvtBC3RjGP8upKK%2Fimg.png)

<br>

### 세마포어와 뮤텍스의 차이는?

- 세미포어 -> 뮤텍스 (o) , 뮤텍스 -> 세미포어 (x)
- 세미포어는 파일형태로 존재, 뮤텍스는 프로세스 범위에 존재?
- 뮤텍스를 소유하고 있는 스레드가 뮤텍스를 해제할 수 있음
- 세마포어를 소유하지 않은 스레드도 세마포어를 해제 가능
