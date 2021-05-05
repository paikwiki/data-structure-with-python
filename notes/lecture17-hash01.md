# 해시 테이블

> 본 포스팅은 한국외대 컴퓨터공학부 신찬수 교수님의 "[자료구조 - Data Structures with Python](https://www.youtube.com/playlist?list=PLsMufJgu5933ZkBCHS7bQTx0bncjwi4PK)" 중 17강 "[해시 테이블](https://youtube.com/watch?v=Bzmepm6pYQI)" 강의를 정리한 노트입니다.

## 해시테이블 소개 및 해시 함수

해시 테이블(Hash Table): 매우 빠른 평균 삽입, 삭제, 탐색 연산 제공

딕셔너리 예시

```py
D = {}
D['2019317'] = "신찬수"
D['2019209'] = "홍길동"
D = { 2019317: "신찬수", 2019209: "홍길동" }
```

### 파이썬에서 key/value를 저장하는 방식

- "key: 2019317, value: "신창수""를 받으면 2019317 % 10의 위치에 저장
- "key: 2019209, value: "홍길동""을 받으면 2019209 % 10의 위치에 저장

"%10"은 열 칸 중에 하나에 저장하기 위해서임. 10칸은 임의의 예시.

만약 "2019235"를 찾으면 2019235 % 10 위치에 찾아가 확인한 후, 없음을 반환한다.

### 해시 함수(hash function)

저장하는 장소를 정할 때 key 값을 index 로 매핑한다. 이 매핑 과정에서 함수(여기서는 나머지 연산)가 쓰인다. 이 함수를 해시 함수라고 부른다.

새로 들어온 값을 저장하려 할 때, 그 곳에 기존의 값이 있으면 충돌(collistion) 발생. 이를 해결하는 걸 충돌 해결(collision resolustion)이라고 부르며 이 해결함수를 충돌 해결 방법이라고 부른다.

세 가지 주요 요소

1. Table: list
2. Hash function
3. Collision resolution method

#### 해시 함수 특징과 종류

```py
H, (H) = m # m은 slots 개수
```

앞서 예시처럼 나머지 연산으로 구분하는 해시 함수를 Division hash function이라고 부른다.

```py
f(k) = (k % P) % m # P는 소수(Prime)
```

이 방식은 간단하지만 충돌이 많이 발생한다. 각 슬롯에 골고루 분산되도록 해주는 해시 함수가 좋은 함수인데 이런 함수를 perfect hash function이라고 부른다. 가장 이상적인 형태의 해시 함수

```txt
key ----> slot
     1:1
```

Universal hash function: 충돌이 일어날 확률이 1/m인 해시 함수

```py
Pr(f(x) == f(y)) = 1/m
```

C-universal hash function: 충돌이 일어날 확률이 c/m인 해시 함수

```py
Pr(f(x) == f(y)) = c/m
```

다양한 해시 함수 종류

- Division
- Multiplication
- Folding
- Mid-squares
- Extraction

키 값이 문자열일 경우

- Addictive: key[i] 번째 문자를 전부 더해서 m으로 나머지 연산
- Rotating: 값 h를 계산하는데 initial_value를 임의로 준 후 for문으로 키값 문자열의 길이만큼 `h = (h << 4) ^ (h >> 28) ^ key[i]`한후 `h%P%m`을 반환
- Universal: 값 h 계산에서 `((h * a) + key[i])) % P`를 한후 `h%m`을 반환. `a`는 임의의 값. C++ STL 해시 함수로 사용되고 있음. 자바에서도 활용.

#### 좋은 해시 함수

1. Less collision
2. Fast computation

이 두 가지는 트레이드오프인 측면이 있다. 적절하게 만드는 게 중요하다.
