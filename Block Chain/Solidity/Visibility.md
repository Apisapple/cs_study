---
tags:
  - BlockChain
  - "#Solidity"
date: 2024-06-29
---
# Visibility

## Visibility의 종류

`Solidity`에서는 다음과 같은 4가지 종류의 접근 제어자를 사용할 수 있다.

- external
	- 외부의 Contract나 주소에서만 접근 가능
- public
	- 어느 곳에서나 접근이 가능
- internal
	-  `private`처럼 internal 정의된 내부에서 접근 가능, 상속을 받은 Contract들도 접근 가능
- private
	- 내부에서만 접근 가능


## Interface

자식 Contract 위한 틀로서, 모든 함수는 추상 함수로만 구성이 되어야 한다.
Interfae는 다음과 같은 특징을 가지고 있다.

### Interface 특징

- 구체적으로 정의된 함수를 선언할 수 없다.
- 다른 인터페이스에 상속이 가능하다.
- 선언되는 함수는 모두 `external` 이어야 한다.
- 상태 변수를 선언할 수 없다.
- 생성자를 선언할 수 없다.

### 예시 코드

``` solidity

// SPDX-License-Identifier: MIT
pragma solidity ^0.8.24;

contract Counter {
    uint256 public count;

    function increment() external {
        count += 1;
    }
}

interface ICounter {
    function count() external view returns (uint256);

    function increment() external;
}

contract MyContract {
    function incrementCounter(address _counter) external {
        ICounter(_counter).increment();
    }

    function getCount(address _counter) external view returns (uint256) {
        return ICounter(_counter).count();
    }
}

// Uniswap example
interface UniswapV2Factory {
    function getPair(address tokenA, address tokenB)
        external
        view
        returns (address pair);
}

interface UniswapV2Pair {
    function getReserves()
        external
        view
        returns (uint112 reserve0, uint112 reserve1, uint32 blockTimestampLast);
}

contract UniswapExample {
    address private factory = 0x5C69bEe701ef814a2B6a3EDD4B1652CB9cc5aA6f;
    address private dai = 0x6B175474E89094C44Da98b954EedeAC495271d0F;
    address private weth = 0xC02aaA39b223FE8D0A0e5C4F27eAD9083C756Cc2;

    function getTokenReserves() external view returns (uint256, uint256) {
        address pair = UniswapV2Factory(factory).getPair(dai, weth);
        (uint256 reserve0, uint256 reserve1,) =
            UniswapV2Pair(pair).getReserves();
        return (reserve0, reserve1);
    }
}

```

