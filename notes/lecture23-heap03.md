# 힙(Heap)

> 본 포스팅은 한국외대 컴퓨터공학부 신찬수 교수님의 "[자료구조 - Data Structures with Python](https://www.youtube.com/playlist?list=PLsMufJgu5933ZkBCHS7bQTx0bncjwi4PK)" 중 23강 "[힙의 insert 연산](https://youtube.com/watch?v=gVRDc5NRjjw)" 강의를 정리한 노트입니다.

## 힙의 insert 연산

```py
A = [15,12,6,11,10,2,3,1,8]
```

```txt
       15
     /   \
    12    6
   / \   / \
  11 10 2   3
 / \
1   8
```

`insert(14)` -> 10의 왼쪽 끝에 들어가므로, 삽입하고 나면,

```py
A = [15,12,6,11,10,2,3,1,8,14]
```

```py
insert(14)
  A.append(14)
```

자리를 두번 바꿔야 한다.

```py
A = [15,12,6,11,14,2,3,1,8,10]
```

```py
A = [15,14,6,11,12,2,3,1,8,10]
```

14가 자기자리를 찾도록 재배치하면 전체적으로 힙이 완성된다. 부모노드로 가면서 자신의 자리를 찾도록 만드는 함수를 `heapify_up`이라고 부른다.

```py
insert(14)
  A.append(14)
  A.heapify_up(9)
  # A[k]를 root 방향으로 이동하면서 heapify를 해준다.

heapify(k):
  while k > 0 and A[(k -1)//2)] < A[k]:
    A[k], A[(k-1) //2] = A[(k-1) //2], A[k]
    k = (k - 1) // 2
```

최악의 경우 리프에서 루트까지 연산. `insert`와 `heapify_up` 모두 h = O(logN).

## 힙의 find_max 연산

```py
A = [15,12,6,11,10,2,3,1,8]
```

```txt
       15
     /   \
    12    6
   / \   / \
  11 10 2   3
 / \
1   8
```

```py
find_max:
  return A[0] # O(1)
```

## 힙의 delete_max 연산

A[0] 을 없애면서 가장 마지막 리프노드를 루트로 옮긴다. 그 후 A[0]를 `heapify_down(0, n)` 해준다.

```txt
       15
     /   \
    12    6
   / \   / \
  11 10 2   3
 / \
1   8
```

```py
delete_max: # O(logN)
  if len(A) == 0: return None
  key = A[0]
  A[0], A[len(A) - 1] = A[len(A) - 1], A[0]
  A.pop()
  heapify_down(0, len(A))
  return key
```

### 성능

- `make_heap`: O(n), O(nlogN)
- `insert`: O(logN)
- `find_max`: O(1)
- `delete_max`: O(logN)
- `heapify_down`: O(h) = O(logN)
- `heapify_up`: O(h) = O(logN)

### 기타

힙에는 `search` 함수가 없다. 정리가 되어 있는 게 아니다보니 알 방법이 없어서 무조건 모두 탐색해야한다. `search`는 효율이 없고 `insert`, `find_max`, `delete_max`를 이용하는 경우에 힙이 좋다.

`find_min`과 `delete_min`을 갖는 힙인 min_heap을 만들 수 있다. 우리가 만든 힙은 max_heap이다.

정렬을 하는 경우, 힙 소트를 할 수 있다. `make_heap()`은 O(nlogN)이므로 정렬 후 `delete_max()`의 반환과 유사한 형식을 이용해 할 수 있다. (자세한 내용은 나중에 다시 확인할 것!)
