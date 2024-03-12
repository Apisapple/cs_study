---
tags:
  - BlockChain
  - Ethereum
date: 2024-03-12
---
Full Node는 각 블록에 대한 검증 및 블록의 상태 데이터를 다운로드 하는 기능을 합니다.

Full Node의 경우 검증이 시작되는 위치에 상관없이 전체 블록 데이터 중, 최근 128개의 블록만 보관합니다. 이로 인해 공간 절약이 가능합니다. 만약 이전 데이터가 필요할 경우, 재생성을 통해서 구할 수 있습니다.

## REFERENCE
* [nodes-and-clients](https://ethereum.org/en/developers/docs/nodes-and-clients/)