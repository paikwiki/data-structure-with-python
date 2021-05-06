# 균형이진탐색트리(Balanced BST) - AVL 트리 정의

> 본 포스팅은 한국외대 컴퓨터공학부 신찬수 교수님의 "[자료구조 - Data Structures with Python](https://www.youtube.com/playlist?list=PLsMufJgu5933ZkBCHS7bQTx0bncjwi4PK)" 중 28강 "[균형이진탐색트리 - AVL 트리 정의](https://www.youtube.com/watch?v=dHHjrl6m5CE)" 강의를 정리한 노트입니다.

## AVL(Adelson-Velsky, Londis) 트리 개요

- 모든 노드에 대해서, 노드의 왼쪽 서브트리와 오른쪽 서브트리의 높이차가 1 이하인 BST
- 1964년에 발표

```txt
        10
       / \
      3  12
     / \
    1   5
       / \
      4   7
```

10을 기준으로, '왼쪽 서브트리의 높이'는 2, '오른쪽 서브트리의 높이'는 0이며, 이 경우에는 AVL 트리의 조건을 만족하지 못한다. 반면 3을 기준으로 보면 좌우 서브트리의 높이가 각각 0, 1로 AVL 트리의 조건을 만족한다. 12를 기준으로 했을 때 역시 좌우가 None이므로 조건을 만족한다(리프 노드는 모두 조건을 만족한다).

만약 12 노드 좌측 하단 노드에 11이 있다면 AVL 트리의 조건을 만족한다.

```txt
# 높이(h)가 0인 AVL트리 (자식 노드가 하나도 없는 트리) : 1개 유형

# h = 1: 3개 유형

  node   node       node
  /        \        /  \
node       node  node  node

# h = 2(아래 모양에서 유형별로 만들어 볼 것)

        node
       /    \
   node      node
   /  \      /  \
node node node  node
```

## AVL 트리의 최소 노드 갯수 N<sub>h</sub>

위 경우에서 노드수가 가장 적은 경우들을 보면,

- h = 0일 때, 노드 수는 1개
- h = 1일 때, 노드 수는 2개
- h = 2일 때, 노드 수는 4개

AVL 노드에서 각 서브트리가 최소의 노드를 가진 경우를 본다면,

h = 3 일때, 최소 노드를 가진 경우를 만들려고 하면 좌우 서브트리의 노드가 최소여야 한다.

- 좌측(또는 우측) 서브트리는 h = 2, 따라서 최소 노드 갯수는 4개
- 우측(또는 좌측) 서브트리는 h = 1, 최소 노드 갯수는 2개

N<sub>h</sub>: 높이가 h인 AVL 트리 중에서 최소 노드 갯수

- N<sub>0</sub> = 1
- N<sub>1</sub> = 2
- N<sub>2</sub> = 4
- N<sub>3</sub> = 7

## AVL 트리의 탐색 시간

그림을 그려서 점화식을 얻어보면,

> N<sub>h</sub> = N<sub>h-1</sub> + N<sub>h-2</sub> + 1

위의 점화식으로부터,

> N<sub>h</sub> >= 2N<sub>h-2</sub> + 1
>
> N<sub>h</sub> >= N<sub>h-2</sub>
>
> N<sub>h</sub> >= 2<sup>h/2</sup> * N<sub>0</sub>
>
> N<sub>h</sub> >= 2<sup>h/2</sup>

높이가 h이고 노드 갯수가 n인 AVL트리를 가정했을 때,

"h <= c·log<sub>2</sub>N"을 증명

```txt
N >= N<sub>h</sub> >= 2<sup>h/2</sup>
h / 2 <= log<sub>2</sub>N
h <= 2·log<sub>2</sub>N

∴ h = O(logN)
```
