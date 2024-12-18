---
tags:
  - Spring
  - Spring-Integration
date: 2024-12-01
---


- Enterprise Application Integration 패턴을 구현하기 위한 Spring framework의 서브 프로젝트
- `Spring Integration`을 사용하면 메시지 기반의 아키텍처를 사용하여 다양한 시스템 간의 통합을 쉽게 구현할 수 있음
- message routing, 변환, 필터링, message channel 및 message endpoint 등 다양한 기능을 제공
- xml, java config, java dsl 등의 방법으로 구성이 가능


### Spring Integration의 장점

- **모듈화 및 유지 보수성**
    
    - 새로운 필터 조건이나 저장 방식이 필요할 때 확장이 용이합니다.
- **EIP(Enterprise Integration Patterns) 지원**
    
    - Spring Integration의 routing, filtering, transform 등의 기능을 활용하여 복잡한 이벤트 흐름을 체계적으로 처리할 수 있습니다.
- **비동기 및 확장성**
    
    - 비동기로 이벤트를 처리할 수 있으며, Spring Integration의 비동기 메시지 채널을 활용하면 높은 성능과 확장성을 제공할 수 있습니다.
- **다양한 통합 가능성**
    
    - 이벤트 처리 후 결과를 데이터베이스, 파일 시스템, HTTP API 등으로 쉽게 저장하거나 전송할 수 있습니다.



## Ref
- https://blog.leaphop.co.kr/blogs/47/Spring_Integration
- https://sup2is.github.io/2020/08/12/what-is-spring-integration.html
- https://github.com/spring-projects/spring-integration
- https://www.baeldung.com/spring-integration