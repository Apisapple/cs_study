---
tags:
  - HyperledgerFabric
  - BlockChain
date: 2024-03-21
---
# Policies

정책은 `resource` 에 관해서 신원을 확인하는 가장 기본이 되는 방식입니다.
정책은 `Signature policies`와 `ImplicitMeta policies` 정의가 가능합니다.


## Signature Policies

Signature Policies는 정책에 대해서 서명을 해야 하는 대상에 대해서 사용자의 신원을 정의합니다.

예시는 다음과 같습니다.
```yaml
Policies:
  MyPolicy:
    Type: Signature
    Rule: "OR('Org1.peer', 'Org2.peer')"
```

예시의 경우, `MyPolicy`라는 정책은 오직 `Org1.peer` 또는 `Org2.peer`의 서명에 의해서만 조건을 만족하도록 합니다.

`Signature Policies`의 경우, `AND`,`OR`, `NOutOf` 등의 논리 조합을 지원합니다.
## ImplicitMeta Policies

![Fabric Policy Hierarchy](https://hyperledger-fabric.readthedocs.io/en/latest/_images/FabricPolicyHierarchy-6.png)

`ImplicitMeta Policies`는 `Signature policies`를 조금 더 세부적으로 설정하며 최종적으로 정의되는 정책입니다.
`ImplicitMeta Policies`의 경우, `<ALL|ANY|MAJORITY> <sub_policy>` 형태의 문법을 사용합니다.

예시는 다음과 같습니다.

```yaml
Policies:
  AnotherPolicy:
    Type: ImplicitMeta
    Rule: "MAJORITY Admins"
```