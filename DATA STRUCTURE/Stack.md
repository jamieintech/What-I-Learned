# Stack

- 데이터를 제한적으로 접근할 수 있는 구조
  - **한쪽 끝에서만 ** 자료를 접근할 수 있음
  - **가장 나중에** 쌓은 데이터를 **가장 먼저** 빼낼 수 있음



## 1. 스택 구조

- 스택은 LIFO (Last In, First Out) 또는 FILO(First In, Last Out) 데이터 관리 방식을 따름
  - LIFO: 마지막에 넣은 데이터를 가장 먼저 추출하는 데이터 관리 방식
  - FILO: 처음에 넣은 데이터를 가장 마지막에 추출하는 데이터 관리 방식
- 대표적인 스택의 활용
  - 컴퓨터 내부의 프로세스 구조의 함수 동작 방식
- 주요 기능
  - **push()**: 데이터를 스택에 넣음
  - **pop()**: 데이터를 스택에서 꺼냄

> Visualgo에서 시각적으로 보면서 이해해봅시다: https://visualgo.net/en/list



## 2. 스택 구조와 프로세스 스택

- 스택 구조는 프로세스 실행 구조의 가장 기본

  - 함수 호출시 프로세스 실행 구조를 스택과 비교해서 이해 필요

    ```python
    def recursive(data):
        if data < 0:
            print("end")
        else:
            print(data)
            recursive(data - 1)
            print('return', data)
    
    recursive(4)
    ```



## 3. 스택의 장단점

**장점**

- 구조가 단순해서 구현이 쉬움
- 데이터 저장/읽기 속도가 빠름

**단점**

- 데이터의 최대 갯수를 미리 정해야함 
  - 파이썬의 경우 재귀함수는 1000번까지만 호출이 가능
- 저장공간의 낭비가 발생할 수 있음
  - 미리 최대 갯수만큼 저장 공간을 확보해야하는데, 모든 공간을 안쓰면 낭비



## 4. 파이썬 리스트로 스택 만들어보기

```python
stack = list()
stack.append(1)
stack.append(2)

#####################
print(stack)		# [1, 2]
print(stack.pop())	# 2
```

- 파이썬의 리스트에는 기본적으로 `append(=push)`, `pop` 메서드가 이미 존재한다!


   

## 5. 스택 함수 만들어보기

```python
def push(data):
    stack_list.append(data)

def pop():
    data = stack_list[-1]
    del stack_list[-1]
    return data

stack_list = list()
push(1)
push(2)
print(stack_list)	# [1, 2]
print(pop())		# 2
```

