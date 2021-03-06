# 메모리(Memory)

## 메인 메모리

### 메인 메모리란?

- CPU가 직접 접근할 수 있는 접근 장치
- 주소가 할당된 일련의 바이트들로 구성되어 있음
- 프로그램이 실행되려면 해당 프로그램이 복사되어 메모리에 올라와야 함
- CPU는 연산을 수행한 후 메인 메모리에 데이터를 저장하거나 필요한 데이터를 요구함


<br/>

### 프로그램 실행 과정

![image](https://user-images.githubusercontent.com/24283422/126812729-646bd586-3121-46a9-a737-b273742681a9.png)

- 컴파일&링킹 -> exe 파일(loadable 파일) 내의 모든 주소는 논리 주소
- 실행 시점에 논리 주소 -> 물리 주소 변환 체계 필요
- 주소 결속(Address Binding) : 논리 주소 -> 물리 주소

<br/>

> 논리 주소

CPU에 의해 생성된 주소, 가상 주소

> 물리 주소

메모리에서 식별되는 주소

<br/>

## MMU

### MMU란?

- Memory Management Unit
- 주소 결속(논리 주소 -> 물리 주소 변환) 역할
- 메모리 보호나 캐시 관리 등 CPU가 메모리에 접근하는 것을 관리해주는 하드웨어

<br/>

### MMU의 메모리 보호

- 프로세스는 독립적인 메모리 공간을 가져야 하며, 다른 공간을 침범해서는 안됨
- 따라서 한 프로세스에게 주소 영역을 설정하고, 잘못된 접근이 오면 trap을 발생시켜 보호

![image](https://user-images.githubusercontent.com/24283422/126814308-09dba299-455a-4fa9-954c-5b4d19b33080.png)

- base : 시작 주소 / limit : 크기
- base <= 프로세스 접근 가능 영역 < base+limit

<br/>

## 가상 메모리

### 메모리 경영 기법 분류

![image](https://user-images.githubusercontent.com/24283422/126814806-1ad0673d-dd4a-4c91-9af2-2d9f50a8e364.png)

<br/>

### 가상 메모리 기법

- 메모리 과할당(over allocating)
- 실제 메모리의 사이즈보다 더 큰 사이즈의 메모리를 프로세스에 할당
- 문제 : 모든 메모리가 사용중이라 페이지를 할당할 수 있는 빈 프레임이 없음
- 해결 : 페이지 교체(대치)

<br/>

### 페이지 교체

![image](https://user-images.githubusercontent.com/24283422/126816458-d42430ba-5ff8-4892-977d-4884b0aad86a.png)

- 물리 메모리에 여유가 없을 때 희생될 페이지를 찾아
  대치
- 페이지 교체 시 오버헤드 발생
  - 희생할 프레임을 디스크에 올릴 때
  - 원하는 페이지를 메모리로 가져올 때

<br/>

### 오버헤드 감소 방법

1. 변경 비트

- dirty bit(modify bit)
- set(=변경 O) : 디스크에 기록 필수
- clear(=변경 X) : 디스크에 기록할 필요 X

2. 페이지 교체 알고리즘

- 페이지 폴트를 발생할 확률을 최대한 줄여줄 수 있는 교체 알고리즘을 사용
- FIFO, OPT, LRU 등

<br/>

## 캐시 메모리

### 캐시 메모리

- 주기억장치에 저장된 내용의 일부를 임시로 저장해두는 기억장치
- CPU와 메인 메모리 간의 성능 차이에 대한 성능 저하를 줄이기 위한 대안
- 만약 CPU가 어떠한 데이터에 대하여 다시 재접근을 할때, 그 데이터를 캐시 메모리에 저장해놨다면 메인 메모리까지 접근할 필요가 없음

<br/>

### 캐시 메모리 특징

1. 캐시는 메인 메모리와 CPU사이에 위치, 자주 사용하는 프로그램과 데이터를 기억

2. 캐시 메모리는 메모리 계층 구조에서 가장 빠른 소자이며, 처리속도가 거의 CPU의 속도와 비슷할 정도의 속도를 가지고 있음

3. 캐시메모리를 사용하면 메인 메모리에 접근하는 횟수가 줄어들어 컴퓨터의 처리속도가 향상됨

4. 캐시 주소표는 검색 시간을 단축시키기 위해 주로 연관기억장치를 사용

5. 캐시의 크기는 보통 수십 KByte ~ 수백 KByte

<br/>

### CPU와 기억장치의 상호작용

- CPU에서 주소 전달 -> 캐시 기억 장치에 명령이 존재하는지 확인
- 존재 = Hit
  - 해당 명령어를 CPU로 전송 -> 완료
- 미존재 = Miss
  - 명령어를 갖고 주기억장치로 접근 → 해당 명령어를 가진 데이터 인출 → 해당 명령어 데이터를 캐시에 저장 → 해당 명령어를 CPU로 전송 → 완료

> 캐시를 잘 활용하면 비용 ↓

> CPU가 어떤 데이터를 원할지 어느정도 예측할 수 있어야 함

> 적중률을 극대화시키기 위해 사용되는 것이 바로 지역성의 원리

<br/>

### 지역성

- 기억 장치 내의 정보를 균일하게 액세스 하는 것이 아니라 한 순간에 특정부분을 집중적으로 참조하는 특성
- 시간 지역성 : 최근에 참조된 주소의 내용은 곧 다음에도 참조되는 특성
- 공간 지역성 : 실제 프로그램이 참조된 주소와 인접한 주소의 내용이 다시 참조되는 특성

<br/>

### 캐싱 라인

빈번하게 사용되는 데이터들을 캐시에 저장했더라도, 내가 필요한 데이터를 캐시에서 찾을 때 모든 데이터를 순회하는 것은 시간 낭비

캐시에 목적 데이터가 저장되어있을 때 바로 접근하여 출력할 수 있어야 캐시 활용이 의미있어짐

따라서 캐시에 데이터를 저장할 시, 자료구조를 활용해 묶어서 저장하는데 이를 캐싱 라인이라고 함

캐시에 저장하는 데이터에 데이터의 메모리 주소를 함께 저장하면서 빠르게 원하는 정보를 찾을 수 있음 (set이나 map 등을 활용)

<br/>

## 참고

- https://ybdeveloper.tistory.com/61
- 캐시 메모리 : https://coding-factory.tistory.com/357
- 컴퓨터의 메모리 구조 : https://beforb.tistory.com/5
