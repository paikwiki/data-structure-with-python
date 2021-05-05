# 스택(stack)

> 본 포스팅은 한국외대 컴퓨터공학부 신찬수 교수님의 "[자료구조 - Data Structures with Python](https://www.youtube.com/playlist?list=PLsMufJgu5933ZkBCHS7bQTx0bncjwi4PK)" 중 9강 "[스택(stack)](https://youtube.com/watch?v=G9ujrSGEB4A)" 강의를 정리한 노트입니다.



## 스택의 사용예 2) 계산기 코드 작성

```txt
 "2 + 3 * 5" - > '2', '+', '3', '*', '5'
                       ^연산자operator  ^피연산자operand
```

- 이항연산자(binary operator): 2 + 3, 3 * 5
- 단항연산자(unary operator): +3, -6

예시에서는 이항연산자만 다룸.

- infix 수식: "2 + 3 * 5" 처럼 연산자가 두 피연산자 사이에 있는 형식
- postfix로 변경하면: "2 3 5 * +"

infix를 postfix로 변경하는 규칙

1. 우선순위에 따라 괄호를 친다: "(2 + (3 * 5))"
2. 연산자의 오른쪽 활호 다음으로 연산자 이동: (2 (3 5) * ) +
3. 괄호 지우기: 2 3 5 * +

연습 해보기

- infix: `3 * (2 + 5) * 4`
- postfix: `3 2 5 + * 4 *`

1. 괄호치기: `((3 * (2 + 5)) *4)`
2. 연산자 이동: `((3 (2 5)+)* 4)*`
3. 괄호 지우기: `3 2 5 + * 4 *`
