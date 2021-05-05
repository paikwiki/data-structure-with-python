# 양방향 연결리스트(Doubly Linked List)

> 본 포스팅은 한국외대 컴퓨터공학부 신찬수 교수님의 "[자료구조 - Data Structures with Python](https://www.youtube.com/playlist?list=PLsMufJgu5933ZkBCHS7bQTx0bncjwi4PK)" 중 15강 "[양방향 연결리스트(Doubly Linked List)](https://youtube.com/watch?v=nQhzNRmnmt8)" 강의를 정리한 노트입니다.

## 한방향 연결리스트의 단점

- 한쪽으로만 연결이 되어 있기 때문에 테일 노드에 대한 조작을 하고 싶을 때 직전의 노드(previous node)를 알고 있어야 한다. 그래서 O(n)의 연산 시간을 사용한다.

양방향 연결리스트를 이용해 이 문제를 해결할 수 있다.

## 양방향 연결리스트

테일 노드와 헤드 노드가 각각 서로를 가리키도록 하면 원형 양방향 연결리스트(Circulary Doubly L.L)라고 부른다. 본 강좌에서는 양방향 연결리스트라고 하면 원형 연결리스트를 지칭하는 것으로 한다.

## 원형 연결리스트

원형 연결리스트의 빈 리스트는 더미 노드(dummy node)라고 부른다. 더미 노드는 원형 연결리스트의 시작을 알리는 마커로서, key로 None을 넣어준다. 더미 노드는 헤드 역할을 하므로 헤드 노드라고 부르기도 한다.

## 구현

```py
class Node:
  def __init__(self, key = None):
    self.key = key
    self.next = self
    self.prev = self
  def __str__(self):
    # implement
  def __len__(self):
    # implement
```

```py
class DoublyLinkedList:
  def __init__(self):
    self.head = Node()
    self.size = 0
  def __iter__(self):
    # implement
  def __str__(self):
    # implement
  def __len__(self):
    # implement
```

## 양방향 연결리스트의 다양한 삽입 삭제 연산

### splice 연산

```py
def splice(self, a, b, x): # 세 개의 노드 a, b, x
  ap = a.prev, bn = b.next, xn = x.next
  ap.next = bn # cut
  bn.prev = ap # cut
  xn.next = a
  a.prev = x
  b.next = xn
  xn.prev = b
```

a와 b를 포함하는 노드를 cut 해서 x의 다음에 연결한다. 이때 x는 양방향 연결리스트 자기 자신일 수도 있고 다른 양방향 연결리스트일 수도 있다.

- 조건1: a -> ... -> b 형태로 배치
- 조건2: a와 b 사이에 head 노드가 없어야 함
- 조건2: a와 b 사이에 x 노드가 없어야 함

6개의 링크를 변경하면 cut과 재연결을 할 수 있다.
