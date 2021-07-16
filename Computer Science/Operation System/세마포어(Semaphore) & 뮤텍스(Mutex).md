## 세마포어(Semaphore) & 뮤텍스(Mutex)

### 간단한 정리
###### 1. Critical Section (임계 영역)
```
보호되어야할 영역, 공유 자원에 접근할 때 문제가 발생하지 않도록
한 번에 하나의 프로세스만 이용하도록 보장해줘야 하는 영역
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

###### 동기화
```
두 개 이상의 프로세스를 한 시점에서는 동시에 처리할 수 없으므로 각 프로세스에 대한 처리 순서를 결정하는 것으로 상호 배제의 한 형태
```

### 세마포어

### 뮤텍스

### 둘의 차이점은?
