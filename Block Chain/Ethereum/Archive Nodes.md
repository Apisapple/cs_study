---
tags:
  - BlockChain
  - Ethereum
date: 2024-03-12
---
`Archive` 노드는 전체 `node`와 `blockchain`의 모든 이전 상태와 동일한 정보를 저장합니다. 

`Archive` 노드를 실행하기 위해서는 하드웨어, 실행 비용, 기술의 전문성 및 경험에 대해서 가장 많은 투자가 필요합니다. `Archive` 노드는 `blockchain`의 데이터를 빠르고 효율적으로 구축하며, 특정 블록에 대해서 사용자의 잔고와 같은 임의의 이력 데이터를 조회하는데 유용합니다.

`Archive` 노드는 다른 일반적인 노드보다는 더 많은 공간을 필요로 하지만, 특정한 경우에는 사용할만한 가치가 있습니다.

## Archive 노드 동작 과정

Arhchive 노드는 BlockChain에 있는 모든 이력 상태를 저장합니다. Archive 노드는 기본적으로 서로 다른 시점에서 네트워크의 스냅샷을 포함해서 저장합니다.

## Archive 노드가 동기화 하는 데이터

Archive 노드는 `full sync` 를 수행하며 header, transaction, 이력을 포함하는 전체의 블록 데이터를 다운로드 합니다. Archive 노드는 download 된 모든 블록을 확인하고 모든 transaction을 다시 실행하며 모든 중간 상태를 기록합니다. 마지막 부분은 Archive 노드가 서로 다른 순간에 BlockChain의 상태에 대한 Archive를 제공하는 이유를 제공합니다.

## Archive 노드의 동기화에 소모되는 시간

Archive 노드의 동기화에 대해서 평균 추정치는 다양하지만 보통 1개월에서 3개월 정도로 예상을 합니다. Archive node는 일반적으로 full node또는 light clients와 비교하였을 때, 모든 데이터를 저장하고 있기 때문에 더 오랜 시간이 걸립니다.

- i7-2720QM CPU @ 2.20GHz
- 16 GB RAM
- SSD 860 Evo 4TB

사양이 다음과 같을 때, archive 노드 실행 정보는 다음과 같습니다.
- 6,700,000 block 동기화
- 1.5 TiB 데이터 사용
- 총 사용된 SSD : 74TiB

아래는 참고한 사이트 및 다이어그램 정보 입니다.
![sync_graph.png](https://www.palkeo.com/en/_images/sync_graph.png)
[parity_archive_node.html](https://www.palkeo.com/en/projets/ethereum/parity_archive_node.html)

## Archive 노드를 사용하는 이유

Archive 노드는 블록체인에 관한 이력 정보를 실행하기 위한 Gateway를 제공합니다. 이는 최근 128개의 블록에 포함된 데이터보다 오래된 데이터가 필요한 경우 유용하게 사용할 수 있습니다.

아래는 주요 사용처 2개의 경우입니다.

### 1. BlockChain에 대한 기록 정보

BlockChain의 과거 데이터를 수집 및 감사하는 서비스를 구축하는 경우 Arhcive 노드가 적절합니다.
BlockChain 탐색기 (Etherscan), on-chain 분석 툴(Dun Analytics) 또는 암호화폐 지갑을 구축하는 경우에 사용됩니다.
### 2. dApp 개발

dApp 프로젝트에서 오래된 BlockChain 데이터를 빠르게 확인하기 위해서는 Archive 노드를 실행해야 합니다. Archive 노드를 사용할 경우, 특정 블록 번호로 계정 잔액을 얻는 것과 같은 작업을 효과적으로 수행할 수 있습니다.