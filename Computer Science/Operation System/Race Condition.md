Race Condition
============================

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
```

## Race Condition이면 무슨 문제가 있을까?

<br>


- Mutual exclusion (상호배제) : 프로세스가 공용 데이터 사용하고 있으면 그 자원을 사용하지 못하도록 막거나, 다른 프로세스가 그 자원을 사용하지 못하도록 막는 것
- DeadLock (데드락) : 두 자원이 필요한 프로세스가 프로그램을 수행할 때까지 이미 소유한 리소스를 해제하지 않아 교착상태에 빠짐
- Starvation (기아상태) : 두 개 이상의 작업이 서로 상대방의 작업이 끝나기만 기다리고 있기 때문에 결과적으로 아무것도 완료되지 못함

<br>


## 이러한 문제들 해결 방법

```
커널 내부에 있는 각 공유 데이터에 접근 할 때마다
그 데이터에 대한 lock/unlock을 하는 방법 
-> Semaphore / Mutex로 해결
```

### Semaphore (세마포어)

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbDhIrM%2Fbtq74EQfeTs%2FJxCHMj7iLcBjuKpY892f6k%2Fimg.png)

- 공유 데이터에 여러 프로세스가 접근하는 것을 막는 것
- 

### Mutex (뮤텍스)

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FqIr0n%2Fbtq74aosXsv%2F8bUjzWTlvtBC3RjGP8upKK%2Fimg.png)


