---
tags:
  - BlockChain
  - HyperLedgerBesu
date: 2024-02-29
---

## 타원 곡선 설정

### 지원 알고리즘 목록
- secp256k1
- secp256r1

### 설정 방법
`genesis` 파일에서 `ecCurve`의 설정을 다음과 같이 설정
```json
{  
"genesis": {  
"config": {  
"ecCurve": "secp256k1",  
[...]  
},  
[...]  
}
```
