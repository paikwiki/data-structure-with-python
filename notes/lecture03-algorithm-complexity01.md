# 알고리즘 시간복잡도 1

> 본 포스팅은 한국외대 컴퓨터공학부 신찬수 교수님의 "[자료구조 - Data Structures with Python](https://www.youtube.com/playlist?list=PLsMufJgu5933ZkBCHS7bQTx0bncjwi4PK)" 중 3강 "[알고리즘 시간복잡도 1](https://youtube.com/watch?v=M2mcJvmYpWY)" 강의를 정리한 노트입니다.

## 자료구조와 알고리즘 성능: 가상컴퓨터 + 가상언어 + 가상코드

### 현실의 문제점

#### 문제점 1)

- "자료구조 + 알고리즘"을 생각하여 코드(C, Java, Python 등)로 구현하고 나면 실제 컴퓨터에서 동작하게 된다.
- 각 켬퓨터마다 HW/SW 환경이 다를 수 있으므로 다른 성능을 낼 수 있고, 이는 큰 문제가 될 수 있다.

#### 문제점 2)

- 입력의 크기가 다양할 수 있다. 다양한 크기의 입력에 대해 코드의 실행 속도를 어떻게 구할 수 있을까.

### 해결책

가상의 컴퓨터(Virtual Machine) + 가상언어(Pseudo language) + 가상코드(Pseudo Code) 를 가정한다.

#### 가상 컴퓨터(Virtual Machine/Random Access Machine)

Turing  Machine -> von Neumann: RAM(Random Access Machine)

RAM = CPU + Memory + 기본연산(단위시간에 수행되는 연산들의 모음)

기본연산이란: 배정, 대입, 북사연산 등으로 이들은 1 단위 시간이 드는 것으로 본다.

- `A = B`(Read and Write)
- 산술연산: +, -, *, / (%, 내림, 올림, 반올림 등은 기본 연산으로 보지 않으나, 수업에서는 이들도 단위시간에 들어가는 것으로 간주)
- 비교연산: >, >=, <, <=, ==, !=
- 논리연산: AND, OR, NOT
- 비트연산: bit-AND, OR, NOT

#### 가상 언어(Pseudo/Virtual Languages)

- 배정, 산술, 비교, 논리, bit-논리 연산 등 기본연산을 표현할 수 있으면 됨
- 비교: if, if else, if elseif... else 등
- 반복: for, while 등
- 함수: 정의, 호출, 반환 문법

#### 가상 코드(Pseudo Code)

실제 돌아가는 코드가 아닌 가상머신(RAM)에서 돌아가는 코드이므로 자유롭게 기술할 수 있다.

```py
# input: n개의 정수를 갖는 배열 A
# output: A의 수 중에서 최대값 리턴
alogirithm arrayMax(A, n):
  currentMax = A[0]
  for i = 1 to n-1 do      # 가상의 코드.
    if currentMax < A[i]:    # C 언어: for(int i = 1; i < n; i++){}
      currentMax = A[i]      # Python: for i in range(A, n):
  return currentMax
```

`A = [3, -1, 9, 2, 12], n = 5`일때 기본연산은 7회(`for` 선언 내부에서 쓰는 i와 관련한 연산은 제외)
