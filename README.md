# 한국외국어대학교 컴퓨터공학부 신찬수 교수님의 자료구조 강의(2020-1)

한국외대 컴퓨터공학부 신찬수 교수님의 "[자료구조 - Data Structures with Python](https://www.youtube.com/playlist?list=PLsMufJgu5933ZkBCHS7bQTx0bncjwi4PK)" 강의를 정리한 노트입니다.

## 안내

1. 학습한 날짜를 아래의 표에 정리합니다.
2. 본 노트는 학습 요약보다는 강의에 집중하기 위한 사적인 필기에 가깝습니다.
3. 총 55강으로 구성되어 있으나, 현재 저에게 필요한 내용인 AVL 트리에 대한 강의인 30강까지만 학습했습니다.
4. 항목 2,3 의 이유로, 수업의 내용에 비해 정리가 부족할 수 있습니다.
5. 노트의 코드는 파이썬 언어의 형태를 하고 있으나, 의사 코드(Psuedo code)가 섞여 있습니다.
6. 전체 동영상 강의와 교수님의 강의 노트를 기반으로 학습하는 것을 권장합니다.

## 동영상 강의 링크와 요약 노트

4월 30일부터 5월 6일까지 총 7일간 학습했습니다. 전체 강좌의 링크는 아래에서 확인할 수 있습니다.

