---
tags:
  - BlockChain
  - HyperLedgerBesu
date: 2024-02-27
---
`Hyperledger Besu`는 Apach 2.0 License로 개발되어 Java로 작성된 OpenSource ethreum client입니다. [[Public Network]] 과 [[Private Network]] 네트워크에서 실행이 됩니다.

Besu는 `Ethereum Network`에서 노드를 실행, 유지, 디버깅 및 모니터링을 하기 위해서 CLI 와 JSON-RPC API 를 제공합니다.

Besu는 [Hardhat](https://hardhat.org/), [Remix](http://remix.ethereum.org/) 같은 web3j 도구를 사용하여 일반적인 Smart Contract 및 Dapp 개발, 배포 및 운영을 지원합니다.

Besu는 클라이언트 내부의 키 관리를 지원하지 않습니다.
Besu와 함께 `Web3Signer`를 사용하여 Key Store를 액세스하고 Transaction에 서명을 할 수 있습니다.