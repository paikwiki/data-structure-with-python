# 연결리스트(Linked List)

> 본 포스팅은 한국외대 컴퓨터공학부 신찬수 교수님의 "[자료구조 - Data Structures with Python](https://www.youtube.com/playlist?list=PLsMufJgu5933ZkBCHS7bQTx0bncjwi4PK)" 중 12강 "[연결리스트(Linked List)](https://youtube.com/watch?v=sMpsvA5O0xU)" 강의를 정리한 노트입니다.

한방향 vs. 양방향

## 배열과 연결리스트 비교

배열은 메모리 공간에 순차적으로 배치되므로 `[]` 연산자로 상수시간 접근이 가능하다. 하지만 연결리스트는 메모리상에서 흩어져 있어서 상수시간 접근이 불가능하다.

연결리스트의 마지막 요소에는 None(C에서의 NULL)이 있다. 이는 다음 값이 없다는 것을 의미하고 그 앞의 값이 마지막 값이 된다.

연결리스트의 각 노드는 data 값(key)과 다음 주소의 값(link) 쌍을 항상 갖고 있어야 한다. 이 쌍을 노드(node)라고 부른다. 노드와 링크로 연결된 구조를 연결리스트라고 부른다.

가장 앞의 노드를 헤드 노드(head node)라고 부른다. n번째의 값을 가져오려면 헤드 노드로부터 링크를 따라가야만 한다.

연결리스트의 장점

- 배열에서 값과 값 사이에 새 값을 넣으려면 삽입한 값 이후의 모든 요소를 한 칸씩 이동해야 한다. 하지만 연결리스트는 중간에 새 노드를 넣고 다시 연결해주면 된다. 두 개의 링크 주소만 바꾸면 되므로 insert 작업에는 상수시간이 걸린다. 단 교체해야할 노드를 알고 있을 때에 상수시간이다.

## 한 방향 연결 리스트 vs 양 방향 연결 리스트

- 한 방향: 링크가 한쪽 방향으로만 연결되어 있으므로, 한 방향으로만 갈 수 있고 반대 방향으로는 갈 수 없다.
- 양 방향: 양쪽 방향으로 링크가 있어서 노드의 양쪽 방향으로 모두 이동할 수 있다.

## 구현해보기

```py
class Node:
  def __init__(self, key = None):
    self.key = key
    self.next = None
  def __str__(self):
    return str(self.key) # print(v.key) 대시 print(v)로 쓸 수 있다.
```

사용 예시

```py
a = Node(3)
b = Node(9)
c = Node(-1)

a.next = b
b.next = c
```

`c` 노드를 테일 노드(tail node)라고 부른다.

헤드 노드의 앞에 `head`와 `size`를 갖고 있는 객체를 만들어서 헤드 노드 앞에 붙이려 한다.

```py
class SinglyLinkedList:
  def __init__(self):
    self.head = None
    self.size = 0
  .
  .
  .
```

한방향 연결리스트에 대해서는 다음 동영상에서 본격적으로 살펴본다.
