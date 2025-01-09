---
tags:
  - BlockChain
  - HyperledgerFabric
date: 2024-03-20
---
# Chaincode Access Control

## 접근 제어

Chaincode는 클라이언트의 접근을 제어하기 위해서 인증서를 활용할 수 있습니다.
Chaincode에서는 `ctx.GetStub().GetCreator()` API 활용을 통해 인증서를 확인할 수 있습니다.
또한, Fabric Contract API에서 확장 API를 제공하여, 클라이언트 신원, 조직 신원 또는 인증서의 OU나 사용자 지정 속성과 같은 클라이언트 신원 속성에 기반한 액세스 제어 결정을 할 수 있습니다.

예를 들어, Ledger 상에서 Key와 Value로 표현되는 Ledger는 가치의 일부로서 클라이언트의 정체성을 표현할 수 있습니다. 저장되는 Value의 값은 Json 형식일 수 있으며 Json 속성 중 하나는 Ledger의 소유자에 대한 속성일 수 있습니다. 그러면 Chaincode의 논리 연산은 Ledger의 소유자만이 향후 자신의 Key Value 데이터를 업데이트할 권한을 가지게 할 수 있습니다.

### Client Identity Chaincode Library?

클라이언트 Chaincode 라이브러리를 사용하면, 클라이언트의 Identity를 기반으로 Access 제어 기능을 구현할 수 있습니다. 다음과 같은 데이터를 참고할 수 있습니다.

* 클라이언트의 MSP ID
* 클라이언트 ID와 관련된 속성
* 클라이언트 ID와 관련된 OU(Organizational Unit) 값

속성은 단순히 ID와 연관된 이름과 값의 쌍으로 이루어집니다. 예를 들어, `email=me@gmail.com`은 ID가 `email` 값이 `me@gmail.com`속성을 가지고 있습니다.

### Client Identity Chaincode Library 사용법

> [!info] client identity chaincode library 사용법에 대해서 정리합니다.

모든 예시 코드는 다음과 같은 2가지를 가정한 상태입니다.

1. Chaincode에서 `ChaincodeStubInterface`의 stub 값을 받은 상태
2. 다음과 같은 import가 되어있는 상태
```go
import "github.com/hyperledger/fabric-chaincode-go/pkg/cid"
```

#### 클라이언트 ID 가져오기
```go
id, err := cid.GetID(stub)
```

#### MSP ID 가져오기
```go
mspid, err := cid.GetMSPID(stub)
```

#### Attribute 값 가져오기
```go
val, ok, err := cid.GetAttributeValue(stub, "attr1")
if err != nil {
   // There was an error trying to retrieve the attribute
}
if !ok {
   // The client identity does not possess the attribute
}
// Do something with the value of 'val'
```

#### Attribute 값 확인
```go
err := cid.AssertAttributeValue(stub, "myapp.admin", "true")
if err != nil {
   // Return an error
}
```

#### 특정 OU값 확인하기
```go
found, err := cid.HasOUValue(stub, "myapp.admin")
if err != nil {
   // Return an error
}
if !found {
   // The client identity is not part of the Organizational Unit
   // Return an error
}
```

#### 클라이언트의 X509 인증서 가져오기
```go
cert, err := cid.GetX509Certificate(stub)
```


## 참고
- [chaincode-access-control](https://hyperledger-fabric.readthedocs.io/en/latest/chaincode4ade.html#chaincode-access-control)
- [Client Identity Chaincode Library](https://github.com/hyperledger/fabric-chaincode-go/blob/main/pkg/cid/README.md)