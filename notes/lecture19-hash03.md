# 해시 테이블

> 본 포스팅은 한국외대 컴퓨터공학부 신찬수 교수님의 "[자료구조 - Data Structures with Python](https://www.youtube.com/playlist?list=PLsMufJgu5933ZkBCHS7bQTx0bncjwi4PK)" 중 19강 "[해시 테이블](https://youtube.com/watch?v=ghjWopXXUeA)" 강의를 정리한 노트입니다.

## Open addressing

- linear probing: 해시 충돌시 한칸씩 내려가는 방식
- quadratic probing: k + 1<sup>2</sup>, k + 2<sup>2</sup>, k + 3<sup>2</sup> 순으로 내려가는 방식. remove 함수가 복잡해진다.
- double hashing: 해시 함수를 두 개 쓰는 방식. f(key) -> f(key) + g(key) -> f(key) + 2g(key).. 순으로 내려간다.

## 성능 평가

- set, remove, search: 클러스터 사이즈의 영향을 직접적으로 받는다. 클러스터 사이즈는 해시 함순 충돌 해결 방식에 영향을 받는다. 또한, 로드 팩터(load factor)의 영향도 받는다.

로드 팩터 확인

- load factor: n / m (M: |H|=slot갯수, n: H에 저장된 item 갯수)
- 0 <= n/m < 1
- load factor가 1에 가까울수록 더 많은 연산이 필요하다.

충돌 비율 확인

- (collision 횟수) / n = 충돌 비율

오픈 어드레싱 방식은 평균적으로 `m >= 2n`(최소 50% 이상 빈 슬롯이라면) 데이터 이사비용을 합치더라도 클러스터의 평균 사이즈가 O(1)이 되도록 유지할 수 있다.

## Chaining

하나의 슬롯에 여러 개의 아이템을 저장하는 방식. 각 슬롯에 한방향 연결리스트를 만든다. 꼭 한방향일 필요는 없다.

`set` 함수가 항상 O(1) 시간 보장. `search`, `remove` 함수는 각 슬롯내의 노드 갯수만큼 O(n) 시간. O(충돌 key의 평균 갯수)

c-universal 해시 함수를 사용하면 `set`, `search`, `remove`가 O(1). C-universal 해시 함수는 c/n만큼의 충돌을 보장하는 함수.

## 결론

해시 함수는 C-universal을 쓰고 충분한 로드 팩터를 확보하면 상수시간 내에 `set`, `remove`, `search`를 수행할 수 있다.
