---
tags:
  - BlockChain
  - Ethereum
  - OpenZeppelin
date: 2024-11-07
---
## Ownership & Ownable

> [!info]
> Contract에 대한 소유권 관리에 대한 기능 설정

```solidity title:example_code(ownable)
// SPDX-License-Identifier: MIT

pragma solidity ^0.8.20;

import {Ownable} from "@openzeppelin/contracts/access/Ownable.sol";

contract MyContract is Ownable {
    constructor(address initialOwner) Ownable(initialOwner) {}

    function normalThing() public {
        // anyone can call this normalThing()
    }

    function specialThing() public onlyOwner {
        // only the owner can call specialThing()!
    }
}
```

Ownable을 활용하여 간단하고 효과적으로 접근 제어를 구현할 수 있습니다.

근본적으로 Ownable을 활용하면 계정의 소유권을 이전하지 못하는 위험을 염두하고 있어야 하지만, `Ownable2Step` 이나 `acceptOwnership` 등의 기능을 활용하여 소유권의 이전 및 확장성을 구현할 수 있습니다.

예시 및 참고 내용
- [Gnosis Safe](https://safe.global/)
- [Aragon DAO](https://aragon.org/)
- [Maker DAO](https://makerdao.com/ko/)
## Role 기반의 Access Control




## Delayed Operation



## Access Management

