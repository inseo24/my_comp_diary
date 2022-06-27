### Layered Architecture

- horizontal layers(수평으로 관리)
- 상위 레이어가 하위 레이어를 사용

단점 : 도메인이 인프라에 의존해 관심사가 섞이게 된다.(JPA)

user interface(presentation) → application → **domain → infra(이 부분에서 domain이 infra에 의존)**

→ 목표는 관심사의 분리

→ 다른 계층이 각자 책임과 역할을 부여해 결합도를 낮추고, 과부하를 줄여 재사용성, 유지보수성을 향상

### Dependency Inversion Principle(DIP)

저수준 모듈이 고수준 모듈을 의존하게 해야 한다.

→ 즉, 인프라가 도메인을 의존하게끔 바꿔야 한다.

→ 레이어드 아키텍처는 DIP 원칙을 위반함

→ 그래서 해결책으로 나오는게 헥사고날 아키텍처

### MSA pattern

- 독립적으로 배포 가능하고
- 기존 비즈니스 로직과 분리되고
- 기존 서비스와 연결이 가능하며
- 독립적으로 확장이 가능함

### 이벤트 중심 아키텍처

- event sourcing - 비즈니스 객체 저장 방식, 이벤트로 모델링
- 도메인 주도 설계 - bounded context 정의해서 서비스와 매핑
- CQRS - 명령-쿼리 책임 분리(Command-Query Responsibility Segregation)
- 데이터 조회하는 쿼리 모델과 업데이트하는 커맨드 모델 분리

### 헥사고날 아키텍처

client → inbound adatper(ex: webAdapater) → (interface) inbound port → service → domain

→ (interface)outbound adapter(ex: persistence adatper, infrastructure adapter)

Package

- adatper
    - exception
    - inbound
        - web
            - dto
            - resource
    - outbound
        - infra
        - persistence(jpa …)
- application
    - component
    - port
        - inbound
        - outbound
    - service
- domain
- common
- extension
- configuration