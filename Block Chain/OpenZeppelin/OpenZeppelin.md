---
tags:
  - Solidity
  - BlockChain
  - OpenZeppelin
date: 2024-11-07
---

## Install & Usage

### installation

#### Hardhat(npm)
```Shell
npm install @openzeppelin/contracts
```


### Usage

``` solidity

// contracts/MyNFT.sol
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

import {ERC721} from "@openzeppelin/contracts/token/ERC721/ERC721.sol";

contract MyNFT is ERC721 {
    constructor() ERC721("MyNFT", "MNFT") {}
}

```


## Linked for development smart contract

[[OpenZeppelin Access Control]]