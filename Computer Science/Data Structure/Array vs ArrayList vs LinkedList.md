## Array vs ArrayList vs LinkedList  
---

### 1. Array  
> 같은 타입의 변수들로 이루어진 유한 집합  
> 값과 그의 위치를 가리키는 인덱스로 구성  

![image](https://user-images.githubusercontent.com/58067265/120814908-4d6bc800-c58a-11eb-8df2-9c5411252e62.png)

논리적 저장 순서와 물리적 저장 순서가 일치 = 인덱스로 값에 접근이 가능 = **_Random Access_** 가능

+ Random Access(비순차 접근)란?  
![image](https://user-images.githubusercontent.com/58067265/120815935-41ccd100-c58b-11eb-9a19-68ead7a39b20.png)
```
저장된 순서대로 데이터를 검색해야 하는 Sequential access 와 달리,어떤 항목에도 일정한 시간에 접근할 수 있는 능력
```

| 장점 | 단점 |
| --- | --- |
|- 랜덤 액세스로 인해 검색에 좋음 O(1)의 시간 복잡도 |- 최초 생성시 크기 지정으로 바꿀 수 없음 |
||- 비순차적으로 데이터 삽입/삭제시 오버헤드 발생|
||- 중간에 메모리가 비어있는 경우 메모리 낭비|


배열의 정적 크기 문제를 해결하기 위해 나온 것이 ArrayList 이다.  

### 2. ArrayList
> List 인터페이스를 상속받은 클래스
> 크기가 가변적으로 변함

![image](https://user-images.githubusercontent.com/58067265/120819863-f3b9cc80-c58e-11eb-87b6-9cb9a7f7a1ab.png)

최초 생성시(크기 지정하지 않고), 10의 크기로 생성됨




### 출처
http://tcpschool.com/c/c_array_oneDimensional
