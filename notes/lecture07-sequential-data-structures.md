# 순차적 자료구조 소개

> 본 포스팅은 한국외대 컴퓨터공학부 신찬수 교수님의 "[자료구조 - Data Structures with Python](https://www.youtube.com/playlist?list=PLsMufJgu5933ZkBCHS7bQTx0bncjwi4PK)" 중 7강 "[순차적 자료구조 소개](https://youtube.com/watch?v=buJBlTsWlW0)" 강의를 정리한 노트입니다.

## 1. array, list

- `index`로 임의의 원소에 접근할 수 있다.
- 연산자 `[]`로 접근할 수 있다. 상수시간(O(1))에 값을 알 수 있다.
- 삽입(`append`, `insert`)
- 삭제(`pop`, `remove`)

`append`와 `pop`은 O(1)이지만, `insert`와 `remove`는 O(n)

## 2. stack, queue, dequeue

- 제한된 접근(삽입, 삭제)만 허용한다.

### stack

- LIFO(Last In First Out)
- 자루처럼 먼저 넣은 것이 밑에 있고, 꺼낼 때 나중에 넣은, 가장 위의 것이 나온다.
- `push`: 삽입. 아래에서부터 차곡차곡 삽입된다.
- `pop`: 삭제. 맨 위 값(가장 나중에 들어온 값)에서부터 삭제한다.

제한된 연산을 가진 자료구조가 많이 쓰인다.

### queue

- FIFO(First In First Out)
- 선착순(가장 먼저 온 사람이 가장 먼저 서비스를 받는다)
- 삽입은 아래서부터 차곡차곡 쌓인다.
- 삭제 역시 아래의 값(가장 먼저 들어온 값)부터 수행한다.

### dequeue

- stack + queue
- 삽입은 위, 아래로 수행할 수 있다.
- 삭제 역시 위, 아래로 수행할 수 있다.

## 3. linked list(연결 리스트)

- 파이썬의 list는 배열과 유사. linked list와는 다르다.
- 값이 연속된 공간이 아닌 메모리 공간에 독립적으로 저장된다.
- 다음 값이 저장된 주소를 갖고 있다(link).
- 각각의 값은 자기자신의 값과 함께 다음 값의 주소를 갖고 있다.
- 마지막 요소는 다음 값의 주소 대신 `NULL`(Python에서는 `None`)을 갖고 있다.
- `index`로 접근할 수 없음.
- n번째 값을 가져오고 싶다면 첫번째로부터 순차적으로 조회해야한다.
