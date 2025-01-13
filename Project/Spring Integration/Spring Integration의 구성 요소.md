---
tags:
  - Spring
  - Spring-Integration
date: 2025-01-13
---
## 구성 요소

**Message** 
- 서로 다른 Component 간의 전달되는 정보의 단위
- 각각의 Message는 `Headers`와 `Payload`로 구성이 됩니다.
	- Header : MetaData 정보를 포함
	- Payload : 실질적인 데이터 정보 포함

**Spring message 구성 요소**

``` Java
public interface Message<T> {
	T getPayload();
	MessageHeaders getHeaders();
}
```


**Channel**
- Message가 전달되는 경로 
- Message의 이동을 제어하고 관리하는 역할
- Channel의 타입
	- Point-to-Point Channel
		- 메시지가 정확히 하나의 수신자에게 전달되는 경우
		- DirectChannel
			- 메시지가 한 개의 endpoint에게 직접 동기적으로 전달되는 처리하는 채널
		- QueueChannel
			- 메시지가 큐(queue)에 저장되며, 하나씩 비동기적으로 순차적으로 처리
		- PriorityChannel
			- 메시지를 우선순위에 따라 정렬해서 메시지를 처리
		- ExecutorChannel
			- Executor 서비스와 함께 사용되어 비동기적으로 메시지를 처리
	- Publish/Subscribe Channel
		- 메시지가 여러 endpoint에게 동시에 전달되는 경우
		- PublishSubscribeChannel

**Endpoint**
- 실질적으로 Message가 처리되는 구성 요소
- 다른 채널로의 라우팅, 메시지 분할, 다시 결합하는 등의 다양한 방식으로 메시지 처리
- 메시지는 엔드포인트에 의해 소비되어야만 채널을 성공적으로 떠날 수 있으며, 엔드포인트에 의해 생성되어야만 채널에 들어갈 수 있음
- Endpoint의 종류
	- Channel Adapter
		- 외부 시스템과 통합하기 위해서 사용
		- 외부 시스템에서 데이터를 수신하거나 외부의 시스템으로 데이터를 보내는 역할
	- Service Activator
		- 메시지를 처리하기 위한 비즈니스 로직을 실행
	- Transformer
		- 메시지를 다른 형식으로 변환
	- Filter
		- 메시지를 조건에 따라 필터링해, 특정 조건을 만족하는 메시지만 다음 단계로 전달
	- Router
		- 메시지를 조건에 따라 다른 채널로 라우팅
	- Splitter
		- 메시지를 여러 부분으로 분할
	- Message Gateway
		- Application 코드와 메시징 시스템 간의 인터페이스 역할
	- Aggregator
		- 여러 개의 메시지를 모아 하나의 메시지로 병합하는 역할


## Reference
- https://godekdls.github.io/Spring%20Integration/message/
- https://docs.spring.io/spring-integration/reference/index.html
- Spring Integration In Action