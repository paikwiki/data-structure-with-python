# 큐(queue)

> 본 포스팅은 한국외대 컴퓨터공학부 신찬수 교수님의 "[자료구조 - Data Structures with Python](https://www.youtube.com/playlist?list=PLsMufJgu5933ZkBCHS7bQTx0bncjwi4PK)" 중 11강 "[큐(queue)](https://youtube.com/watch?v=nqCNk_DmPio)" 강의를 정리한 노트입니다.

FIFO(First in First out) 규칙의 순차적 자료 구조

- 삽입: `enqueue`
- 삭제: `dequeue`

```py
enqueue(5)
enqueue(-2)
dequeue() # 5
enqueue(10)
dequeue() # -2
```

queue는 두 개의 인덱스가 필요하다.

- `enqueue`는 현재 어디까지 쌓여있는지 알아야 한다. (rear index)
- `dequque`는 다음에 나갈 인덱스를 알아야 한다. (front index)

```py
class Queue:
  def __init__(self):
    self.items = []
    self.front_index = 0
  def enque(self, val):
    self.items.append(val)
  def dequeue(self):
    if self.front_index == len(self.items): # 현재 dequeue할 수 있는 값이 없음
      print("Queue is empty")
      return None
    else:
      x = self.items[front_index]
      self.front_index += 1
      return x
```

## 큐 활용 예시: Josephus Problem

여섯 명(n)중에 2번째(k) 사람마다 죽는다면 몇 번의 사람이 살아남는가?

```txt
n = 6, k = 2
    1
  6   2
  5   3
    4
```

아래처럼 동작하면 된다.

```py
Josephus(n, k):
  return 최종 생존자의 번호
```

`n = 9, k = 3`이라면, `k - 1 = 2`는 `dequeue` 하자마자 다시 `enqueue`를 한다. `k` 번째가 나오면 `dequeue`를 하여 삭제한다. 이 로직을 마지막 살아남는 사람이 나올 때까지 반복한다. 코드는 강의 노트를 참고할 것.

## 덱(deque)

stack + queue 형태. 덱은 양쪽 끝에서 insert와 delete가 이루어진다.

- 삽입: `append`, `append_left`
- 삭제: `pop`, `pop_left`

파이썬에서는 `deque` 클래스를 제공한다. 덱 관련한 내용은 온라인 QnA에서 따로 설명한다.
