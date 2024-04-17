---
tags:
  - HyperledgerFabric
date: 2024-04-17
---
# CouchDB as the state database

## Chaincode queries

대부분의 Chaincode는 `GetState`, `PutState`, `GetStateByPartialCompositeKey` 등의 shim API를 통해서 LevelDB 또는 CouchDB 에 사용할 수 있습니다. 만약 StateDB로 CouchDB를 사용하고 Chaincode에서 ledger를 JSON으로 모델링한 경우, CouchDB에서 사용하는 JSON 쿼리 문자열을 사용할 수 있습니다.

쿼리에 대한 응답은 Ledger 상에 데이터를 JSON 데이터 형태로 응답합니다.
하지만, JSON 쿼리의 결과 값이 Chaincode 실행에 대해서 Commit 시간 사이에 변형이 없을 것이라는 보장은 없습니다. 이러한 문제로, JSON 쿼리를 사용하여 channel 원장을 업데이트 하는 단일 트랜잭션에서는 사용하지 않는 것이 좋습니다.

예를 들어 `Alice`가 소유한 Ledger 데이터에 대한 JSON 쿼리를 수행하고 이를 BOB에게 이전하는 경우, Chaincode 실행 시간과 commit 시간 사이에 다른 트랜잭션에 의해서 `Alice`에게 ledger 데이터의 변형이 있을 수 있습니다.

## CouchDB Pagination


## CouchDB indexes
