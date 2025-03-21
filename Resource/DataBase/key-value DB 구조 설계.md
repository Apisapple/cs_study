---
tags:
  - database
date: 2025-03-20
---
## 기본 개념

- key-value 쌍
	- `key`는 고유한 식별자
	- `value`는 간단한 scala 값이나 복잡한 데이터 구조
- key는 유일한 값이어야 하며, 일반적으로 짧을수록 성능이 향상

## 설계 방안

### 단일 서버 저장소 설계

#### 메모리 기반 해시 테이블
- 모든 데이터를 메모리에 저장하여 빠른 접근 속도를 제공
- 데이터가 너무 많은 경우, 메모리 제한이 발생할 수 있음

#### 디스크 사용
- 자주 사용하지 않는 데이터는 디스크에 저장하여 메모리 효율성을 높일 수 있음

### 분산 저장소 설계

#### [[CAP 정리]]
- 데이터 일관성, 가용성, 파티션 감내 중 두 가지를 선택해야 함.
- 일반적으로 파티션 감내는 필수적이므로, 일관성과 가용성 중 하나를 선택해서 진행해야 함.

### 데이터 일관성 모델

- 강한 일관성
	- 모든 사본에 쓰기 연산 결과가 반영될 때까지 읽기 / 쓰기를 금지
	- 이는 고가용성 시스템에는 적합하지 않음
- 최종 일관성
	- 쓰기 연산 후 일정 시간이 지나면 모든 사본이 일관성을 가지게 됨.
	- 대부분의 key-value에서 사용

## 장애 감지 및 복구

### 가십 프로토콜
- 분산형 장애 감지 솔루션으로, 노드 간의 상태를 주기적으로 공유하여 장애를 감지