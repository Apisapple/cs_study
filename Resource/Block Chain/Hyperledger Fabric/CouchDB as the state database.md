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

Fabric에서는 키 범위에 대한 JSON Query 문에 대해서 Pagination 기능을 지원합니다.
키의 범위를 사용하거나 JSON Query를 사용하여 페이지 지정을 지원하는 API를 사용할 경우, 페이지의 크기와 책갈피를 모두 사용할 수 있습니다.

효율적인 Pagination 기능을 사용하기 위해서는 반드시 Fabric pagination API를 사용해야만 합니다. 특히 CouchDB의 `limit` 키워드의 경우, Fabric에서 자체 pagination 기능을 지원하기 때문에 동작하지 않습니다.

만약 Pagination query API (`GetStateByRangeWithPagination()`, `GetStateByParticalCompositeKeyWithPagination()`, `GetQueryResultWithPagination()`) 를 사용하여 페이지의 크기를 지정하면, pageSize로 제한된 결과 목록이 반환됩니다. 같이 반한되는 `bookmark`는 호출하는 클라이언트로 전송될 수 있으며, 클라이언트는 `bookmark`를 사용하여 다음 Page의 결과를 받는 후속 쿼리를 실행할 수 있습니다.

Pagination API의 Query 결과는 클라이언트 Paging 요구를 지원하기 위해 만들어졌기 때문에 읽기 전용 트랜잭션에서만 사용할 수 있습니다. 읽고 쓰기가 필요로 하는  트랜잭션의 경우, Pagenation이 되지 않은 Chaincode Query API를 사용해야 합니다.

모든 Chaincode Query 문의 경우, totalQueryLimit(기본 : 100000)에 의해 제한이 됩니다.

## CouchDB indexes

CouchDB에서 index는 JSON Query를 효율적으로 수행하기 위해서 필요하며, 정렬이 있는 모든 JSON Query의 경우 필수적으로 필요로 합니다. 인덱스를 사용하면 Ledger 상에 대량의 데이터가 있는 경우에도 Chaincode에서 데이터를 확인할 수 있습니다.
Index는 Chaincode와 함께 `/META_INF/statedb/couchdb/indexes` 디렉터리에 패키지화 될 수 있습니다. 각 index는 확장자가 json인 자체 텍스트 파일에 정의가 되어야 하며, CouchDB Index JSON 구문을 따르는 JSON 형식의 인덱스 정의가 포함되어야 합니다.
JSON 형태로 정의할 때, CouchDB index JSON 문법으로 정의합니다.

```JSON
{
	"index": {
		"fields":["docType","owner"]
	},
	"ddoc":"indexOwnerDoc", 
	"name":"indexOwner",
	"type":"json"
}
```

Chaincode의 `META_INF/statedb/couchdb/indexes` 디렉터리에 있는 모든 인덱스는 배포를 위해 Chaincode와 함께 패키징이 됩니다. 패키징된 인덱스는 chiancode 패키지가 peer에 설치되거나 정의된 chaincode가 channel에 commit 될 때, peer channel과 chaincode의 특정한 DB에 배포됩니다. 체인코드를 먼저 설치한 다음 channel에 체인코드 정의를 commit 하는 경우, 인덱스는 commit 시간에 배포가 됩니다. 이미 채널에 chaincode가 정의되어 있고 이후, chaincode 패키지가 채널에 가입된 피어에 설치가 된 경우, 인덱스는 chaincode 설치 시간에 배포됩니다.

인덱스가 배포되면, Chaincode Query에서 자동으로 활용이 됩니다. CouchDB는 Query에서 사용되는 필드를 기반으로 사용할 인덱스를 자동으로 결정할 수 있습니다. 또는 selector Query에서 `use_index` 키워드를 사용하여 인덱스를 지정할 수도 있습니다.

동일한 인덱스는 설치된 Chaincode의 후속 버전에도 존재할 수 있습니다. 인덱스를 변경하려면 동일한 인덱스 이름을 사용하되 인덱스 정의를 변경하면 됩니다. 설치 및 인스턴스화 될 때는 인덱스 정의가 peer의 state DB에 다시 배포됩니다.

이미 대량의 데이터가 있는 경우, 후에 Chaincode를 설치하는 경우 설치 시 인덱스 생성에 시간이 소요될 수 있습니다. 마찬가지로 이미 대량의 데이터가 있는 경우에는 후속 Chaincode 버전의 정의를 commit하는 경우에도 인덱스 생성에 시간이 소요될 수 있습니다.
이러한 시간에 state DB를 Query하는 Chaincode 함수를 호출하지 않도록 주의해야 합니다.
인덱스가 초기화되는 동안 Chaincode Query가 Timeout될 수가 있습니다.
transaction 처리 중에는 블록이 원장에 commit되면 인덱스가 자동으로 새로 고쳐집니다.
peer가 chaincode 설치 중에 다운이 되어버릴 경우, couchdb 인덱스가 생성되지 않을 수 있습니다. 이런 경우, 인덱스를 생성하려면 Chaincode를 다시 설치해야 합니다.

## CouchDB 설정

### CouchDB를 위한 Peer 설정

CouchDB를 State DB로 활성화하려면 `goleveldb`에서 `CouchDB`로 `stateDatabase` 구성 옵션을 변경해야 합니다. 또한, `couchDBAddress`를 구성하여 피어가 사용할 `CouchDB`를 가리키도록 설정해야 합니다. `username`과 `password` 속성은 관리자의 사용자 이름과 비밀번호를 채워져야 합니다.
`couchDBConfig` section에는 추가 옵션이 제공이 됩니다. `core.yaml`에 대한 변경 사항은 peer를 다시 시작한 후, 즉시 적용이 됩니다.

#### core.yaml에 stateDatabase section 정보
```YAML
state:
  # stateDatabase - options are "goleveldb", "CouchDB"
  # goleveldb - default state database stored in goleveldb.
  # CouchDB - store state database in CouchDB
  stateDatabase: goleveldb
  # Limit on the number of records to return per query
  totalQueryLimit: 10000
  couchDBConfig:
     # It is recommended to run CouchDB on the same server as the peer, and
     # not map the CouchDB container port to a server port in docker-compose.
     # Otherwise proper security must be provided on the connection between
     # CouchDB client (on the peer) and server.
     couchDBAddress: couchdb:5984
     # This username must have read and write authority on CouchDB
     username:
     # The password is recommended to pass as an environment variable
     # during start up (e.g. LEDGER_COUCHDBCONFIG_PASSWORD).
     # If it is stored here, the file must be access control protected
     # to prevent unintended users from discovering the password.
     password:
     # Number of retries for CouchDB errors
     maxRetries: 3
     # Number of retries for CouchDB errors during peer startup
     maxRetriesOnStartup: 10
     # CouchDB request timeout (unit: duration, e.g. 20s)
     requestTimeout: 35s
     # Limit on the number of records per each CouchDB query
     # Note that chaincode queries are only bound by totalQueryLimit.
     # Internally the chaincode may execute multiple CouchDB queries,
     # each of size internalQueryLimit.
     internalQueryLimit: 1000
     # Limit on the number of records per CouchDB bulk update batch
     maxBatchUpdateSize: 1000
```
