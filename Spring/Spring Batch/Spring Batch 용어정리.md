---
tags:
  - Spring
  - Spring-Batch
date: 2024-11-29
---

**Job**
- 전체 배치 처리 과정을 추상화한 개념으로, 하나 이상의 Step을 포함하며 Spring Batch 게층에서 가장 상위에 위치하는 개념
- 각각의 Job은 고유한 이름을 가지며, 이 이름은 실행에 필요로 하는 파라미터와 함께 JobInstance를 구분하는데 사용

**JobInstance**
- 특정 Job의 실제 실행되는 인스턴스를 의미
- 한번 생성된 JobInstance는 해당 날짜의 데이터를 처리하는데 사용이 되며, 실패를 하였을 경우, 같은 JobInstance를 다시 실행하여 작업을 완료하는 것이 가능

**JobParameters**
- JobInstance를 구별하기 위해서 사용되는 파라미터
- Spring Batch는 String, Double, Long, Date 4가지 타입의 파라미터를 지원

**JobExecution**
- JobInstance의 한 번의 시행 정보
- 실행 상태, 시작 시간, 종료 시간, 생성 시간 등 JobInstance의 실행에 대한 세부적인 정보 가지고 있음

**Step**
- Job의 하위 단계로서 실제 Batch 처리 작업이 이루어지는 단위
- 한 개 이상의 Step으로 Job이 구성이 되며, 각 Step은 순차적으로 처리
- 각 Step의 내부에는 `ItemReader`, `ItemProcessor`, `ItemWriter`를 사용하는 chunk 방식 또는 `Tasklet` 하나를 가지는 것이 가능

**StepExecution**
- Step의 한 번의 실행을 말하며, Step의 실행 상태, 실행 시간 등의 정보를 포함
- 각 Step의 실행 시도마다 새로운 StepExecution이 생성
- 읽은 아이템의 수, 쓴 아이템의 수, Commit 횟수, Skip한 아이템의 수 등의 Step 실행에 대한 상세한 정보도 포함

**ExecutionContext**
- Step 간 또는 Job 실행 도중 데이터를 공유하는 데 사용되는 저장소
**JobRepository**

**JobLauncher**

**ItemReader**

**ItemProcessor**

**ItemWriter**

**TeskLet**

**JobOperator**

**JobExplorer**
