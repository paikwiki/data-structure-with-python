# 자료구조와 알고리즘

> 본 포스팅은 한국외대 컴퓨터공학부 신찬수 교수님의 "[자료구조 - Data Structures with Python](https://www.youtube.com/playlist?list=PLsMufJgu5933ZkBCHS7bQTx0bncjwi4PK)" 중 2강 "[자료구조와 알고리즘](https://youtube.com/watch?v=jgWyu83DfO0)" 강의를 정리한 노트입니다.

## 개요

자료구조

- 자료(data)를 담기 위한 저장공간과 연산을 통칭
- 자료구조 = 저장공간(memory) + 연산(읽기, 쓰기, 삽입, 삭제 탐색)

알고리즘

- 자료를 입력받아 유한한 횟수의 연산들을 이용해 원하는 결과를 출력하는 것

> 자료구조와 알고리즘은 뗄레야 뗄 수 없는 바늘과 실 같은 것

### 자료구조의 예

#### 변수(variable)

```py
a = 5     # 쓰기 연산
print(a)  # 읽기 연산
```

#### 배열(array), 리스트(list)

```py
A = [3, -1, 5, 7] # 접근: 원소의 index를 이용
                  # 읽기 쓰기 예: A[3]
                  # 삽입: A.append(9) 마지막 자리(A[4])에 원소를 추가
                  #       A.intsert
                  # 삭제: A.pop() 매개변수가 없으면 마지막 값을 반환 후 삭제
                  #       A.pop(2)
```

### 알고리즘의 예

- 100개의 정수를 리스트 A에 담는다(입력)
- 오름차순 정렬(출력)

## 알고리즘

인류 최초의 알고리즘: 최대공약수(GCD) 계산 알고리즘(By Euclid)

9세기, 페르시아, Algebra 수학자 Al-Khwarizmi -> 유럽에 라틴어로 번역되는 과정에 Algorismus로 번역됨. 수학자의 이름과 라틴어 수인 "Arithmos"이 합쳐져 "Algorithm"이 됐다는 게 정설.

gcd(8, 12) = max{1, 2, 4} = 4

```py
gcd_sub(a, b):
  while a != 0 and b != 0:
    if a > b: a = a - b
    else: b = b - a
  return a + b

# 개선
gcd_mod(a, b):
  while a != 0 and b != 0:
    if a > b: a = a % b
    else: b = b % a
  return a + b

# gcd_rec(recursive)
```
