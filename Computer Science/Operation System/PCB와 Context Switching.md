## PCB와 Context Switching

🕹 다시 한번 짚고 넘아가자!
```
하나의 cpu는(1 코어) 하나의 task만 수행할 수 있다.
```

#### Context Swithching 이란 무엇일까?
![image](img\선점비선점스케줄링.PNG)
멀티프로세스/멀티스레드 환경일때, cpu가 task(프로세스/스레드)를 실행하고 있는 상태에서 인터럽트 요청에 의해 다음 우선순위의 Task가 실행되어야 한다.
이때 기존의 Task상태 또는 레지스터 값을 교체하는 작업을 말한다.
```

#### PCB란 무엇일까?

컨텍스트를 스위칭하기 위해서는 각 프로세스/스레드의 상태를 알아야 한다.
그리고 스위칭하기 위해서는 어떤 프로세스/스레드를 어디까지 진행했는지 여부도 알아야 한다.

```
프로세스를 제어하기 위한 정보의 모음을 말한다. 프로세스가 생성될 때 pcb가 만들어져 각 프로세스는 고유의 PCB를 갖는다. (스레드는 TCB)
```

#### PCB가 어떤 정보를 저장하고 있을까?

![image](https://user-images.githubusercontent.com/58067265/123518871-e2be3000-d6e2-11eb-98af-64c6c07c10dc.png)

* 프로세스 고유 번호
* 프로세스 상태
  * create 
  * ready
  * waiting
  * running
  * terminated
* 포인터 = 다음 실행될 프로세스의 포인터
* program counter = 다음에 실행할 명령어의 주소
* 레지스터
* cpu 스케쥴링 정보 = 우선순위, 최종 실행 시각, cpu 점유 시간
* 메모리 관리 정보 = 해당 프로세스의 주소 공간
* 프로세스 계정 정보
* 입출력 상태 정보 = 프로세스에 할당된 입출력장치 목록, 열린 파일 목록

#### 언제 Context Switching이 일어날까?
![image](https://user-images.githubusercontent.com/58067265/123519245-008c9480-d6e5-11eb-957f-ab820aee7c12.png)

1) 인터럽트 발생 시 (Interrupt)
2) 실행중인 cpu 사용 할당을 모두 소모했을 때 (schedular dispatch)
3) 입출력을 위해 대기할 때 (I/O or Event wait)

#### 어떻게 진행이 될까?
![image](https://user-images.githubusercontent.com/58067265/123520003-7bf04500-d6e9-11eb-9925-b03dfb8ee384.png)


#### 



#### 추가로 알면 도움이 될 키워드
* 레지스터

## 출처
https://thebook.io/006950/ch10/01/03-01/  
https://www.crocus.co.kr/1364  








