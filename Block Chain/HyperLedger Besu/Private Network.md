---
tags:
  - BlockChain
  - HyperLedgerBesu
date: 2024-02-27
---
> Besu를 사용해서 `Private Network` Enterprise applications을 개발하는 것이 가능하다.

## Private Architecture

아래의 다이어그램은 Private Networks를 위한 Besu의 구조입니다.

![Besu Private Architecture](https://besu.hyperledger.org/assets/images/private-architecture-5a4d514abd93e693a77b25cacdfc9ef7.jpeg)

## System requirements

`Private network` 시스템의 경우 다음과 같은 의존성을 가지고 있습니다.
* network의 크기
* 네트워크에 전송된 transaction의 수
* Block의 가스 제한
* 노드가 처리하는 Json-RPC, PubSub 또는 GraphQL 쿼리문의 난이도와 개수

일반적으로 `Private Network`는 `Public Network`보다 네트워크의 크기가 작아 더 적은 요구사항으로 동작할 수 있습니다.

System의 요구 사항을 결정하기 위해서는 [Prometheus](https://prometheus.io/docs/introduction/overview/) 를 통해 CPU와 남은 공간 확인을 통해 모니터링 할 필요가 있습니다. 
> [Grafana](https://grafana.com/) 에서 Besu를 위해서 sample dashboard를 제공합니다.

## Java virtual Machin size

최소 `4GB` 메모리를 가지고 있는 JVM이 필요하며 network 환경에 따라서 형태가 달라질 수 있습니다.

## VM 요구 사항

VirtualBox 같은 Local 형태의 VM 환경을 운영할 경우 다음과 같은 설정이 필요합니다.

* BIOS의 설정에서 Intel Virtualization Technology(VTX) 및   
  Virtualization Technology for Directed I/O(VT-d)를 사용하도록 설정해야 합니다.

* Windows의 경우 `Hypre-V`를 사용하지 않도록 설정을 해야 할 수 있습니다.

Virtual Machine의 다음과 같은 설정을 추천합니다.

* Memory Size : 6GB
* Disk의 최소 크기 : 10GB
* Virtual hard disk file type : VDI


## 설치 옵션

* Docker image
* Binaries
* from Source Code

#### Docker image 설치 방법

##### Expose Ports

P2P discovery, GraphQL, Metrics, HTTP, WebSocket JSON-RPC 등을 위해서 다음과 같은 port를 expose 해줘야 합니다. 
```bash
docker run -p <localportJSON-RPC>:8545 -p <localportWS>:8546 -p <localportP2P>:30303 hyperledger/besu:latest --rpc-http-enabled --rpc-ws-enabled
```

```bash
docker run -p 8545:8545 -p 13001:30303 hyperledger/besu:latest --rpc-http-enabled
```


### Start Besu

`besu` 명령을 이용해서 node를 실행할 수 있습니다.
만약 실행하는 과정에서 이전에 연결된 네트워크가 아닌 다른 네트워크와 연결을 할 경우,
기존에 있는 Local의 블록 데이터를 삭제하거나 `--data-path` 옵션을 사용하여 다른 데이터 저장 경로를 지정해야 합니다.
Local의 블록 데이터를 삭제하고자 할 경우, `besu/build/distribution/besu-<version>` diredtory의 `database` diredtory를 삭제하면 됩니다.

#### Genesis configuration

`genesis file`을 통해서 설정을 할 수 있습니다. `--genesis-file` 옵션을 활용하여 설정할 수 있습니다.
```json
{
  "config": {
    "chainId": 48122,
    "berlinblock": 0,
    "clique": {
      "blockperiodseconds": 1,
      "epoch": 30000
    }
  },
  "nonce": "0x0",
  "timestamp": "0x5ca916c6",
  "extraData": "0x0000000000000000000000000000000000000000000000000000000000000000c0A8e4D217eB85b812aeb1226fAb6F588943C2C20000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000",
  "gasLimit": "0x47b760",
  "difficulty": "0x1",
  "mixHash": "0x0000000000000000000000000000000000000000000000000000000000000000",
  "coinbase": "0xc0A8e4D217eB85b812aeb1226fAb6F588943C2C2",
  "number": "0x0",
  "gasUsed": "0x0",
  "parentHash": "0x0000000000000000000000000000000000000000000000000000000000000000",
  "alloc": {
    "0xc0A8e4D217eB85b812aeb1226fAb6F588943C2C2": {
      "balance": "0x200000000000000000000000000000000000000000000000000000000000000"
    },
    "0xD1cf9D73a91DE6630c2bb068Ba5fDdF9F0DEac09": {
      "balance": "0x200000000000000000000000000000000000000000000000000000000000000",
      "privatekey": "0x797c13f7235c627f6bd013dc17fff4c12213ab49abcf091f77c83f16db10e90b",
      "derivation": "m/44'/60'/0'/0/0"
    },
    "0xd826E703658FA2CE8D1018D42E637C08d9846A17": {
      "balance": "0x200000000000000000000000000000000000000000000000000000000000000",
      "privatekey": "0x4be84b298ccb944e96befc4f03b943ec13709f6a8e5b5d8595c486dfa88fd254",
      "derivation": "m/44'/60'/1'/0/0"
    },
    "0x247DdfA00415710E0416f8c103b5E6428782C916": {
      "balance": "0x200000000000000000000000000000000000000000000000000000000000000",
      "privatekey": "0xaa682edca26f3e17889d69276e6c6a4fcf1594af97e48f4dc3ac6dbb29e7924b",
      "derivation": "m/44'/60'/2'/0/0"
    },
    "0x500a8704F86C0d9126Dfb949fDC4dc248c228fB4": {
      "balance": "0x200000000000000000000000000000000000000000000000000000000000000",
      "privatekey": "0x45d09c64e4973b16422b31d5e4a1fbf57ae8fd25037566af8bc1d046022d754b",
      "derivation": "m/44'/60'/3'/0/0"
    },
    "0x32d9ad8F398995fFF658E74430749d65E0ee6702": {
      "balance": "0x200000000000000000000000000000000000000000000000000000000000000",
      "privatekey": "0x2f51f2d881e0a6f7f249139a2afe8da084424616d08aa0ce9fb1c960b49f022f",
      "derivation": "m/44'/60'/4'/0/0"
    },
    "0xd32d3f6dA1664C4ee7acae64fEC3661cEa6ee448": {
      "balance": "0x200000000000000000000000000000000000000000000000000000000000000",
      "privatekey": "0x87abeb4c0230ca6fdf42f7d2cb2baa510856e42f039ab7670b13845e45dc3245",
      "derivation": "m/44'/60'/5'/0/0"
    },
    "0x5F6C5F2431CE84f2Fa84deB6B27A1764DB6feB1a": {
      "balance": "0x200000000000000000000000000000000000000000000000000000000000000",
      "privatekey": "0x5f0ad910e681553c9407582f620d9560541fa8b8c4d03e9e2e3caed5eea6a220",
      "derivation": "m/44'/60'/6'/0/0"
    },
    "0x9fCDe74bf5465D5C32a09f158047803a061B3C1B": {
      "balance": "0x200000000000000000000000000000000000000000000000000000000000000",
      "privatekey": "0x76930906e95c96a9be735b0f182184424f450feca5ea71bf743a8c47ea6e2635",
      "derivation": "m/44'/60'/7'/0/0"
    },
    "0xb582703c0a0e2b598f9362A5e5c17Ab6865b0342": {
      "balance": "0x200000000000000000000000000000000000000000000000000000000000000",
      "privatekey": "0x32e90654e141cb4f92dd9fccef100778c112636b20b9017a9ae56be9a8c2c648",
      "derivation": "m/44'/60'/8'/0/0"
    },
    "0x179740E29B1E7b2C61F6004b8d5caD575D6eaa88": {
      "balance": "0x200000000000000000000000000000000000000000000000000000000000000",
      "privatekey": "0x028bf0ee2807cf9a8d22db99f12aea783a2e6b4897c9ddb7557e33291c7d35c5",
      "derivation": "m/44'/60'/9'/0/0"
    }
  }
}
```


#### Transaction nonces

Besu는 `eth_getTransactionCount`를 이용하여 다음 transaction의 nonce를 얻습니다. nonce의 값은 `transaction pool`에 있는 transaction에 의존하여 정해집니다.


### 합의 프로토콜

- QBFT
	- enterprise 급의 네트워크에서 추천되는 프로토콜
- IBFT 2.0
- Clique
- Proof of stake
- Ethash

각각의 설정은 `config` 파일 내부에서 설정할 수 있습니다.
```json
{  
"config": {  
...  
"ethash": {  
...  
}  
},  
...  
}

```


#### QBFT 합의 알고리즘 설정 방법

Hyperledger Besu는 QBFT 권한 증명(POA) 합의 프로토콜을 사용할 수 있습니다.

QBFT 네트워크에서는 검증하기 위해서 알려진 계정이 transaction과 block을 검증합니다. 검증하는 교대로 블록을 만듭니다. 블록을 BlockChain에 입력하기 전에 2/3 이상의 검증자가 먼저 블록에 서명을 해야 합니다.

설정하는 방법은 `genesis file`을 통해서 설정하는 것이 가능합니다.

```json
{
  "config": {
    "chainid": 1337,
    "berlinBlock": 0,
    "qbft": {
      "epochlength": 30000,
      "blockperiodseconds": 5,
      "requesttimeoutseconds": 10
    }
  },
  "nonce": "0x0",
  "timestamp": "0x5b3d92d7",
  "extraData": "0xf87aa00000000000000000000000000000000000000000000000000000000000000000f8549464a702e6263b7297a96638cac6ae65e6541f4169943923390ad55e90c237593b3b0e401f3b08a0318594aefdb9a738c9f433e5b6b212a6d62f6370c2f69294c7eeb9a4e00ce683cf93039b212648e01c6c6b78c080c0",
  "gasLimit": "0x29b92700",
  "difficulty": "0x1",
  "mixHash": "0x63746963616c2062797a616e74696e65206661756c7420746f6c6572616e6365",
  "coinbase": "0x0000000000000000000000000000000000000000",
  "alloc": {
    "64d9be4177f418bcf4e56adad85f33e3a64efe22": {
      "balance": "0x446c3b15f9926687d2c40534fdb564000000000000"
    },
    "9f66f8a0f0a6537e4a36aa1799673ea7ae97a166": {
      "balance": "0x446c3b15f9926687d2c40534fdb564000000000000"
    },
    "a7f25969fb6f3d5ac09a88862c90b5ff664557a7": {
      "balance": "0x446c3b15f9926687d2c40534fdb564000000000000"
    },
    "f4bbfd32c11c9d63e9b4c77bb225810f840342df": {
      "balance": "0x446c3b15f9926687d2c40534fdb564000000000000"
    }
  },
  "number": "0x0",
  "gasUsed": "0x0",
  "parentHash": "0x0000000000000000000000000000000000000000000000000000000000000000"
}
```

QBFT 설정 정보
- `blockperiodseconds` - 최소 block 시간, 단위 초.
- `epochlength` - 모든 표를 다시 설정할 이후의 블록 수.
- `requesttimeoutseconds` - 각 합의 알고리즘이 시작 전, 변경하는데 걸리는 시간. 단위 초.
- `blockreward` - 보상에 대한 값을 설정. 기본 값은 0으로 설정. 만약 설정하게 될 경우, 
			  다른 모든 노드도 같은 값으로 설정을 해야 합니다.
- `validatorcontractaddress` - smart contract 검증자의 address 정보. 
						contract 검증자 선택을 사용하는 경우에만 필요로 합니다.
						주소값은 할당 섹션의 주소와 동일한 값을 가져야 합니다.
- `miningbeneficiary` - block 생성에서의 마이닝 비용
