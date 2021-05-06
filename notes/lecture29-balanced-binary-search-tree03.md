# 균형이진탐색트리(Balanced BST) - AVL 트리 삽입 연산

> 본 포스팅은 한국외대 컴퓨터공학부 신찬수 교수님의 "[자료구조 - Data Structures with Python](https://www.youtube.com/playlist?list=PLsMufJgu5933ZkBCHS7bQTx0bncjwi4PK)" 중 29강 "[균형이진탐색트리 - AVL 트리 삽입 연산](https://youtube.com/watch?v=KkgN2xAzmG8)" 강의를 정리한 노트입니다.

## AVL(Adelson-Velsky, Londis) 트리 구현

### AVL 트리에 새 노드 삽입

- AVL 트리: 모든 노드에 대해서, 노드의 왼쪽 서브트리와 오른쪽 서브트리의 높이차 <= 1

- class Node: BST 와 동일 <- 각 노드에는 key, left, right, parent에 height 변수 추가
- class BST: 사용. insert, deleteByMerging, deleteByCopying, search
- class AVL(BST)

> insert, delete 함수는 연산에 따라 height가 변하므로 수행시 height 정보를 업데이트 해야 한다.

```py
class AVL(BST):
  def insert(self, key):
    super(AVL, self).insert(key)
    v = super(AVL, self).insert(key) # step.1
    .
    .
```

- `AVL` 클래스에 `__init__`이 없으면 부모 클래스 `BST`의 생성자가 호출된다.
- `insert`는 BST와 똑같이 동작한 후, 높이차 조건에 위배되는 경우에는 조치를 취한다.
- 위배되는 경우를 바로잡는 것을 rebalance라고 한다.

> `super` 키워드: 첫번째인자(클래스)의 객체(self)의 부모를 호출

```txt
# insert(9)

 5     <- z
  \
   7   <- y
    \
     9 <- x 또는 v
```

- 9: 삽입된 새로운 값. v라고 부름
- 5: v로부터 올라가다가 AVL 트리의 조건을 만족하지 않는 첫번째 노드. z라고 부름
- 7: z의 자식노드. y라고 부른다. y의 자식노드인 v는 x라고 부른다.

> rebalance(x,y,z)

z에서 밸런스가 깨졌을 때, y는 z의 자식, x는 y의 자식이다.

### insert

> insert(self, key):

1. `v = super(AVL, self).insert(key)`
2. `find x, y, z`
3. `w = rebalance(x, y, z)`. w는 원래 z 위치에 있었던 노드
4. `if w.parent == Node: self.root = w`

`insert` 이후의 두 가지 케이스

1. z, y, x가 왼쪽 자식으로만 구성되거나, 오른쪽 자식으로만 구성되는 경우
2. z, y, x가 일직선이 아니고 각각 다른 방향의 자식일 경우, 세 점이 삼각형 모양으로 되는 경우.

### rebalance

1. z, y, x가 왼쪽으로 구성된 경우: `rotateRight(z)`
2. z, y, x가 일직선이 아니고 각각 왼쪽자식, 오른쪽 자식일 경우: `rotateLeft(y)`, `rotateRight(z)`

### 수행시간

1. `v = super(AVL, self).insert(key)`   -> O(h) = O(logN)
2. `find x, y, z`                       -> O(h)
3. `w = rebalance(x, y, z)`             -> O(1)
4. `if w.parent == Node: self.root = w` -> O(1)

삽입에는 O(logN) 시간이 소요된다.
