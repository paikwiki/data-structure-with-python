# 이진트리 - 정의와 순회

> 본 포스팅은 한국외대 컴퓨터공학부 신찬수 교수님의 "[자료구조 - Data Structures with Python](https://www.youtube.com/playlist?list=PLsMufJgu5933ZkBCHS7bQTx0bncjwi4PK)" 중 24강 "[이진트리 - 정의와 순회](https://www.youtube.com/watch?v=HDjqrmmpFdU)" 강의를 정리한 노트입니다.

## 이진트리(Binary Tree)

이진트리의 표현법

- 배열과, 리스트를 이용한 표현법
- 노드와 링크를 클래스로 직접 표현. Node 클래스와 BT class를 이용한 표현법

### 클래스를 이용한 표현

```py
class Node:
  def __init__(self, key):
    self.key = key
    self.parent = self.left = self.right = None
  def __str__(self):
    return str(self.key)
```

사용 예시

```py
a = Node(6)
b = Node(9)
c = Node(1)
d = Node(5)
a.left = b
a.right = c
b.parent = c.parent = a
b.left = d
d.paren = b
```

```txt
    6
   / \
  9   1
   \
    5
```

### 이진트리 순회(traversal)

이진트리의 노드를 빠짐없이 출력하는 세가지 방법

```txt
       F
    /     \
   B       G
  / \       \
 A   D      I
    /\    /
   C  E  H
```

- preorder(MLR): F B A D C E G I H
- inorder(LMR): A B C D E F G H I
- postorder(LRM): A C E D B I H G F

M: 현재 노드, L: 좌측 서브트리, R: 우측 서브트리

### 구현

```py
class Node:
  def __init__(self, key):
    self.key = key
    self.parent = self.left = self.right = None
  def __str__(self):
    return str(self.key)
  def preorder(self): #현재 방문중인 노드 == self
    if self != None: # MLR
      print(self.key)
      if self.left:
        self.left.preorder()
      if self.right:
        self.right.preorder()
  def inorder(self):
    if self != None: # LMR
      if self.left:
        self.left.inorder()
      print(self.key)
      if self.right:
        self.right.inorder()
  def postorder(self):
    if self != None: # LRM
      if self.left:
        self.left.postorder()
      if self.right:
        self.right.postorder()
      print(self.key)
```

### reconstruct

`preorder`, `inorder`, `postorder` 중 두 개 이상의 출력된 결과를 기반으로 이진트리의 모양을 추측할 수 있다.
