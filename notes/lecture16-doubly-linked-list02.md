# 양방향 연결리스트 삽입-삭제-탐색 연산

> 본 포스팅은 한국외대 컴퓨터공학부 신찬수 교수님의 "[자료구조 - Data Structures with Python](https://www.youtube.com/playlist?list=PLsMufJgu5933ZkBCHS7bQTx0bncjwi4PK)" 중 16강 "[양방향 연결리스트 삽입-삭제-탐색 연산](https://youtube.com/watch?v=zWrFVf9_YTQ)" 강의를 정리한 노트입니다.

```txt
           |------------------v
head [.]->[0]<->[3]<->[-1]<->[9]
size [3]   ^------------------|
```

## 이동 연산

- `moveAfter(self, a, x)` -> `splice(a, a, x)`
- `moveBefore(a, x)` -> `splice(a, a, x.prev)`

## 삽입 연산

삽입

- `insertAfter(x, key)` -> `moveAfter(Node(key), x)`
- `insertBefore(x, key)` -> `moveBefore(Node(key), x)`

푸시

- `pushFront(key)` -> `insertAfter(self.head, key)`
- `pushBack(key)` -> `insertBefore(self.head, key)`

## 탐색 연산

탐색

```py
def search(self, key):
  v = self.head # dummy node
  while v.next != self.head:
    if v.key == key:
      return v
    v = v.next
  return None
```

## 삭제 연산

삭제

```py
def remove(x) # node x를 삭제
  if x == None or x == self.head:
    return
  x.prev.next = x.next
  x.next.prev = x.prev
  del x
```

popFront

```py
def popFront()
  if self.size == 0:
    return None
  remove(self.head.next)
```

popBack

```py
def popBack()
  if self.size == 0:
    return None
  remove(self.head.prev)
```

## 그외의 함수

- `join`: 두 연결리스트를 하나로 합침
- `split`: 하나의 연결리스트를 어떤 노드 x를 기준으로 나눔

## 양방향 연결리스트 연산의 수행시간

- `moveAfter/moveBefore`: O(1)     # splice 활용
- `insertAfter/insertBefore`: O(1) # splice 활용
- `pushFront/pushBack`: O(1)       # splice 활용
- `remove(x)`: O(1)
- `popFront/popBack`: O(1)
- `search(key)`: O(n)
- `splice(a, b, x)`: O(1)

`remove`는 `search`를 먼저 호출해야하므로 시간이 더 걸리 수 있다. 한 방향 연결리스트는 테일 노드를 수정하는 연산이 O(n)이었지만 원형 양방향 연결리스트는 O(1)이다.
