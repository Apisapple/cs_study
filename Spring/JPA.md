---
tags:
  - Java
  - Spring
date: 2024-07-13
---
# JPA
> Java [[ORM]] 기술에 대한 API 표준 명세

## JPA의 사용 이유

1. 생산성
   - JPA를 사용하면 자바 컬렉션에 ==객체를 저장하듯이 JPA에 저장할 객체를 전달하여 진행.== 따라서 반복적인 소스 코드와 CRUD용 SQL을 개발자가 직접 작성하지 않아도 됨.
    이를 통해, ==DB 설계 중심의 패러다임을 객체 중심으로 전환== 할 수 있다.
   
2. 유지 보수
   * 직접 JDBC API 코드를 작성해야 했던 것을 JPA가 대신 처리해주므로 필드의 추가, 삭제, 수정 등의 코드가 줄어든다. 즉, 유지보수해야 하는 코드의 수가 줄어든다.

3. 패러다임 불일치 해결
   - 상속, 연관 관계, 객체 그래프 탐색, 비교하기와 같이 패러다임의 불일치 문제를 해결해준다.
 
4. 성능
   - Application과 DB 사이에서 다양한 성능 최적화 기회를 제공한다.
    > 두 번 조회하지 않아도 되는 경우, 기존 데이터를 반환
    > SQL Hint 등의 기능도 제공할 수 있음
        
5. 데이터 접근 추상화와 벤더 독립성
   - 관계형 데이터베이스 기술에 종속되지 않고, 다양한 데이터베이스로 쉽게 사용할 수 있도록 한다.


## Entity Manager 와 Entity Factory

Entity Manager Factory
- Entity Manager를 생성해서 반환하는 역할을 하는 class
- 여러 Thread가 동시에 접근해도 안전하여 Thread 간에 공유가 가능

Entity Manager
- Entity를 저장, 수정, 삭제, 조회 등 Entity와 관련된 모든 일을 처리하는 객체
- 여러 Thread가 동시에 접근하면 동시성 문제가 발생하므로 절대 공유하면 안되는 객체

## Entity의 생명주기

Entity는 다음의 4가지 상태가 존재한다.

- **비영속(new/transient)**
	- [[영속성 컨텍스트]]와 전혀 관계가 없는 상태
	- 순수한 객체 상태이며 아직 저장하지 않은 상태
- **영속(managed)**
	- 영속성 컨텍스트에 저장된 상태
	- Entity Manager를 통해서 Entity를 영속성 컨텍스트에 저장한 상태
- **준영속(detached)**
	- 영속성 컨텍스트에 저장되었다가 분리된 상태
	- 영속성 컨텍스트가 관리하던 영속 상태의 Entity를 관리하지 않는 상태
- **삭제(removed)**
	- 삭제된 상태
	- Entity를 영속성 컨텍스트와 DB에서 삭제한 상태

![entity lifecycle](https://upload.wikimedia.org/wikipedia/commons/a/a0/EntityLifeCycle.png)

