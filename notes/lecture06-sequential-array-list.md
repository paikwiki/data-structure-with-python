# 순차적 자료구조: 배열과 리스트

> 본 포스팅은 한국외대 컴퓨터공학부 신찬수 교수님의 "[자료구조 - Data Structures with Python](https://www.youtube.com/playlist?list=PLsMufJgu5933ZkBCHS7bQTx0bncjwi4PK)" 중 6강 "[순차적 자료구조: 배열과 리스트](https://youtube.com/watch?v=Lqd8o7vL2Z8)" 강의를 정리한 노트입니다.

## 배열(array) VS. 리스트(list) <- Python

- 가장 기본적인 순차적(sequential) 자료구조(매우 기본, 중요)

```c
int A[4] = {2, 4, 0, 5};
```

`A[0]`에는 첫번째 요소의 바이트 주소가 저장되어 있다.

`A[2] = A[2] + 1`: `A[2]`에 대한 읽기/쓰기 수행. `A[2]`의 값이 업데이트(산술연산), 대입(`=`) 연산. 이 연산은 모두 상수시간(O(1))이 걸림. 계산의 편의상 읽기/쓰기를 카운트하지 않았으나 원래는 1 단위시간이 걸린다.

RAM이므로 `A[2]`의 주소가 있으면 값을 바로 가져올 수 있다.

`A[0]`의 주소에서 + (4bytes * 2개)

`A[0]`의 주소가 `100`이라면 `A[2]`는 `108`. 산술연산 두 번으로 구할 수 있으므로, `O(1)`로 볼 수 있다.

> 배열은 `index`를 이용해 특정 위치의 값을 상수시간 내에 읽고 쓸 수 있게 해주는 자료구조이다.

### Python의 list

`index`를 이용해 값을 읽고 쓸 수 있으며, 더 많은 함수를 제공한다.

```py
A = [2, 4, 0, 5]
```

파이썬의 리스트는 각각의 값을 다른 메모리에 저장한다. `2`, `4`, `0`, `5`는 객체가 되고, 따로 저장되며, `A[0]`은 `2`가 저장된 곳의 주소를 가리키고, `A[1]`은 `4`가 저장된 곳의 주소를 가리킨다.

`A[2] = A[2] + 1`을 수행하면 `A[2]`가 가리키던 `0` 객체를 더이상 가리키지 않고, `1`을 갖고 있는 객체를 가리키게 된다.

#### Python list의 함수들

- `A.append(6)`: list의 맨 뒤에 `6`을 삽입(이전과 마찬가지로 마지막 위치에 `6`을 가리키는 주소를 저장)
- `A.pop()`: list 맨 뒤의 값을 삭제하고 반환
- `A.pop(1)`: `A[1]`을 제거하고 반환. `A[1]` 이후의 요소 `A[n]`은 `A[n -1]`으로 이동

`append()`와 `pop()`은 기본으로 제공되는 삽입/삭제 연산

- `A.insert(1, 10)`: `A[1]`에 `10`을 삽입. 기존의 `A[1]` 이후의 요소 `A[n]`은 `A[n + 1]`로 이동
- `A.remove(value)`: `A`에서 왼쪽으로부터 첫번째 `value`를 찾아 제거. 삭제한 `A[v]` 이후의 `A[n]`은 `A[n  - 1]`로 이동
- `A.index(value)`: `A`를 왼쪽부터 검색해 첫번째 `value`의 인덱스 반환
- `A.index(value)`: `A`를 왼쪽부터 검색해 해당 `value`의 개수 반환

파이썬의 list는 다양한 연산을 제공해 편의성이 높다.

#### list의 이점

- 용량(capacity)를 자동으로 조절한다. 공간이 부족하면 더 큰 용량을 할당하여 값을 저장.
- `pop()`에 의해 요소들이 삭제가 되면 더 작은 용량을 할당하여 작은 리스트를 유지.

> dynamic array: 자동으로 용량을 조정하는 배열. C 언어에서는 제공하지 않는다.

```c
int A[4] = {2, 4, 0, 5}
A[4] = 10;     // error

// 배열의 크기를 바꾸려면
int *b = (int *)malloc(sizeof(int) * 4); // 동적 할당
int *c = (int *)malloc(sizeof(int) * 6); // 동적 할당
free (b);
b = c;
free(c);
```

아래 코드로 배열의 크기가 변경되는 것을 확인할 수 있다.

```py
import sys

a = []                             # empty list
print(sys.getsizeof(A))  # 28bytes(운영체제에 따라 다를 수 있음)
A.append(10)
print(sys.getsizeof(A)) # 44bytes(운영체제에 따라 다를 수 있음)
```

#### list는 클래스(class)

list A가 있다면 그 안에는:

- `capacity`: 용량
- `n`: 현재 저장된 값의 개수

`capacity`가 `100`일 때, `append()` 연산이 반복되면 `n`이 증가.

`A.append(x)`의 동작을 개념적으로 살펴보면:

```py
if A.n < A.capacity:
  A[n] = x
  A.n = n + 1
else: A.n == A.capacity
  B = A.capacity * 2 # 2배 크기의 리스트 새로 할당
  for i in range(n):
    B[i] = A[i]           # A의 값을 B로 복사 O(n)만큼의 시간 소모
  del A
  A = B
  A[n] = x
  A.n = n + 1
```

#### list의 연산별 시간복잡도(Big-O)

- `A.append()`, `A.pop`: O(1) 평균
- `A.insert()`, `A.remove()`: O(n) w.c
- `A.index()`, `A.count()`: O(n) w.c
