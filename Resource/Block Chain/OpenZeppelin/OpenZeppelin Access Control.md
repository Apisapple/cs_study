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

`onlyRole` 수정자를 이용하여, 다양한 형태의 역할을 부여할 수 있습니다.
### AccessControl 사용하기
``` solidity title:ERC20_토큰_기반의_간단한_예시_코드
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

import {AccessControl} from "@openzeppelin/contracts/access/AccessControl.sol";
import {ERC20} from "@openzeppelin/contracts/token/ERC20/ERC20.sol";

contract AccessControlERC20MintBase is ERC20, AccessControl {
    // Create a new role identifier for the minter role
    bytes32 public constant MINTER_ROLE = keccak256("MINTER_ROLE");

    error CallerNotMinter(address caller);

    constructor(address minter) ERC20("MyToken", "TKN") {
        // Grant the minter role to a specified account
        _grantRole(MINTER_ROLE, minter);
    }

    function mint(address to, uint256 amount) public {
        // Check that the calling account has the minter role
        if (!hasRole(MINTER_ROLE, msg.sender)) {
            revert CallerNotMinter(msg.sender);
        }
        _mint(to, amount);
    }
}
```

`AccessControle` Contract는 역할 기반의 확장된 접근 제어를 제공합니다.
`AccessControle` Contract를 활용하면, `Ownerable` 과 비교하여 좀 더 세부적인 권한을 정의하여 구현할 수 있습니다.
## Delayed Operation



## Access Management

