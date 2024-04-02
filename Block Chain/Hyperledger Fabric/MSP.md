---
tags:
  - HyperledgerFabric
date: 2024-03-28
---
# Membership Service Providers (MSP)

MSP(Membership Service Providers)는 Fabric 네트워크 참가자의 신원과 액세스 제어를 관리하는 역할을 담당합니다.

## MSP 구성 요소

- 신원(Identity)
	- 네트워크 참가자의 이름 및 역할과 같은 신원 속성을 정의합니다. 네트워크에 권한이 있는 당사자만이 네트워크에 접근할 수 있도록 보장하며, 네트워크의 무결성을 유지하는데 필수적인 요소입니다.

- 등록(Enrollment)
	- 네트워크에 새로운 참가자를 등록하고, 새로운 참가자들에게 암호화 키를 생성하는 과정을 처리합니다. 디지털 신원 생성과 네트워크 참가자의 신원을 검증하는 
	  과정을 포함합니다.

- 루트 인증서(Root Certificates)
	- MSP와 네트워크 참가자 간의 신뢰를 확립하는데 사용됩니다. 네트워크 참가자의 인증서를 서명하고 발급하는 루트 인증 기관(CA)의 공개 키와 이름을 포함합니다.

- 중간 인증서(Intermediate Certificates)
	- MSP의 계층 형태의 신뢰 구조를 관리하는 데 사용됩니다. 신뢰의 위임을 허용하고 네트워크 참가자의 액세스 제어 수준을 정의합니다.

## Reference

- https://www.linkedin.com/pulse/understanding-hyperledger-fabric-membership-service
- https://hyperledger-fabric.readthedocs.io/en/latest/msp.html
- https://hyperledger-fabric.readthedocs.io/en/latest/membership/membership.html