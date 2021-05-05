# 알고리즘 시간 복잡도(Big-O 표기법)

> 본 포스팅은 한국외대 컴퓨터공학부 신찬수 교수님의 "[자료구조 - Data Structures with Python](https://www.youtube.com/playlist?list=PLsMufJgu5933ZkBCHS7bQTx0bncjwi4PK)" 중 5강 "[알고리즘 시간 복잡도(Big-O 표기법)](https://youtube.com/watch?v=0xGJx6qsNCY)" 강의를 정리한 노트입니다.

## 앞서 4강에서 본 3개의 함수의 시간 복잡도:

- Algorithm1(arrayMax): T<sub>1</sub>(n) = 2n - 1
- Algorithm2(sum1): T<sub>2</sub>(n) = 4n + 1
- Algorithm3(sum2): T<sub>3</sub>(n) = (3/2)n<sup>2</sup> - (3/2)n + 1

### 도출할 수 있는 명제:

1. Algorithm2가 Algorithm1보다 2배 느리다.
2. Algorithm3는 `n < (5/3) `이면 Algorithm2보다 빠르다.
3. Algorithm3는 모든 n에 대해서 Algorithm1보다 느리다.
4. Algorithm3는 `n > 5/3`이면 항상 Algorithm2보다 느리다.

- T1(n), T2(n)은 n에 대해 선형적으로 증가. 최고차항이 1차항
- T3(n)은 n에 대해 제곱으로 증가. 최고차항이 n의 2제곱

> n에 대한 최고차항 = 단위 시간의 증가율을 결정

## Big-O 표기법

이를 이용해 알고리즘의 수행시간을 간단하게 표기할 수 있다. 함수값을 결정하는 가장 중요한 최고차항만 표시하여 함수의 수행시간을 대략적으로 표현한다.

- T<sub>1</sub>(n) = 2n - 1 은 T<sub>1</sub>(n) = O(n)
- T<sub>2</sub>(n) = 4n + 1은 T<sub>2</sub>(n) = O(n)
- T<sub>3</sub>(n) = (3/2)n<sup>2</sup> - (3/2)n + 1은 T<sub>2</sub>(n) = O(n<sup>2</sup>)

### 표기방법

1. 최고차항만 남긴다
2. 최고차항 계수(상수)는 생략
3. Big-O(최고차항)

### 집합으로 이해하기

- T1(n) = O(n)
- T2(n) = O(n)

위 두 함수는 O(n) 집합 안에 들어있는 것으로 보면 된다. 즉,

- T1(n) ∈ O(n)
- T2(n) ∈ O(n)

### 예시

#### 예시1

```py
def inclrement_one(a):
  return a + 1
```

T(n) = 1 는 O(1) = O(n<sup>0</sup>)

#### 예시2

```py
def number_of_bits(n):
  count = 0
  while n > 0 :
    n = n // 2
    count += 1
  return count
```

n / (2<sup>count</sup>) = 1 는 log<sub>2</sub>N = count

T(n) = c·log<sub>2</sub>N + 1 = O(log<sub>2</sub>N)
