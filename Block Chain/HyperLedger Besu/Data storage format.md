
## 데이터 저장 형태 유형

- [Forest](#forest)

- [Bonsai](#bonsai)

### Forest

`forest mode` 라고 불리며, 기본이 되는 저장 형태
forest mode에서는 각 노드는 `key-value` 형태로 hash 값을 저장

#### forest 저장 방식 특징

- Merkle Partricia Tries(MPT) 기반
	- Forest는 Ethereum의 상태 트리를 **Merkle Patricia Trie**로 관리
	- 트리는 노드 단위로 저장되며, 노드 간의 참조가 해시

#### forest 이점

- 트리의 구조는 상태 데이터의 증명 및 검증에 용이
- BlockChain에서 **State Proof**를 제공할 수 있는 기본 구조
- 모든 노드와 데이터를 저장하므로 전체 블록체인 상태를 완벽히 재구성할 수 있음
#### forest 단점

- 노드가 많아질수록 읽기 / 쓰기 성능이 느려질 수 있음
- 디스크의 공간을 많이 차지함.
- 데이터가 조각화가 될 수 있는 경향이 있음
- 불필요한 중복 데이터가 발생할 수 있음.

### Bonsai

Hyperledger Besu의 새로운 데이터 저장소 형식으로 공간 효율성을 극대화하고 빠른 동기화를 지원

#### Bonsai 저장 방식의 특징

- Flat Database 구조
	- Bonsai 트리 구조는 데이터를 압축하여 저장
		- archive node의 forest mode에서는 약 12TB를 사용하는 반면, 
		  bonsai는 1100GB를 사용
	- 최신 상태 데이터만 저장이 가능하며, 과거 상태 데이터는 별도로 관리

- Key-Value 기반
	- 상태 데이터는 Key-Value 쌍으로 저장되며, 상태를 업데이트할 때마다 값만 갱신
	- 이 접근 방식은 최신 상태를 빠르게 액세스할 수 있도록 설계

#### Bonsai 이점

- Forest와 비교하여 디스크 공간 사용이 효율적
- 읽기 / 쓰기 성능의 개선
- 최신 상태를 저장하기 때문에 빠른 동기화가 가능

#### Bonsai 단점
- 과거 상태 데이터를 복구하거나 증명하기가 어려울 수 있음
- State Proof가 필요한 환경에서는 Forest에 비해 제한적인 상황


### Forest와 Bonsai 비교
| **특징**             | **Forest**           | **Bonsai**                           |
| ------------------ | -------------------- | ------------------------------------ |
| **구조**             | Merkle Patricia Trie | Flat Database with Key-Value storage |
| **성능**             | 상대적으로 느림             | 빠른 읽기/쓰기                             |
| **디스크 공간**         | 많이 사용 (비효율적)         | 적게 사용 (효율적)                          |
| **동기화 속도**         | 느림                   | 빠름                                   |
| **State Proof 지원** | 가능                   | 제한적                                  |
| **과거 상태 관리**       | 완전한 과거 상태 보존         | 최신 상태만 보존, 별도 관리 필요                  |


### 결론

- **Bonsai**는 더 나은 성능과 공간 효율성을 제공하며, 빠른 동기화와 최신 상태 관리를 우선시하는 환경에서 유용
- **Forest**는 완전한 상태 데이터 보존 및 증명을 요구하는 환경에서 적합