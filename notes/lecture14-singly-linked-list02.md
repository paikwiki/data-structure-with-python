# 한방향 연결리스트

> 본 포스팅은 한국외대 컴퓨터공학부 신찬수 교수님의 "[자료구조 - Data Structures with Python](https://www.youtube.com/playlist?list=PLsMufJgu5933ZkBCHS7bQTx0bncjwi4PK)" 중 14강 "[한방향 연결리스트](https://youtube.com/watch?v=aCHwXmpuAkY)" 강의를 정리한 노트입니다.

## 추가 연산들: 탐색(search) + 제너레이터(generator)

### 서치

```py
def search(self, key):
  # key 값의 노드를 리턴, 없으면 None 리턴
  v = self.head
  while v.next != None:
    if v.key == key:
      return v
    v = v.next
  return None # or return v (== None)
```

### 제너레이터

```py
A = [3, 5, -1, 9]
for x in A: # A의 요소를 순서대로 x에 대입해준다.
  print(x)
```

리스트처럼 `for` 루프에서 사용할 수 있게 해주는 것이 제너레이터.

```py
def __iterator__(self):
  v = self
  while v != None:
    yield v
    v = v.next
```

`yeild`가 있는 함수를 가리켜 제너레이터라고 한다. `L`이라는 이름의 연결리스트에 대해 아래처럼 쓸 수 있다.

```py
for x in L:
  print(x)
```

연결리스트의 이터레이터가 종료되면 `StopIterator`라는 에러 메시지가 자동으로 생성된다. 이 에러 메시지가 발생하면 자동으로 이터레이터를 빠져 나온다.
