# 이진탐색트리 - 삭제 연산

> 본 포스팅은 한국외대 컴퓨터공학부 신찬수 교수님의 "[자료구조 - Data Structures with Python](https://www.youtube.com/playlist?list=PLsMufJgu5933ZkBCHS7bQTx0bncjwi4PK)" 중 26강 "[이진탐색트리 - 삭제 연산](https://www.youtube.com/watch?v=VVhmgQIJCu8)" 강의를 정리한 노트입니다.

## 삭제 연산

삭제 연산의 두 종류

- deleteByMerging
- deleteByCopying

### deleteByMerging

강의에서는 deleteByMerging을 살펴 본다.

x노드를 지울 때 x의 왼쪽노드를 L, 오른쪽 노드를 R이라고 했을 때, x 자리에 L을 두고, L의 가장 큰 노드의 자식 노드로 R을 연결하는 방식이다.

경우들:

1. L == None : R을 x 로 대체한다.
2. x == root : root 노드를 업데이트 해줘야 한다.

```py
deleteByMerging(self, x): # 노드 x 를 삭제
  a = x.left, b = x.right
  pt = x.parent
  # c == x를 대체할 노드
  # m == L에서 가장 큰 노드
  if a != None:
    c = a
    m = a
    while m.right:
      m = m.right
    if b != None:
      b.parent = m
      m.right = b
  else: # a == None
    c = b
  if pt != None:
    if c: c.parent = pt
    if pt.key < c.key:
      pt.right = c
    else:
      pt.left = c
  else:  # pt == None (root == x)
    self.root = c
    if c: c.parent = None
  self.size -= 1
  # return은 다음에 다시 설명하기로 함
```

강의 노트의 코드를 보면 충분히 이해할 수 있다.

### deleteByCopying

x 노드를 지울 때 x의 왼쪽노드를 L, 오른쪽 노드를 R이라고 했을 때, x를 지우는 게 아니라 값을 복사하는 방식으로 변경해주는 방법. L에서 가장 큰 값(m)을 찾아서 x에 복사해준다. 원래 m의 자리에는 m의 왼쪽 서브트리가 들어온다.

deletebyCopying은 직접 구현해볼 것.

### 삭제 연산의 수행 시간

- deleteByMerging: O(h)
- deleteByCopying: O(h)

두 함수 모두 m을 찾는데 드는 수행시간이 절대적으로 대부분을 차지.

- insert
- search(find_loc)
- delete(merging, copying)

위 함수 모두 O(h) 시간이 든다.

```py
# case 1
insert(1)
insert(2)
insert(3)
insert(4)

# case 2
insert(2)
insert(1)
insert(3)
insert(4)
```

같은 키 값을 저장해도 height의 크기가 전혀 다를 수 있다. 이는 수행시간의 큰 차이를 만들기 때문에 어떤 순서로 키값이 삽입되는지와 상관없이 가능하면 작게 유지하기 위한 서치트리를 균형이진탐색트리(balanced binary search tree)라고 부른다.