- "자료구조 - Data Structures with Python" 동영상 강의 목록: [https://www.youtube.com/playlist?list=PLsMufJgu5933ZkBCHS7bQTx0bncjwi4PK](https://www.youtube.com/playlist?list=PLsMufJgu5933ZkBCHS7bQTx0bncjwi4PK)

| 연번 | 동영상 링크                         | 노트        | 학습일        |
| -: | --------------------------------- | ----------- | ----------- |
|  1 | [자료구조(2020-1) 과목 소개](https://youtube.com/watch?v=PIidtIBCjEg)                    | [:memo: note](./notes/lecture01-intro.md) | 2021.04.30. |
|  2 | [자료구조와 알고리즘](https://youtube.com/watch?v=M2mcJvmYpWY)                            | [:memo: note](./notes/lecture02-data-structure-and-algorithm.md) | 2021.05.01. |
|  3 | [알고리즘 시간복잡도1](https://youtube.com/watch?v=jgWyu83DfO0)                           | [:memo: note](./notes/lecture03-algorithm-complexity01.md) | 2021.05.01. |
|  4 | [알고리즘 시간복잡도2](https://youtube.com/watch?v=ysn9dLDNLEU)                           | [:memo: note](./notes/lecture04-algorithm-complexity02.md) | 2021.05.01. |
|  5 | [알고리즘 시간복잡도 BigO](https://youtube.com/watch?v=0xGJx6qsNCY)                       | [:memo: note](./notes/lecture05-algorithm-complexity03.md) | 2021.05.01. |
|  6 | [순차적 자료구조: 배열과 리스트](https://youtube.com/watch?v=Lqd8o7vL2Z8)                   | [:memo: note](./notes/lecture06-sequential-array-list.md) | 2021.05.01. |
|  7 | [순차적 자료구조 소개](https://youtube.com/watch?v=buJBlTsWlW0)                           | [:memo: note](./notes/lecture07-sequential-data-structures.md) | 2021.05.02. |
|  8 | [스택(Stack)](https://youtube.com/watch?v=OzFXiukhv8o)                               | [:memo: note](./notes/lecture08-stack.md) | 2021.05.02. |
|  9 | [스택 활용 - 계산기(1/2)](https://youtube.com/watch?v=G9ujrSGEB4A)                      | [:memo: note](./notes/lecture09-stack-calculator01.md) | 2021.05.02. |
| 10 | [스택 활용 - 계산기(2/2)](https://youtube.com/watch?v=MYk4autDAJ0)                      | [:memo: note](./notes/lecture10-stack-calculator02.md) | 2021.05.02. |
| 11 | [큐(Queue)](https://youtube.com/watch?v=nqCNk_DmPio)                                 | [:memo: note](./notes/lecture11-queue.md) | 2021.05.02. |
| 12 | [연결리스트 소개](https://youtube.com/watch?v=sMpsvA5O0xU)                               | [:memo: note](./notes/lecture12-linked-list.md) | 2021.05.03. |
| 13 | [한방향 연결리스트 - 삽입,삭제 연산](https://youtube.com/watch?v=kGZoEShMcSQ)                | [:memo: note](./notes/lecture13-singly-linked-list01.md) | 2021.05.03. |
| 14 | [한방향 연결리스트 - 탐색 연산](https://youtube.com/watch?v=aCHwXmpuAkY)                    | [:memo: note](./notes/lecture14-singly-linked-list02.md) | 2021.05.03. |
| 15 | [양방향 연결리스트 - splice 연산](https://youtube.com/watch?v=nQhzNRmnmt8)                 | [:memo: note](./notes/lecture15-doubly-linked-list01.md) | 2021.05.03. |
| 16 | [양방향 연결리스트 - 삽입,삭제,탐색 연산](https://youtube.com/watch?v=zWrFVf9_YTQ)            | [:memo: note](./notes/lecture16-doubly-linked-list02.md) | 2021.05.04. |
| 17 | [해시 테이블 - 소개, 해시 함수](https://youtube.com/watch?v=Bzmepm6pYQI)                   | [:memo: note](./notes/lecture17-hash01.md) | 2021.05.04. |
| 18 | [해시 테이블 - open addressing(linear probing)](https://youtube.com/watch?v=Bj4pd9rJp5c)| [:memo: note](./notes/lecture18-hash02.md) | 2021.05.04. |
| 19 | [해시 테이블 - 성능 평가, chaining](https://youtube.com/watch?v=ghjWopXXUeA)              | [:memo: note](./notes/lecture19-hash03.md) | 2021.05.04. |
| 20 | [트리구조 소개](https://youtube.com/watch?v=w-1w4ood7Bc)                                | [:memo: note](./notes/lecture20-tree.md) | 2021.05.04. |
| 21 | [힙(heap) - 정의](https://youtube.com/watch?v=8XnPN6IB22Y)                             | [:memo: note](./notes/lecture21-heap01.md) | 2021.05.04. |
| 22 | [힙(heap) - make_heap 연산](https://youtube.com/watch?v=6VMSTOdHRfI)                   | [:memo: note](./notes/lecture22-heap02.md) | 2021.05.04. |
| 23 | [힙(heap) - insert](https://youtube.com/watch?v=gVRDc5NRjjw)                          | [:memo: note](./notes/lecture23-heap03.md) | 2021.05.04. |
| 24 | [이진트리 - 정의와 순회](https://youtube.com/watch?v=HDjqrmmpFdU)                         | [:memo: note](./notes/lecture24-binary-tree.md) | 2021.05.05. |
| 25 | [이진트리 - 이진탐색트리 정의와 탐색,삽입 연산](https://youtube.com/watch?v=Bhprzw_1kb0)       | [:memo: note](./notes/lecture25-binary-search-tree01.md) | 2021.05.05. |
| 26 | [이진트리 - 이진탐색트리 삭제 연산](https://youtube.com/watch?v=VVhmgQIJCu8)                 | [:memo: note](./notes/lecture26-binary-search-tree02.md) | 2021.05.05. |
| 27 | [균형이진탐색트리 - 정의와 회전](https://youtube.com/watch?v=Kuw0f3-E-Hw)                    | [:memo: note](./notes/lecture27-balanced-binary-search-tree01.md) | 2021.05.06. |
| 28 | [균형이진탐색트리 - AVL 트리 정의](https://youtube.com/watch?v=dHHjrl6m5CE)                 | :memo: note(준비중) | 2021.05.06. |
| 29 | [균형이진탐색트리 - AVL 삽입 연산](https://youtube.com/watch?v=KkgN2xAzmG8)                 | :memo: note(준비중) | 2021.05.06. |
| 30 | [균형이진탐색트리 - AVL 트리 삭제 연산](https://youtube.com/watch?v=W3uPlSCzAZM)             | :memo: note(준비중) | 2021.05.06. |

## 기타

- [강의 동영상 목록](https://www.youtube.com/playlist?list=PLsMufJgu5933ZkBCHS7bQTx0bncjwi4PK)의 24, 25번째 동영상은 "이진트리 - 정의와 순회"로, 동일한 강의입니다.

## 저작권 안내

이 저장소는 학습 목적으로 생성한 저장소입니다. 모든 예제 코드와 내용에 대한 저작권은 원저자에게 있습니다.
