# Queue

> Queue는 배열과 함께 가장 쉬운 자료구조 중 하나이다. 
>
> Queue : 줄, 대기 행렬 (식당 웨이팅라인 같은 거)

## 1. Queue의 구조

- 가장 먼저 넣은 데이터를 가장 먼저 꺼낼 수 있는 구조(First-In, First Out)

  - 음식점에서 가장 먼저 줄을 선 사람이 제일 먼저 음식점에서 입장하는 것과 동일
  - FIFO 또는 LILO(Last-In, Last Out) 방식으로 스택과 꺼내는 순서가 반대

  

## 2. Queue의 용어

- Enqueue: 큐에 데이터를 넣는 기능
- Dequeue: 큐에서 데이터를 꺼내는 기능



## 3. 파이썬의 queue 라이브러리 활용하기

- queue 라이브러리는 다양한 큐 구조의 `Queue()`, `LifoQueue()`, `PriorityQueue()` 등을 제공

- 프로그램을 작성할 때 프로그램에 따라 적합한 자료 구조를 사용

  - Queue(): 가장 일반적인 큐 자료구조

  - LifoQueue(): 나중에 입력된 데이터가 먼저 출력되는 구조(=스택)

  - PriorityQueue(): 데이터마다 우선순위를 줘서 우선순위가 높은 순으로 데이터 출력

    > 이 외에도 다양한 queue들이 존재한다

### Queue()

```python
# Queue()로 큐 만들기 - FIFO
import queue

# 큐 생성
data_queue = queue.Queue()

# 큐에 데이터 삽입 = put()
data_queue.put("hello")
data_queue.put("world")

# 초기 큐의 길이 = 2
print(data_queue.qsize())

# 하나씩 꺼낼 때 마다 큐의 길이가 줄어든다
print(data_queue.get(), data_queue.qsize())     #hello 1
print(data_queue.get(), data_queue.qsize())     #world 0
```

### LifoQueue()

```python
import queue

# LifoQueue 생성 - Last In First Out
data_queue = queue.LifoQueue()

# 데이터 삽입
data_queue.put("Hello")
data_queue.put("World")

# 데이터 꺼내기 - 뒤에서부터 나옴
print(data_queue.get())     #World
print(data_queue.get())     #Hello
```

### PriorityQueue()

```python
import queue

# 우선순위 큐 생성
data_queue = queue.PriorityQueue()

# 데이터 삽입 (우선순위, 데이터)
# 튜플 형태로 삽입한다
data_queue.put((5, "Hello"))
data_queue.put((11, "World"))

# 우선순위가 더 높은(숫자가 더 작은) 데이터가 먼저 나온다 
print(data_queue.get())     #(5, 'Hello')
print(data_queue.get())     #(11, 'World')
```



## 참고: Queue는 어디에 쓰일까?

멀티 태스킹을 위한 프로세스 스케쥴링 방식을 구현하기 위해 많이 사용됨 (운영체제 참조)

> 큐의 경우 특별히 언급되는 장단점은 없음. 하지만 큐의 활용 예로 프로세스 스케쥴링 방식을 함께 이해해두는 것이 좋음



## 4. Queue 구현하기

```python
queue_list = list()

# 데이터 삽입
def enqueue(data):
    queue_list.append(data)

# 데이터 꺼내기
def dequeue():
    data = queue_list[0]    #FIFO기 때문에 맨 앞의 데이터를 추출
    del queue_list[0]       #기존 데이터 삭제
    return data
```

```python
# 데이터 삽입
for i in range(10):
    enqueue(i)
    
print(queue_list)	# [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]

# 첫번째 데이터 꺼내기
dequeue()
print(queue_list)   # [1, 2, 3, 4, 5, 6, 7, 8, 9]
```

