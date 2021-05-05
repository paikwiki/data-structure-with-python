# 힙(Heap)

> 본 포스팅은 한국외대 컴퓨터공학부 신찬수 교수님의 "[자료구조 - Data Structures with Python](https://www.youtube.com/playlist?list=PLsMufJgu5933ZkBCHS7bQTx0bncjwi4PK)" 중 22강 "[힙(Heap)](https://youtube.com/watch?v=6VMSTOdHRfI)" 강의를 정리한 노트입니다.

```py
A = [2,8,6,1,10,15,3,12,11]
```

```txt
       2
     /   \
    8     6
   / \   / \
  1  10 15  3
 / \
12 11
```

위와 같은 힙 성질을 만족하지 않는 리스트를 힙 성질을 만족하도록 변경하는 것을 make_heap이라고 한다. 이를 위해서는 `heapify_down`을 반복적으로 수행

1, 12, 11을 보면,

- 1: A[3]
- 12: A[3 * 2 + 1] = A[7]
- 11: A[3 * 2 + 2] = A[8]

셋중 12가 가장 크므로, 1과 12를 바꾼다. A[3]과 A[7]을 바꾸면,

```py
A = [2,8,6,12,10,15,3,1,11]
```

6, 15, 3을 보면, 15가 가장 크므로 6과 15를 바꾼다.

```py
A = [2,8,15,12,10,6,3,1,11]
```

8, 12, 10을 보면 12가 가장 크므로 8과 12를 바꾼다.

```py
A = [2,12,15,8,10,6,3,1,11]
```

8, 1, 11을 보면 11이 가장 크므로 8과 11을 바꾼다.

```py
A = [2,12,15,11,10,6,3,1,8]
```

A[0]인 2를 자기자리를 찾으려면 2, 15를 바꾸고, 또 6과 2를 바꾼다.

```py
A = [15,12,6,11,10,2,3,1,8]
```

이렇게 하면 힙 성질을 만족한다.

결론: 자식노드와 비교하여 가장 큰 값을 부모 노드 자리로 옮기면 make_heap이 된다.

```py
make_heap(A):
  n = len(A)
  for k in range(n-1, -1, -1):
    #A[k] -> heap 성질 만족하는 곳으로 내려보낸다.
    heapify_down(k, n)
```

```py
heapify_down(k, n):
  # A[k], n값
  while A[k] != leaf:
    L, R = 2*k+1, 2*k+2
    m = index_max(A[k], A[L], A[R])
    if k != m:
      # A[K], A[m]을 swap
    else:
      break
```

## 성능

`heapify_down`은 `A[k]`를 `n`번 부른다. 상수 연산을 루트로부터 가장 깊은 리프노드까지 가는, 트리의 높이(height)만큼 반복하면 최악의 케이스이다.

> `T = O(nh) # h = height`

n개의 노드를 가진 힙의 높이 h는?

- level0 : 1
- level1 : 2
- level2 : 2<sup>2</sup>
- level3 : 2<sup>3</sup>
- level h - 1 : 2<sup>h - 1</sup>
- level h : < 2<sup>h</sup>

다 더하면 1 + 2 + 2^2 +..... + 2^(k-1) + 1 <= n

1 + 2 + 2^2 +.....+ 2^(k-1) = (2<sup>h -1</sup> / 2 - 1) + 1 = 2<sup>h</sup> <= n

`h <= log<sub>2</sub>n

- heapify_down: O(h) = O(logN)
- make_heap: o(nh) = O(nlogN) (사실은 O(n) 시간에도 된다)
