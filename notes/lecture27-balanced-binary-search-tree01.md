# 균형이진탐색트리(Balanced BST) - 정의와 회전

> 본 포스팅은 한국외대 컴퓨터공학부 신찬수 교수님의 "[자료구조 - Data Structures with Python](https://www.youtube.com/playlist?list=PLsMufJgu5933ZkBCHS7bQTx0bncjwi4PK)" 중 27강 "[균형이진탐색트리 - 정의와 회전](https://www.youtube.com/watch?v=Kuw0f3-E-Hw)" 강의를 정리한 노트입니다.

## 이진탐색트리

- 각 노드 x의 좌측에는 x보다 작거나 같은 값이, 우측에는 x보다 큰 값이 있다는 조건을 만족해야 한다
- 탐색, 삽입, 삭제에 O(height) 시간만큼 소요된다. 삽입, 삭제는 탐색의 비용에 영향을 받는다.
- 비효율적으로(연결리스트처럼) 저장되면 "h <= n - 1"이 될 수 있다.

```txt
    1
     \
     10
     /
    8
   /
  5
   \
    7
```

반면, 힙의 높이는 항상 "log(n+1) <= h <= n - 1"을 보장.

## 균형이진탐색트리

힙처럼 항상 트리의 높이가 O(logN) 정도로 보장이 되는 트리를 균형이진탐색트리라고 한다.

### 균형이진탐색트리의 예

- AVL트리
- 레드블랙(Red-Black) 트리
- (2,3,4)-트리
- 스프레이(splay) 트리

### 균형을 맞추는 방법

- 트리의 높이가 커질 때 트리를 조정해 항상 높이를 O(logN) 정도로 유지
- 이때 사용하는 함수가 회전(Rotation)

```txt
     z     <--------      x
   /  \         left     / \
  x    c  [rotation]    a   z
 /  \          right       / \
a    b    --------->      b   c
```

### 균형이진탐색트리의 회전

우측 회전

- 왼쪽의 일부가 높이 레벨 1만큼 증가하고, 오른쪽의 일부가 높이 레벨 1만큼 감소한다
  - x: level 1 증가, z: level 1 감소
- 총 6개의 링크를 변경해야 한다

좌측 회전

- 왼쪽의 일부가 높이 레벨 1만큼 감소하고, 오른쪽의 일부가 높이 레벨 1만큼 증가한다
  - x: level 1 감소, z: level 1 증가
- 총 6개의 링크를 변경해야 한다

### 회전 구현

```py
def rotateRight(self, z):
  if not z: return
  x = z.left
  if x == None: return
  b = x.right
  x.parent = z.parent     # 1st update
  if z.parent:
    if z.parent.left == z:
      z.parent.left = x  # 2nd update
    else:
      z.parent.right.x
  x.right = z     # 3rd update
  z.parent = x    # 4th update
  x.left = b      # 5th update
  if b:
    b.parent = z  # 6th update
  if self.root == z:
    self.root = x
```

`rotateLeft`는 `rotateRight`에 대칭적으로 구현하면 된다.

### 회전 연산의 수행 시간

균형이진탐색트리의 회전은 O(1) 시간이 든다.
