## 세마포어(Semaphore) & 뮤텍스(Mutex)

### 간단한 정리
###### 1. Critical Section (임계 영역)
```
보호되어야할 영역, 공유 자원에 접근할 때 문제가 발생하지 않도록
한 번에 하나의 프로세스만 이용하도록 보장해줘야 하는 영역, 각 프로세스에서 공유데이터를 접근하는 코드 부분을 말함
```

###### 2. 임계 영역 문제 해결하기 위한 조건 3가지 -> [지난 발표 자료 참고](https://github.com/SSAFY5-Seoul7-Study/CS-Study/blob/main/Computer%20Science/Operation%20System/Race%20Condition.md)
```
- 상호배제(Mutual Exclution)
- 진행(Progress)
- 한정대기(Bounded Waiting)
```

###### 3. 임계 영역의 동시 접근을 해결하기 위한 방법 

```
- 락
- 세마포어
- 모니터
```

###### 4. 동기화
```
두 개 이상의 프로세스를 한 시점에서는 동시에 처리할 수 없으므로 각 프로세스에 대한 처리 순서를 결정하는 것으로 상호 배제의 한 형태
```

###### 5. 스핀락
```
임계 구역에 진입이 불가능할 때, 가능할 때까지 루프를 돌면서 재시도하는 방식으로 구현된 lock
임계구역 진입 전까지 루프를 돌기 때문에 busy waiting 발생
```



세마포어와 뮤텍스는 임계 영역에서 동기화 방법이다.  

---


### 뮤텍스
![image](https://user-images.githubusercontent.com/58067265/126017430-64299e66-d1d8-4320-bf0e-0492e2727ab3.png)

```
임계구역을 가진 스레드들이 running time이 서로 겹치지 않게 단독으로 실행되게 하는 기술
공유 리소스에 대한 접근 조율을 위해 locking과 unlocking을 사용한다. = 뮤텍스 객체를 동시에 이용할 수 X
```

>
---


### 세마포어
![image](https://user-images.githubusercontent.com/58067265/126017387-89fdf747-3143-4900-a8b8-75b231a077ad.png)

```
세마포어란 여러 프로세스/스레드가 공유된 자원의 데이터에 접근하는 것을 Signaling mechanism을 이용하여 통제하는 것
```

##### 종류
1) binary semaphore (뮤텍스와 같음)

2) count semaphore  
  자원을 사용하면 감소, 방출하면 증가함


---
### 공유 자원에 접근하는 방법

![image](https://user-images.githubusercontent.com/58067265/126016678-a01bd725-6b33-4876-9cbd-3b82976e8e96.png)  

위 그림에서 resource가 3개니까, semaphore를 초기화해줄 때 3으로 한다.
1) 세마포어 획득
> 획득할 때, 1 감소한다. 0이된 이후 다른 Task 진입하려면 대기한다.


2) 작업할당
> mutex는 resource를 단독 task가 접근할 수 있도록 제어한다.

**_태스크가 세마포어를 획득해도 뮤텍스를 획득해야 리소스 접근 가능_**  

---

### 둘의 차이점은?

###### ✅ 동기화 대상의 개수
> mutex는 1개, semaphore는 1개 이상

###### ✅ semaphore는 mutex가 될 수 있지만, mutex는 semaphore가 될 수 없다.
> 뮤텍스와 이진 세마포어

###### ✅ mutex는 소유하고 있는 스레드가 mutex를 해제할 수 있다.
> 뮤택스는 소유하고 있는 스레드가, 세마포어는 소유하고 있지 않은 스레드도 해당 세마포어를 해제할 수 있음

###### ✅ 뮤텍스는 프로세스의 범위를 가져 종료될 때 자동으로 clean되고 세마포어는 파일 시스템 상 파일 형태로 존재
---

### 출처
http://blog.skby.net/%EC%84%B8%EB%A7%88%ED%8F%AC%EC%96%B4-semaphore/  

