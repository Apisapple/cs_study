---
tags:
  - BlockChain
  - HyperLedgerBesu
date: 2024-02-27
---
> Besu를 사용해서 `Private Network` Enterprise applications을 개발하는 것이 가능하다.

## Private Architecture

아래의 다이어그램은 Private Networks를 위한 Besu의 구조입니다.

![Besu Private Architecture](https://besu.hyperledger.org/assets/images/private-architecture-5a4d514abd93e693a77b25cacdfc9ef7.jpeg)

## System requirements

`Private network` 시스템의 경우 다음과 같은 의존성을 가지고 있습니다.
* network의 크기
* 네트워크에 전송된 transaction의 수
* Block의 가스 제한
* 노드가 처리하는 Json-RPC, PubSub 또는 GraphQL 쿼리문의 난이도와 개수

일반적으로 `Private Network`는 `Public Network`보다 네트워크의 크기가 작아 더 적은 요구사항으로 동작할 수 있습니다.

System의 요구 사항을 결정하기 위해서는 [Prometheus](https://prometheus.io/docs/introduction/overview/) 를 통해 CPU와 남은 공간 확인을 통해 모니터링 할 필요가 있습니다. 
> [Grafana](https://grafana.com/) 에서 Besu를 위해서 sample dashboard를 제공합니다.

### Java virtual Machin size
