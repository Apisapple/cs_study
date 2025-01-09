---
tags:
  - HyperledgerFabric
  - BlockChain
date: 2024-03-21
---
# Resources

Hyperledger Fabric은 `chaincode`, `system-chaincode`, `events-streamsource`으로 상호작용을 합니다. `chaincod`, `system-chaincod` 같이 서로 상호작용을 하기 위한 포인트가 `resource`를 의미합니다. 
application 개발자는 어떤 `resource`가 제공이 되는지 알아야 하며, 그에 따른 정책도 알아야 합니다. 이러한 정책 부분은 `configtx.yaml`에  `<component>/<resource>` 형태로 명시되게 됩니다.
예를 들면, `cscc/GetConfigBlock` 형태는 `cscc` component의 `GetConfigBlock`resource가 있습니다. 