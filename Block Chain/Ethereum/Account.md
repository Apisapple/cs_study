---
tags:
  - BlockChain
  - Ethereum
date: 2024-03-08
---
## Ethereum에서의 Account

`Ethereum`에서의 계정은 `Ethereum` 네트워크에서 거래를 보낼 수 있는 `Ethereum`(ETH) 잔액을 가진 대상을 말합니다. 계정은 사용자가 제어하거나 스마트 컨트랙트를 배포할 수 있습니다.

`Ethereum`에서는 2가지 타입의 계정이 존재합니다.

### Ethereum의 Account 종류

- Externally-owned account (EOA)
    
    - 누구나 개인키로 컨트롤을 할 수 있는 계정
        
- Contract account
    
    - 네트워크에 배포된 컨트랙트를 의미합니다. 소스코드를 기반으로 통제가 가능한 계정을 말합니다.
        

두 개의 Account는 모두 ETH 토큰을 소유하거나 보낼 수 있으며, 배포된 contract와 상호작용 하는 것이 가능합니다.

|            | EOA               | Contract                                |
| ---------- | ----------------- | --------------------------------------- |
| 생성 비용      | 생성 비용 없음          | network 저장 공간 사용으로 비용 발생                |
| 트랜잭션       | transaction 시작 가능 | 수신한 transaction에 대한 응답 가능               |
| ETH 전송     | 다른 EOA와 통신만 가능    | trigger code를 활용하여 다른 Contract, EOA와 통신 |
| KeyPair 소유 | Key Pair 소유       | Key Pair를 소유하지 않음                       |
