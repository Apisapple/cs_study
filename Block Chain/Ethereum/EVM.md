---
tags:
  - BlockChain
  - Ethereum
date: 2024-03-12
---
# EVM

----
## EVM 정의

Ethereum Virtual Machine(EVM)은 Ethereum 네트워크를 구성하는 Client를 실행하고 있는 수천 개의 연결된 컴퓨터에 의해서 유지되는 하나의 단일 개체를 의미합니다.

Ethereum 프로토콜은 EVM이 중단되지 않고 지속적으로 불변하는 작동을 유지하기 위한 목적으로 존재합니다. BlockChain의 상태는 언제나 하나의 정규 상태를 가지며, EVM은 블록에서 블록으로 새로운 유효 상태를 계산하는 규칙을 정의합니다.

---
## Ethereum의 상태 

Ethereum은 `SmartContract`를 기반으로 각 노드에 분산 [유한 상태 머신](https://ko.wikipedia.org/wiki/%EC%9C%A0%ED%95%9C_%EC%83%81%ED%83%9C_%EA%B8%B0%EA%B3%84) 데이터로 볼 수 있습니다. Ethereum의 상태는 계정, 잔액, 기계 상태를 보유하고 있는 대규모 데이터 구조로서 미리 정의된 규칙에 다라서 블록에서 블록으로 변경할 수 있고 임의의 코드를 실행할 수 있습니다. 블록에서 블록으로 상태를 변경하는 규칙은 EVM에 의해서 정의를 합니다.

![EVM](https://ethereum.org/content/developers/docs/evm/evm.png)

### Ethereum의 상태 전이 함수

EVM은 입력이 주어지게 되면 결정론적인 출력을 생성합니다. 
$$
Y(S , T) = S'
$$
기존에 검증된 S와 새로 검증된 Transaction (T)을 Ethereum 상태 transation 기능 **Y(S, T)** 에 넣어 새로운 형태 S'을 생성합니다.

#### State

Ethereum의 맥락에서, State는 [Modified Merkle Patricia Trie](https://ethereum.org/en/developers/docs/data-structures-and-encoding/patricia-merkle-trie/) 라고 불리는 구조의 모든 계정의 Hash로 연결된 하나의 Single root hash 유지하고 있습니다.
#### Transactions

Transaction은 계정에서 암호로 서명된 데이터 입니다. Transaction은 호출된 메시지의 결과가 담겨 있는 transaction과 contract의 결과가 담겨있는 2가지 타입의 종류가 있습니다.
Contract는 `smart contract`의 bytecode가 포함된 새로운 contract 계정이 생성됩니다. 다른 계정이 해당 계약으로 메시지를 호출할 때마다 해당하는 바이트 코드를 실행합니다.

