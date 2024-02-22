---
tags:
  - DesignPattern
---

## IoC(Inversion of Control, 제어의 역전)

Object의 생성, 관계의 설정, 사용, 제거 등 Object 전반에 걸친 모든 제어 권한을 Application이 가지는 게 아닌 Famework의 Container에게 넘기는 개념을 말합니다.

GoF의 디자인 패턴에서 이 용어가 언급이 되었습니다.

아래는 예시 코드 입니다.

```java

public class A {
	private B b;

	public A() {
		b = new B();
	}
}

```

위 코드의 경우, A class는 B class를 직접 인스턴스화 해서 의존 관계를 가지게 됩니다.

```java
public class A {

	@Autowired
	private B b;
}
```
아래는 Spring에서 많이 사용하는 IoC 방법입니다.


## IoC 적용의 이점

- 객체 간의 [[결합도]]를 낮춰준다.
- 유연한 코드 작성이 가능하다
- 가독성이 증진된다.
- 코드 중복을 방지할 수 있다.
- 유지 보수에 용이하다.