---
tags:
  - BlockChain
  - HyperLedgerBesu
date: 2024-02-29
---
## Besu에서 Free gas 설정 과정
### Free gas network 설정

transaction은 기본적으로 resource를 사용하므로 관련 비용인 `gas`가 발생합니다. 
`gas`의 총 비용은 아래와 같이 계산이 됩니다.
$$
Cost Gas = Gas Used * GasPrice
$$

> Free gas network를 사용하기 위해서는 모든 node에서 최소 gas의 가격이 zero로 설정이 되어야 합니다. 만약 어떤 노드가 설정을 0보다 큰 값을 설정할 경우, 거래가 중단이 될 수 있습니다.


#### 1. Block Size 설정

`genesis` 파일에서 block size의 제한을 `0x1fffffffffffff`로 설정합니다. 

```json
{  
"config": {  
....  
},  
...  
"gasLimit": "0x1fffffffffffff",  
....  
}

```
#### 2. Contract Size 설정
`config`에서 `contractSizeLimit`의 사이즈를 최대 사이즈로 설정합니다.

```json
(  
"config": {  
...  
"contractSizeLimit": 2147483647,  
...  
}  
...  
}
```

#### 3. Besu 실행

노드를 실행할 때, `--min-gas-price=0` 옵션을 추가하여 Besu 노드 실행