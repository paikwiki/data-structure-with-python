# 균형이진탐색트리(Balanced BST) - AVL 트리 삭제연산

> 본 포스팅은 한국외대 컴퓨터공학부 신찬수 교수님의 "[자료구조 - Data Structures with Python](https://www.youtube.com/playlist?list=PLsMufJgu5933ZkBCHS7bQTx0bncjwi4PK)" 중 30강 "[균형이진탐색트리 - AVL 트리 삭제연산](https://www.youtube.com/watch?v=W3uPlSCzAZM)" 강의를 정리한 노트입니다.

## AVL(Adelson-Velsky, Londis) 트리 구현

### AVL 트리의 노드 삭제

```txt
# 1. u 삭제(불균형 상태)

     o
   /   \
 o       z
/|     /   \
oo    y     o
||   / \   /
oo  x   o  u
||  |\
oo  oo
||
oo

# 2. rotateRight(z)

     o
   /   \
 o       y
/|     /   \
oo    x     z
||   |\    / \
oo   oo   o   o
||
oo
||
oo
```

x y z를 정할 때는 height가 높은 쪽으로 간다. `rotateRight(z)`는 z의 부모노드(이 경우 root)의 균형을 깨뜨리게 된다. 이렇게 균형을 맞추려 하면 계속 부모의 균형에 영향을 주므로, 부모로 올라가면서 계속 맞춰야 한다.

`insert`의 경우에는 1회 또는 2회면 가능했으나 `delete`는 최악의 경우 모든 높이 레벨에서 다 회전을 수행해야 한다. O(logN) 회전이 필요할 수 있다.

### delete 구현

```py
delete(self, u):
  v = super(AVL, self).deleteByCopying(u)
    # v는 u를 삭제함으로써 균형이 깨질 수 있는(가능성이 있는) 가장 깊은 곳의 노드
    # 앞에서 살펴본 케이스에서는 u의 부모였던 노드가 v로 반환
    # 반환된 v로부터 균형이 깨진 노드를 다시 찾음
    # 강의 노트도 참고할 것
  while v != None:
    if v  is_not_balanced:
      z = v
      if z.left.height >= z.right.height:
        y = z.left
      else:
        y = z.right
      if y.left.height >= y.right.height:
        x = y.left
      else:
        x = y.right
      v = rebalance(x, y, z) #
    w = v # w는 예전에 v가 있었던 자리. 즉 v의 자식
    v = v.parent
  # while을 빠져나오면 v == None, w == root
  selft.root = w
```

### delete 수행시간

- 높이: <= 2logN : O(logN)
- insert: O(logN)
  - 노드 삽입 : O(logN)
  - rebalance: 1회 또는 2회 회전 O(1)
- delete
  - 노드 제거: O(logN)
  - rebalance: 매 level에서 O(logN) 회전

AVL트리는 insert, delete 를 모두 O(logN)만에 수행하는 균형이진 탐색트리의 대표적인 예 중 하나이다.
