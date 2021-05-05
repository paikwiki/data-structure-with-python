# 해시 테이블

> 본 포스팅은 한국외대 컴퓨터공학부 신찬수 교수님의 "[자료구조 - Data Structures with Python](https://www.youtube.com/playlist?list=PLsMufJgu5933ZkBCHS7bQTx0bncjwi4PK)" 중 18강 "[해시 테이블](https://youtube.com/watch?v=Bj4pd9rJp5c)" 강의를 정리한 노트입니다.

## 충돌회피방법(Collision resolution method)

### Open addressing

 가고자하는 슬롯이 비어 있지 않을 경우 주위를 살펴보는 방식 세 가지

- linear probing: 바로 아래의 슬롯부터 확인해서 빈칸을 발견하면 저장
- quadratic probing
- double hashing

오픈 어드레싱과 대비되는 방법: Chaining

클러스터: 비슷한 키 값이 모여있는 단위를 말함. 클러스터가 크면 삽입/탐색에 시간이 많이 소요됨. 클러스터는 가급적 피해야 한다.

### 연산

#### set

1. key값이 H에 있으면 value를 업데이트
2. key값이 H에 없으면 (key, value)를 insert

`set`에 사용할 `find_slot` 함수

```py
find_slot(key): # key값이 있으면 slot 번호 리턴
                # key값이 없으면 key값이 삽입될 slot 번호 리턴
  i = f(key)
  start = i
  while ( H[i] == occupied) and (H[i].key != key)
    i = (i + 1)%m
    if i == start: return Full
  return i
```

set 함수

```py
set(key, value = None):
  i = find_slot(key)
  if i == Full: return None # 반환 전에 H를 키워야 함!
  if H[i].is_occupied:
    H[i].value = value
  else:
    H[i].key, H[i].value = key, value
  return key
```

#### search

```py

search(key):
```

set과 비슷하게 구현하면 된다. 교재 참고

#### remove

클러스터에서 사이에 있는 값이 사라지면 클러스터가 끊기지 않도록 아래에 있는 값을 올려줘야 한다. 이때 원래 자기 자리에 있는 값은 올려선 안 된다.

올려야 하는 값을 검색할 때는 클러스터의 끝까지 확인해줘야 한다.빈칸 또는 끝칸을 만날 때까지 작업을 한다.

`k = f(H[j].key)`일 때, 현재 타겟 i가 k와 j 사이에 있다면 (`k < i <= j`)라면 올릴 수 있다.

```py
remove(key):
  i = find_slot(key)
  if H[i].is_occupied: return None
  j = i # H[i]: 빈 slot, H[j]: 이사해야할 slot
  while True:
    H[i] = None
    while True: # H[j] 찾기
      j = (j + 1) % m
      if H[j].is_occupied: return key
      k = f(H[j].key)
      if (k < i <= j):break
    H[i] = H[j]
    i = j
```

### 성능

- 성능은 클러스터의 길이에 비례한다.
- 클러스터의 길이를 결정하는 것은 해시 함수.
- 충돌 해소를 어떤 방식으로 하는지 여부
