# 스택(stack)

> 본 포스팅은 한국외대 컴퓨터공학부 신찬수 교수님의 "[자료구조 - Data Structures with Python](https://www.youtube.com/playlist?list=PLsMufJgu5933ZkBCHS7bQTx0bncjwi4PK)" 중 10강 "[스택(stack)](https://youtube.com/watch?v=MYk4autDAJ0)" 강의를 정리한 노트입니다.

## 스택의 사용예 2) 계산기 코드 작성2

- 문제:
  - 입력: +, -, *, /, (, ), 숫자(영문자)로 구성된 infix 수식
  - 출력: postfix 수식

- `A + B * C -> A B C * +`

분석

1. 피연산자의 순서는 그대로
2. 자신보다 연산자 우선순위가 낮은 연산자가 나올 때까지 대기(이때 스택에서 대기)

- `A * B + C -> A B * C +`
- `A + B + C -> A B C * +`

괄호가 있으면 괄호도 스택에 담는다. 오른쪽 괄호는 우선순위가 가장 높고 왼쪽 괄호는 우선순위가 가장 낮다.왼쪽괄호가 나오면 무조건 스택에 연산자를 담다가, 오른쪽 괄호가 오는 순간 왼쪽 괄호가 나올 때까지 `pop`을 한다.

### 구현하기

- 리스트: outstack
- 스택: opstack

```py
# psuedo code

for each token in expr:
  if token == operand:
    outstack.append(token)
  if token == '(':
    opstack.push(token)
  if token == ')':
    opstack에서 '('가 나올때까지 pop하면서 outstack에 `append`
  if token in '+*-/`:
    opstack에 token보다 우선순위 높은 연산자는 모두 `pop`한 후 자신을 `push`
opstack에 남은 연산자 모두 `pop`한 후 outstack에 `append`
```

위 psuedo code에 따라 아래 수식을 postfix 수식으로 변환하기

> `6 + (3 - 2) * 4`

왼쪽 괄호가 나오면 무조건 스택에 넣었다가 오른쪽 괄호가 나오는 시점에 왼쪽 괄호가 나올 때까지 pop 해준다. 이 부분 중요.

> `6 3 2 - 4 * +`

### postfix 수식을 이용해 계산하기

```py
# psuedo code

if token == operand
  S.push(token)
if token in '+-*/':
  a = S.pop()
  b = S.pop()
  S.push(a token b)
```

위 puedo code를 이용해 계산하면 10의 결과를 얻을 수 있다.
