# 알고리즘 시간 복잡도(time complexity)

> 본 포스팅은 한국외대 컴퓨터공학부 신찬수 교수님의 "[자료구조 - Data Structures with Python](https://www.youtube.com/playlist?list=PLsMufJgu5933ZkBCHS7bQTx0bncjwi4PK)" 중 4강 "[알고리즘 시간 복잡도(time complexity)](https://youtube.com/watch?v=ysn9dLDNLEU)" 강의를 정리한 노트입니다.

## 알고리즘 시간 복잡도를 계산하는 방법

1. 모든 입력에 대해 기본연산 횟수를 더한 후 평균(__현실적으로 불가능__)
2. 가장 안 좋은 입력(Worstcase input)에 대한 기본연산 횟수를 측정(__worstcase time complexity__)

2번 방법의 경우 어떤 입력에 대해서도 W.T.C.보다 수행시간이 크지 않다. 즉 연산횟수가 보장된다.

> 알고리즘의 시간 복잡도를 정의하는 방법
>
> 알고리즘의 수행시간 = 최악의 입력에 대한 기본연산 횟수

```py
# input: n개의 정수를 갖는 배열 A
# output: A의 수 중에서 최대값 리턴
alogirithm arrayMax(A, n):
  currentMax = A[0]
  for i = 1 to n-1 do
    if currentMax < A[i]:
      currentMax = A[i]
  return currentMax
```

위 코드에서 `currentMax < A[i]` 조건이 항상 참일 경우 가장 연산횟수가 크다.

예시: `A = [2, 5, 7, 9, 15, 26]`

`for`문이 n - 1만큼 실행할 때 기본연산은 2번 수행씩 된다.

- 대입연산: `1` 단위시간
- 반복문: `(n - 1) * 2` = `2n - 2` 단위시간

> T(n) = 2n - 1

`n = 6` 일때, `T(6) = 12 - 1 = 11`

### 시간 복잡도 예시

#### 예시 1

```py
algorithm sum1(A, n):
  sum = 0                  # 대입연산 (1 단위시간)
  for i = 0 to n - 1 do
    if A[i] % 2 == 0:    # 짝수이면 (1 단위시간)
      sum += A[i]        # 더하고 대입하라(2 단위시간)
  return sum
```

`A`의 모든 값이 짝수이면 worstcase 입력

> T(n) = 4n + 1

`n`이 커지면 `n`에 비례해 수행시간이 커진다.

#### 예시 2

```py
algorithm sum2(A, n)
  sum = 0
  for i = 0 to n - 1 do
    for j = i to n - 1 do
      sum += A[i] * A[j]
  return sum
```

| i    | j     |
|------|-------|
| 0    | n     |
| 1    | n - 1 |
| 2    | n - 2 |
| n -1 | 1     |

```txt
1 + 2 + ... + n = (n(n + 1) / 2) * 3

T(n) = ((3/2)n)(n+1) + 1
     = (3/2)n^2 - (3/2)n + 1
```

`n`이 커지면 `n^2`에 비례해 수행시간이 커진다.
