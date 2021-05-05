# 한방향 연결리스트

> 본 포스팅은 한국외대 컴퓨터공학부 신찬수 교수님의 "[자료구조 - Data Structures with Python](https://www.youtube.com/playlist?list=PLsMufJgu5933ZkBCHS7bQTx0bncjwi4PK)" 중 13강 "[한방향 연결리스트](https://youtube.com/watch?v=kGZoEShMcSQ)" 강의를 정리한 노트입니다.

## `pushFront`와 `pushBack`

```py
class SinglyLinkedList:
  def __init__(self):
    self.head = None
    self.size = 0
  def __len__(self):
    return self.size
  def pushFront(self, key):
    new_node = Node(key)
    new_node.next = self.head;
    self.head = new_node
    self.size += 1
  def pushBack(self, key):
    v = Node(key)
    if len(self) == 0:
      self.head = v
    else:
      tail = self.head
      while tail.next != None:
        tail = tail.next
      tail.next = v
    self.size += 1

```

사용 예시

```py
L = SinglyLinkedList()
L.pushFront(-1) # [-1]->0
L.pushFront(9)  # [9]->[-1]->0
L.pushFront(3)  # [3]->[9]->[-1]->0
L.pushFront(5)  # [5]->[3]->[9]->[-1]->0
L.pushBack(4)  # [5]->[3]->[9]->[-1]->[4]->0
```

## 삭제 연산 `popFront`와 `popBack`

> [5]->[3]->[9]->[1]->0

`popFront()`

```py
def popFront(self):
  if len(self) == 0:
    return None
  else:
    x = self.head
    key = x.key
    self.head = x.next
  self.size -= 1
  del x
  return key
```

`popBack()`

```py
def popBack(self):
  if len(self) == 0: return None
  else: # running techinque
    prev, tail = None, self.head
    while tail.next != None:
      prev = tail
      tail = tail.next
    if len(self) == 1:
      self.head = None
    else
      prev.next = tail.next # None
      key = tail.key
      del tail
      self.size -= 1
      return key
```

## 한방향 연결리스트의 수행 시간

- `pushFront`: O(1)
- `popFront`: O(1)
- `pushBack`: O(n)
- `popBack`: O(n)
