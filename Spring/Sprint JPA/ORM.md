---
tags:
  - DesignPattern
date: 2024-07-13
---
# ORM (Object-Relational Mapping)

객체 지향 프로그래밍 언어를 사용하여 호환되지 않는 유형의 시스템 간에 데이터를 변환하는 프로그래밍 기술을 말한다. **즉, 객체와 관계형 데이터베이스의 데이터를 Object에 연결하는 것을 의미한다.** ORM을 사용하면 ==SQL Query문 없이== 데이터를 DB에 저장하고 관리할 수 있습니다.

개발자가 객체 지향 프로그래밍에 더 집중할 수 있게 해주며, DB 설계와 비즈니스 사이의 간극을 줄여줄 수 있습니다.

Java에서는 Hibernate, Python은 SQLAlchemy, Ruby의 ActiveRecord 등이 대표적인 ORM 라이브러리 입니다.



## ORM의 주요 기능과 장점

### 주요 기능

- 객체와 테이블 간의 데이터 연결
- 데이터 쿼리 및 조작
- 트랜잭션 관리

### 장점

- 객체 지향적인 방식으로 DB를 조작을 가능하게 해준다.
	- 개발 과정의 단순화 및 개발 시간 단축
	  
- ORM은 데이터 설계 변경 시, 코드의 대대적인 수정 없이 유연하게 대응할 수 있게 함
	- Application의 확장성과 유지 보수성을 향상
	  
- DB에 대한 독립성을 제공
	- Application의 소스 코드를 변경하지 않고, 다른 DB로 쉽게 전환하는 것이 가능

## ORM 사용 시, 고려해야 할 사항

1. 성능 저하를 초래할 가능성이 있다.
   - ORM이 생성하는 SQL 쿼리가 최적화되지 않았을 경우, 발생할 수 있다. ORM의 경우, 일반적인 경우를 대상으로 SQL 쿼리를 생성하기 때문에 특정 상황에서는 비효율적일 수 있다.

2. ORM을 사용하면 DB에서 복잡한 쿼리를 처리하는 데 한계가 있을 수 있다.
   - 일반적인 DB 작업을 간단하게 만들어 주지만, 복잡한 쿼리나 최적화가 필요한 경우 직접 작성하지 않기 때문에 어려울 수 있다.

3. 객체 모델과 DB 모델 간의 불일치 문제를 고려해야 한다.
   객체 지향 모델과 관계형 데이터베이스 모델 사이에서 구조적인 차이가 존재하며, 이를 해결하기 위해서 추가적인 작업이 필요할 수 있다.