# 이진탐색트리 - 정의와 탐색, 삽입 연산

> 본 포스팅은 한국외대 컴퓨터공학부 신찬수 교수님의 "[자료구조 - Data Structures with Python](https://www.youtube.com/playlist?list=PLsMufJgu5933ZkBCHS7bQTx0bncjwi4PK)" 중 25강 "[이진탐색트리 - 정의와 탐색, 삽입 연산](https://www.youtube.com/watch?v=Bhprzw_1kb0)" 강의를 정리한 노트입니다.

## 이진탐색트리

특정 키 값을 찾는 연산을 효율적으로 할 수 있도록 조직화한 트리

이진탐색트리의 정의

- 각 노드의 왼쪽 서브트리의 key 값은 노드의 key 값보다 작거나 같아야 한다.
- 각 노드의 오른쪽 서브트리의 key 값은 노드의 key 값보다 커야 한다.

이진탐색트리의 예

```txt
      15
    /    \
   4      20
  /      / \
 2     17   32
        \
        19
```

모든 노드에 대해서 위 조건이 만족되어 있어야 한다.

- 15의 왼쪽 노드: 2, 4
- 15의 오른쪽 노드: 20, 17, 32, 19
- 20의 왼쪽 노드: 17, 19
- 20의 오른쪽 노드: 32

이렇게 구성하면 현재의 key 값을 기준으로 검색해야할 노드의 방향을 결정할 수 있다.

탐색 시 level by level로 내려가므로 위 예시에서는 height가 3이고, 수행시간은 O(h)이다.

## 구현

### BST 클래스

```py
class BST:
  def __init__(self):
    self.root = None
    self.size = 0
  def __len__(self):
    return self.size
  def __iter__(self):
    return self.root.__iter__() # Node클래스에 구현된대로 방문.
                                # generator에 대해 별도 학습할 것
```

사용 예시

```py
T = BST()
T.insert(15) # 아직은 구현 전인 함수
T.insert(4)
```

### 탐색

`find_loc()`

```py
def find_loc(self, key):
  if self.size == 0: return None
  p = None # p is parent of v
  v = self.root
  while v: # while v != None
    if v.key == key: return v
    elif v.key < key:
      p = v
      v = v.right
    else:
      p = v
      v = v.left
  retern p
```

`search()`

```py
def search(self, key):
  v = self.find_loc(key)
  if v == None:
    return None
  else:
    return v
```

### 삽입

- 탐색트리는 규칙을 갖고 있으므로 key가 들어갈 위치가 정해진다.

`insert()`

```py
def insert(self, key):
  p = self.find_loc(key) # find_loc() 은 O(h)
  if p == None or p.key != key:
    v = Node(key)
    if p == None:
      self.root = v
    else:
      v.parent = p
      if p.key >= key: # left/right
        p.left = v
      else:
        p.right = v
    self.size = self.size + 1
    return v
  else:
    print("key is already in the tree")
    return p # 중복 key를 허용하지 않으면 None 리턴 p == None
```

`insert()` 함수는 O(h)
