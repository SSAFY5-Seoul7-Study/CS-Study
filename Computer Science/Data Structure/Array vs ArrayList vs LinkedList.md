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
|- 순차 접근의 경우 빠른 성능을 보여줌|- 비순차적으로 데이터 삽입/삭제시 오버헤드 발생|
||- 중간에 메모리가 비어있는 경우 메모리 낭비|


배열의 정적 크기 문제를 해결하기 위해 나온 것이 ArrayList 이다.  

### 2. ArrayList
> List 인터페이스를 상속받은 클래스  
> **Resizable-array**

+ 어떻게 크기가 변할 수 있을까?  
1. (크기를 선언하지 않은 경우) 10만큼의 배열 크기로 생성
2. 원소를 추가할 때, 크기를 벗어나는 경우 1.5배 크기의 새 배열 생성 후 값 복사와 대입

![image](https://user-images.githubusercontent.com/58067265/120819863-f3b9cc80-c58e-11eb-87b6-9cb9a7f7a1ab.png)
![image](https://user-images.githubusercontent.com/58067265/120824234-341b4980-c593-11eb-8c56-a56bbe65c286.png)
![image](https://user-images.githubusercontent.com/58067265/120824072-0afab900-c593-11eb-88a5-bf912c0f521a.png)
![image](https://user-images.githubusercontent.com/58067265/120825456-5f526880-c594-11eb-944f-38e42ed74f34.png)


=> 배열로 구현이 되어 있다 = 배열의 장점을 그대로 가져간다.

| 장점 | 단점 |
| --- | --- |
|- 크기 변동 가능|- 비순차적으로 데이터 삽입/삭제시 오버헤드 발생|
|- 랜덤 액세스로 인해 검색에 좋음 O(1)의 시간 복잡도|- 원소의 수가 많은 경우 복사 양이 많아져 시간이 오래 걸림|
|- 순차 접근의 경우 빠른 성능을 보여줌||

여전히 비순차적인 원소의 추가/삭제시 시간이 오래걸린다는 단점이 있다.  
이 문제를 해결하기 위해 나온 것이 LinkedList이다.

### 3. LinkedList
> 각 노드가 데이터와 포인터를 가지고 연결되어 있는 자료구조, 불연속적임  
> 실제 Java에서는 더블 링크드 리스트로 구현이 되어 있음

![image](https://user-images.githubusercontent.com/58067265/120826300-3d0d1a80-c595-11eb-85d1-d8d0484beb49.png)

![image](https://user-images.githubusercontent.com/58067265/120830382-65971380-c599-11eb-8552-aaeac7151ea9.png)

| 장점 | 단점 |
| --- | --- |
|- 크기 변동 가능|- 랜덤액세스 불가 -> 순차 접근만 가능 |
|- 불필요한 작업이 줄어 ArrayList보다 추가/삭제 작업 빠름|- 순차접근시 ArrayList보다 느림 (참조의 지역성 - Cache Locality) |
||- 참조를 위한 메모리 추가 할당 필요|

### 4. ArrayList vs LinkedList (성능 비교)  
![image](https://user-images.githubusercontent.com/58067265/120833389-b3614b00-c59c-11eb-87c2-45b6430e1eec.png)

![image](https://user-images.githubusercontent.com/58067265/120837052-3a182700-c5a1-11eb-8b85-4c8ff2eb9150.png)

* 순차적 추가/삭제시 = ArrayList > LinkedList
* 비순차적 추가/삭제시 = ArrayList < LinkedList


### 5. 어떤걸 사용하는게 가장 좋을까?  
* 삽입/삭제가 빈번하게 발생하는 프로세스 = LinkedList  
* 인덱스를 이용해 자료를 검색하는 프로세스 => Array(지정된 크기) 혹은 ArrayList(크기 변동)


### 추가적으로 공부하면 좋을 Key Word
* Cache Locality > https://stackoverflow.com/questions/12065774/why-does-cache-locality-matter-for-array-performance
* Quick Sort 와 Merget Sort 는 배열 vs 리스트 중 어디서 쓰면 더 좋을까?
* Random Access 와 Sequential Access 란?

### 참고 자료
![image](https://user-images.githubusercontent.com/58067265/120837431-a7c45300-c5a1-11eb-936a-bd493bd513d0.png)


### 출처
http://tcpschool.com/c/c_array_oneDimensional
https://www.nextree.co.kr/p6506/  
https://devlog-wjdrbs96.tistory.com/64  
https://slidesplayer.org/slide/14462338/  

