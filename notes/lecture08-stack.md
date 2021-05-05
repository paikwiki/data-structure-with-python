# 스택(stack)

> 본 포스팅은 한국외대 컴퓨터공학부 신찬수 교수님의 "[자료구조 - Data Structures with Python](https://www.youtube.com/playlist?list=PLsMufJgu5933ZkBCHS7bQTx0bncjwi4PK)" 중 8강 "[스택(stack)](https://youtube.com/watch?v=OzFXiukhv8o)" 강의를 정리한 노트입니다.

자료구조는 삽입, 삭제, 탐색, 이 세 가지 연산은 어느 자료구조든지 제공을 해야한다.

## 스택의 연산

- 삽입: `push`
- 삭제: `pop`

스택은 아래에서부터 저장이 되고, 최근에 들어온 값부터 제거가 되는 형식이다(LIFO)

스택은 `push`와 `pop` 연산으로만 값을 변경할 수 있다. 따라서 파이썬 리스트를 간접적으로 사용하면서, 두 연산으로만 값을 변경하도록 한다.

### 편의상 제공하는 연산

- `top`: 가장 위에 있는 값을 반환. `pop`과 달리 삭제를 수행하지 않는다.
- `len`: 요소의 개수를 반환하는 함수

## 스택 클래스 구현

```py
class Stack:
  def __init__(self):
    self.items = [] # 데이터 저장을 위한 리스트 준비

  def push(self, val):
    self.items.append(val)

  def pop(self):
    try:                      # pop할 아이템이 없으면
      return self.items.pop()
    except IndexError:        # indexError 발생
      print("Stack is empty")

  def top(self):
    try:
      return self.items[-1]
    except IndexError:
      print("Stack is empty")

  def __len__(self): # len() 호출하면 stack의 item 수 반환
    return len(self.items)
```

사용 예시

```py
S = Stack()
S.push(10)
S.push(2)
print(S.pop()) # 2
print(S.top()) # 10
print(len(S))  # 1 -> 이렇게 호출하면 파이썬은 S.__len__()을 호출함
```

### 연산의 수행시간

- `push`: O(1)(상수 시간)
- `pop`: O(1)
- `top`: O(1)
- `len`: O(1) (리스트에서 개수를 항상 알고 있으므로 값만 리턴한다)

## 스택의 사용예 1) 괄호 맞추기

> 보기1: (2 + 5) * 7 - ((3 - 1) / 2 + 7) # 쌍이 맞음
>
> 보기2: (()()) # 쌍이 맞음
>
> 보기3: (()))( # 쌍이 맞지 않음

- 문제:
  - 입력: 왼쪽과 오른쪽 괄호의 문자열
  - 출력: 쌍이 맞으면 True, 아니면 False 반환

보기2를 보면,

> ( ( )  ( ) )
> 1 2 2  3 3 1

좌측 괄호를 만나면 `push`, 우측 괄호를 만나면 `pop`을 수행한다. 끝까지 수행한 후 스택에 아무것도 남지 않았다면 짝이 맞는 것. True.

> ( ) )
> 1 1 2

위 경우, 마지막에 `pop`을 수행하려 할 때 에러가 발생. 왼쪽괄호가 하나 모자른 것이다. False.

> ( ) (
> 1 1 2

끝까지 수행한 후 무언가 남아있다면 오른쪽 괄호 하나가 모자른 경우. False.

```py
for p in parSeq:
  if p == '(': S.push(p)
  elif p == ')': S.pop() # 에러 발생시 오른쪽 괄호가 더 많은 것으로 보고 return False
  else: print("Not allowed Symbol")
if len(S) > 0: return False
else: return True
```
