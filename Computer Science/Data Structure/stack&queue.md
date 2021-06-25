## 스택(Stack)

입력과 출력이 한 곳(방향)으로 제한 즉, 자료를 가르키는 포인터가 하나!

##### LIFO (Last In First Out, 후입선출) : 가장 나중에 들어온 것이 가장 먼저 나옴

![image](https://user-images.githubusercontent.com/54837242/120880937-69ae4a00-c608-11eb-9d77-8325043a1eb3.PNG)

**_언제 사용?_**

함수의 콜스택, 문자열 역순 출력, 연산자 후위표기법

<br>

데이터 넣음 : push()

데이터 최상위 값 뺌 : pop()

비어있는 지 확인 : isEmpty()

꽉차있는 지 확인 : isFull()

+SP

<br>

push와 pop할 때는 해당 위치를 알고 있어야 하므로 기억하고 있는 '스택 포인터(SP)'가 필요함

스택 포인터는 다음 값이 들어갈 위치를 가리키고 있음 (처음 기본값은 -1)

```java
private int sp = -1;
```

<br>

##### push

```java
public void push(Object o) {
    if(isFull(o)) {
        return;
    }

    stack[++sp] = o;
}
```

스택 포인터가 최대 크기와 같으면 return

아니면 스택의 최상위 위치에 값을 넣음

<br>

##### pop

```java
public Object pop() {

    if(isEmpty(sp)) {
        return null;
    }

    Object o = stack[sp--];
    return o;

}
```

스택 포인터가 0이 되면 null로 return;

아니면 스택의 최상위 위치 값을 꺼내옴

<br>

##### isEmpty

```java
private boolean isEmpty(int cnt) {
    return sp == -1 ? true : false;
}
```

입력 값이 최초 값과 같다면 true, 아니면 false

<br>

##### isFull

```java
private boolean isFull(int cnt) {
    return sp + 1 == MAX_SIZE ? true : false;
}
```

스택 포인터 값+1이 MAX_SIZE와 같으면 true, 아니면 false

<br>

<br>

#### **동적 배열 스택**

위처럼 구현하면 스택에는 MAX_SIZE라는 최대 크기가 존재해야 한다

(스택 포인터와 MAX_SIZE를 비교해서 isFull 메소드로 비교해야되기 때문!)

<br>

최대 크기가 없는 스택을 만드려면?

> arraycopy를 활용한 동적배열 사용  
> cf\_ 배열의 복사가 필요할 때는 for문 보다는 System.arraycopy나 Arrays.copyOf를 이용하는게 직관적이므로 권장된다. 전체 길이를 전부 복사하거나 복사 대상의 객체를 유지하지 않아도 된다면 copyOf를 사용하자. 복사하는 길이를 명시해야 하거나 객체를 유지해야 한다면 System.arraycopy를 사용하면 된다.

<br>

```java
public void push(Object o) {

    if(isFull(sp)) {

        Object[] arr = new Object[MAX_SIZE * 2];
        System.arraycopy(stack, 0, arr, 0, MAX_SIZE);
        stack = arr;
        MAX_SIZE *= 2; // 2배로 증가
    }

    stack[sp++] = o;
}
```

기존 스택의 2배 크기만큼 임시 배열(arr)을 만들고

arraycopy를 통해 stack의 인덱스 0부터 MAX_SIZE만큼을 arr 배열의 0번째부터 복사한다

복사 후에 arr의 참조값을 stack에 덮어씌운다

마지막으로 MAX_SIZE의 값을 2배로 증가시켜주면 된다.

<br>

이러면, 스택이 가득찼을 때 자동으로 확장되는 스택을 구현할 수 있음

<br>

#### 스택을 연결리스트로 구현해도 해결 가능

```java
public class Node {

    public int data;
    public Node next;

    public Node() {
    }

    public Node(int data) {
        this.data = data;
        this.next = null;
    }
}
```

```java
public class Stack {
    private Node head;
    private Node top;

    public Stack() {
        head = top = null;
    }

    private Node createNode(int data) {
        return new Node(data);
    }

    private boolean isEmpty() {
        return top == null ? true : false;
    }

    public void push(int data) {
        if (isEmpty()) { // 스택이 비어있다면
            head = createNode(data);
            top = head;
        }
        else { //스택이 비어있지 않다면 마지막 위치를 찾아 새 노드를 연결시킨다.
            Node pointer = head;

            while (pointer.next != null)
                pointer = pointer.next;

            pointer.next = createNode(data);
            top = pointer.next;
        }
    }

    public int pop() {
        int popData;
        if (!isEmpty()) { // 스택이 비어있지 않다면!! => 데이터가 있다면!!
            popData = top.data; // pop될 데이터를 미리 받아놓는다.
            Node pointer = head; // 현재 위치를 확인할 임시 노드 포인터

            if (head == top) // 데이터가 하나라면
                head = top = null;
            else { // 데이터가 2개 이상이라면
                while (pointer.next != top) // top을 가리키는 노드를 찾는다.
                    pointer = pointer.next;

                pointer.next = null; // 마지막 노드의 연결을 끊는다.
                top = pointer; // top을 이동시킨다.
            }
            return popData;
        }
        return -1; // -1은 데이터가 없다는 의미로 지정해둠.

    }

}
```

<br>

<br>

<br>

## 큐(Queue)

입력과 출력을 한 쪽 끝(front, rear)으로 제한 (포인터 갯수가 2)

##### FIFO (First In First Out, 선입선출) : 가장 먼저 들어온 것이 가장 먼저 나옴

<br>

**_언제 사용?_**

버퍼, 마구 입력된 것을 처리하지 못하고 있는 상황, BFS  
※시스템 처리의 순서가 중요할때 front로 사용되는 자료구조(교통정리,스케줄러)

<br>

큐의 가장 첫 원소를 front, 끝 원소를 rear라고 부름

큐는 **들어올 때 rear로 들어오지만, 나올 때는 front부터 빠지는 특성**을 가짐

접근방법은 가장 첫 원소와 끝 원소로만 가능

<br>

데이터 넣음 : enQueue()

데이터 뺌 : deQueue()

비어있는 지 확인 : isEmpty()

꽉차있는 지 확인 : isFull()

<br>

데이터를 넣고 뺄 때 해당 값의 위치를 기억해야 함. (스택에서 스택 포인터와 같은 역할)

이 위치를 기억하고 있는 게 front와 rear

front : deQueue 할 위치 기억

rear : enQueue 할 위치 기억

<br>

##### 기본값

```java
private int size = 0;
private int rear = -1;
private int front = -1;

Queue(int size) {
    this.size = size;
    this.queue = new Object[size];
}
```

<br>

<br>

##### enQueue

```java
public void enQueue(Object o) {

    if(isFull()) {
        return;
    }

    queue[++rear] = o;
}
```

enQueue 시, 가득 찼다면 꽉 차 있는 상태에서 enQueue를 했기 때문에 overflow

아니면 rear에 값 넣고 1 증가

<br>

<br>

##### deQueue

```java
public Object deQueue(Object o) {

    if(isEmpty()) {
        return null;
    }

    Object o = queue[front];
    queue[front++] = null;
    return o;
}
```

deQueue를 할 때 공백이면 underflow

front에 위치한 값을 object에 꺼낸 후, 꺼낸 위치는 null로 채워줌

<br>

##### isEmpty

```java
public boolean isEmpty() {
    return front == rear;
}
```

front와 rear가 같아지면 비어진 것

<br>

##### isFull

```java
public boolean isFull() {
    return (rear == queueSize-1);
}
```

rear가 사이즈-1과 같아지면 가득찬 것

<br>

---

일반 큐의 단점 : 큐에 빈 메모리가 남아 있어도, 꽉 차있는것으로 판단할 수도 있음

(rear가 끝에 도달했을 때)

<br>

이를 개선한 것이 **'원형 큐'**

논리적으로 배열의 처음과 끝이 연결되어 있는 것으로 간주함!
![image](https://user-images.githubusercontent.com/54837242/120881507-906e7f80-c60c-11eb-8bce-596337fa1fbf.PNG)

원형 큐는 초기 공백 상태일 때 front와 rear가 0

공백, 포화 상태를 쉽게 구분하기 위해 **자리 하나를 항상 비워둠**

```
(index + 1) % size로 순환시킨다
```

<br>

##### 기본값

```java
private int size = 0;
private int rear = 0;
private int front = 0;

Queue(int size) {
    this.size = size;
    this.queue = new Object[size];
}
```

<br>

##### enQueue

```java
public void enQueue(Object o) {

    if(isFull()) {
        return;
    }

    rear = (++rear) % size;
    queue[rear] = o;
}
```

enQueue 시, 가득 찼다면 꽉 차 있는 상태에서 enQueue를 했기 때문에 overflow

<br>

<br>

##### deQueue

```java
public Object deQueue(Object o) {

    if(isEmpty()) {
        return null;
    }

    front = (++front) % size;
    Object o = queue[front];
    return o;
}
```

deQueue를 할 때 공백이면 underflow

<br>

##### isEmpty

```java
public boolean isEmpty() {
    return front == rear;
}
```

front와 rear가 같아지면 비어진 것

<br>

##### isFull

```java
public boolean isFull() {
    return ((rear+1) % size == front);
}
```

rear+1%size가 front와 같으면 가득찬 것

<br>

원형 큐의 단점 : 메모리 공간은 잘 활용하지만, 배열로 구현되어 있기 때문에 큐의 크기가 제한  
일반 배열로 구현했을때 생성->복사 과정이 복잡해 속도와 안전성이 떨어짐.
<br>

<br>

이를 개선한 것이 '연결리스트 큐'

##### 연결리스트 큐는 크기가 제한이 없고 삽입, 삭제가 편리

<br>

##### enqueue 구현

```java
public void enqueue(E item) {
    Node oldlast = tail; // 기존의 tail 임시 저장
    tail = new Node; // 새로운 tail 생성
    tail.item = item;
    tail.next = null;
    if(isEmpty()) head = tail; // 큐가 비어있으면 head와 tail 모두 같은 노드 가리킴
    else oldlast.next = tail; // 비어있지 않으면 기존 tail의 next = 새로운 tail로 설정
}
```

> - 데이터 추가는 끝 부분인 tail에 한다.
>
> - 기존의 tail는 보관하고, 새로운 tail 생성
>
> - 큐가 비었으면 head = tail를 통해 둘이 같은 노드를 가리키도록 한다.
> - 큐가 비어있지 않으면, 기존 tail의 next에 새로만든 tail를 설정해준다.

<br>

##### dequeue 구현

```java
public T dequeue() {
    // 비어있으면
    if(isEmpty()) {
        tail = head;
        return null;
    }
    // 비어있지 않으면
    else {
        T item = head.item; // 빼낼 현재 front 값 저장
        head = head.next; // front를 다음 노드로 설정
        return item;
    }
}
```

> - 데이터는 head로부터 꺼낸다. (가장 먼저 들어온 것부터 빼야하므로)
> - head의 데이터를 미리 저장해둔다.
> - 기존의 head를 그 다음 노드의 head로 설정한다.
> - 저장해둔 데이터를 return 해서 값을 빼온다.

<br>

이처럼 삽입은 tail, 제거는 head로 하면서 삽입/삭제를 스택처럼 O(1)에 가능하도록 구현이 가능하다.

## 덱(Deque-[double-ended queue])

두 개의 포인터를 사용하여, 양쪽에서 삭제와 삽입을 발생 시킬 수 있다. 큐와 스택을 합친 형태로 생각할 수 있다.

데이터 넣음 : append(o): 오른쪽, appendleft(o): 왼쪽

데이터 뺌 : pop(o): 오른쪽, popleft(o): 왼쪽

비어있는 지 확인 : isEmpty()

꽉차있는 지 확인 : isFull()

<br>

**_언제 사용?_**

데이터 검색을 거의 하지 않을 경우(랜덤액세스)
스케줄링, 스케줄링에 우선순위를 줄때 큐와 스택보다 덱이 더 효율이 잘나오는 경우가 있다.  
컨테이너(container)의 양끝 엘리먼트(element)에 접근하여 삽입 또는 제거를 할 경우, 일반적인 리스트(list)가 이러한 연산에 O(n)이 소요되는 데 반해, 데크(deque)는 O(1)로 접근 가능하다.(단, list로 구현한 덱은 제외)

<br>

java에서 구현

```java
class Node<E>{

private E data;
private Node<E> next;
private Node<E> prev;

Node(E data) {
this.data = data;
this.next = null;
this.prev = null;
}

void setNext(Node<E> next) {
this.next = next;
}

void setPrev(Node<E> prev) {
this.prev = prev;
}

void setData(E data) {
this.data = data;
}

Node<E> getNext() {
return next;
}

Node<E> getPrev() {
return prev;
}

E getData() {
return data;
}
};
```

```java
public class Deque<E>{

private Node<E> front;
private Node<E> rear;

Deque() {
front = rear = null;
}

-- setter,getter--

boolean empty() {
if (front == null) return true;
else return false;
}

boolean push_front(E data) {
 if (empty()) {
    front = new Node<E>(data);
    rear = front;
    return true;
}
front.setPrev(new Node<E>(data));
front.getPrev().setNext(front);
front = front.getPrev();
return true;
}

boolean push_rear(E data) {
if (empty()) {
    rear = new Node<E>(data);
    front = rear;
    return true;
}
rear.setNext(new Node<E>(data));
rear.getNext().setPrev(rear);
rear = rear.getNext();
return true;
}

E pop_front() {
E tmp = front.getData();
if (empty()) return null;
if (front == rear) {
    front = null;
    rear = null;
    return tmp;
}
front = front.getNext();
front.setPrev(null);
return tmp;
}

E pop_rear() {
E tmp = rear.getData();
if (empty()) return null;
if (front == rear) {
    front = null;
    rear = null;
    return tmp;
}
rear = rear.getPrev();
rear.setNext(null);
return tmp;
}

E begin() {
return front.getData();
}

E end() {
return rear.getData();
}

}
```

### 나중에 지울꺼

기본적으로 stack과 queue는 선형 구조이다.
![image](https://user-images.githubusercontent.com/54837242/120881340-4e910980-c60b-11eb-94b6-e97842d5ba58.PNG)

**Native Code와 Managed Code란?**

Native Code는 컴퓨터 기계어로 동작하는  
즉, OS에 의해 직접적으로 컴파일 되는 코드를 의미한다.  
작성한 코드 그대로 컴퓨터에서 구동이 된다. 컴퓨터와 매우 밀접한 관계가 있다.

반대로 Managed Code는 구동 시키기 위해선 인터프리터라고 불리우는 다른 프로그램이 반드시 요구 되는 코드를 의미한다.  
자바 버츄어 머신이나 .Net Framework와 같은 인터프리터가 필요한 코드를 의미한다.
구동하기 위해선 반드시 인터프리터를 깔아야한다.
