CPU 스케줄링
========================
### 스케줄링 정의
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

### CPU 스케줄링 발생 하는 상황
+ 실행상태에서 대기상태로 전환될 때 (ex. 입출력 요청)
+ 실행상태에서 준비상태로 전환될 때 (ex. 인터럽트 발생)
+ 대기 상태에서 준비상태로 전환될 때 (ex. 입출력 종료시)
+ 종료될 때


### CPU 스케줄링 알고리즘 종류

![image](https://github.com/SSAFY5-Seoul7-Study/CS-Study/blob/7e4cd5d22addf0ac19edde2a23760b7272342e0e/Computer%20Science/Operation%20System/img/%EC%84%A0%EC%A0%90%EB%B9%84%EC%84%A0%EC%A0%90%EC%8A%A4%EC%BC%80%EC%A4%84%EB%A7%81.PNG)

#

### 비선점 방식
> 프로세스가 CPU 할당 받아 실행 중이면 강제로 CPU 뺏을 수 없는 스케줄링

#### FCFS (First Come First Service)

```
선입선출(FIFO) , 도착 순대로 CPU 할당
장점 : 일괄 처리 시스템 등에 적합
단점 : 호위 효과(convoy effect) 발생 가능성 ↑
```

![image](https://media.vlpt.us/images/yerin4847/post/b0487918-7782-43be-bbfa-ce360c81af88/image.png)

#

#### SJF (Shortest Job First)
```
CPU 작업 시간이 가장 짧은 순으로 스케줄링 , 작업 시간 동일 -> FCFS
장점 : 평균 대기 시간 최소화
단점 : 무기한 연기 현상 발생 -> 밀리지 않게 Aging 기법 , 프로세스 생성 시 총 실행 시간에 대한 정확한 계산 불가능
```

#

#### HRN (Highest Response-ratio Next)
```
우선 순위 계산하여 점유 불평등 보완 (SJF 단점 보완)
장점 : 긴작업과 짧은 작업 간 불평등 완화
      -> 시분할 시스템에 활용 시 유용
단점 : 준비상태 큐에 있는 각 프로세스의 서비스 시간을 지속적으로 추적 -> Overhead 증가
```
![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdfQsf5%2Fbtqy4dyUeQD%2FYynjjS4HEAQ5kGCeUysC60%2Fimg.png)

#


### 선점 방식
> 프로세스가 시행 중이라도 강제 중지하고 CPU 뺏을 수 있는 스케줄링

#### Round Robin
```
들어온 순으로 같은 크기의 시간할당 -> 할당된 시간 끝나면 작업 중지, 다른 프로세스 실행
장점 : 공평함
단점 : 타임 슬라이스의 크기에 효율이 좌우됨.
```
![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcxFC5P%2Fbtqy5d6hG8v%2F3f2K8kUWKpSqerSg70x290%2Fimg.png)

#

#### SRT (Shortest Remaining Time)
```
SJF에 선점 방식 도입, 처리가 완료 되는데 가장 짧은 시간이 소요된다 판단되는 프로세스를 먼저 수행
-> 진행 중인 프로세스 있어도 최단 잔여시간 프로세스를 위해 짧은 프로세스를 할당
```
![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdLGZ4s%2Fbtqy4dFPWQM%2FJFTdMtaGKf9X40NzA2GbLk%2Fimg.png)

#

#### MLQ(Multi Level Queue) : 다단계 큐 스케줄링
```
준비 상태 큐를 여러 개 두어 스케줄링
각 큐의 독자적인 스케줄링 알고리즘으로 CPU 할당
다른 큐로 작업 이동 불가, 우선순위에 따른 선점
단점 : 우선순위 낮은 큐는 실행 못함 -> MLFQ
```
![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FlDJG3%2Fbtqy2nCixut%2Fe4oZCNSJZ9VwGcHh4aSJ4k%2Fimg.png)

#

#### MLFQ(Multi Level Feedback Queue) : 다단계 피드백 큐 스케줄링
```
MLQ + CPU Time Slice(Quantum)
동적인 프로세스 우선 순위 변화 적용 !

** RR방식과 함께 가장 많이 사용 !
```
+ 우선순위 낮을수록 시간 할당량(Time Quantum) ↑
+ 큐 사이 프로세스 이동 가능
+ 맨 아래 큐에서 오래 대기하면 상위 큐로 이동
![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FkHw6P%2FbtqD3HC3lf7%2FWK2HAPXKyZxNpwoEkE3RkK%2Fimg.png)

#

