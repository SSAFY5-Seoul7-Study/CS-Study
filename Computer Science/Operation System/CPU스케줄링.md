CPU 스케줄링
========================
### 1. 스케줄링 정의
> 한정된 CPU의 작업 처리시간을 여러 프로세스 혹은 여러 쓰레드가 효율적으로 이용할 있도록 분배하는 정책이자 알고리즘 -> 효율적으로 CPU 사용하기 위해 작업할 프로세스 고르는 것 !

### 스케줄링의 성능 기준 
- CPU utilization (CPU 활용률) - CPU 작동한 총 시간 대비 실제 사용 시간
- Throughput (처리량) - 단위 시간 당 완료된 프로세스의 개수
- Turnaround time (반환 시간) - 작업 시작부터 완료까지 소요 시간
- Waiting time (대기 시간) - 프로세스가 준비 큐에서 스케줄링 될 때까지 기다리는 시간
- Response time (응답 시간) - 서비스 요청 후 첫 반응이 나오기까지 걸린 시간

-> 사용자 관점 (반환시간, 대기 시간, 응답 시간) , 시스템 관점 (CPU 활용률, 처리량)

```
시스템 마다 추구하는 성능 다름
- Batch System : 가능하면 많은 일 수행에 초점 (throughout, CPU utilization 최대화)
- Interactive System : 빠른 response time, 적은 waiting time  ex) 우리가 사용하는 PC
- Real time System : 시간 제약 조건에 맞춰 스케줄링이 중요
```

#

### CPU 스케줄링 알고리즘 종류

![image](img\선점비선점스케줄링.PNG)

### 비선점 방식

#### FCFS (First Come First Service)
> 선입선출(FIFO) , 도착 순대로 CPU 할당
> 장점 : 일괄 처리 시스템 등에 적합 , 단점 : 호위 효과(convoy effect) 발생 가능성 ↑

![image](https://media.vlpt.us/images/yerin4847/post/b0487918-7782-43be-bbfa-ce360c81af88/image.png)

#

#### SJF (Shortest Job First)
> CPU 작업 시간이 가장 짧은 순으로 스케줄링 , 작업 시간 동일 -> FCFS
> 장점 : 평균 대기 시간 최소화 , 단점 : 무기한 연기 현상 발생 -> 밀리지 않게 Aging 기법 , 프로세스 생성 시 총 실행 시간에 대한 정확한 계산 불가능

![image](https://media.vlpt.us/images/yerin4847/post/b0487918-7782-43be-bbfa-ce360c81af88/image.png)



