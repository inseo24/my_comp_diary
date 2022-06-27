### SimpleJpaRepository

- JpaRepository를 구현하는 구현체
- 얘를 상속 받으면 안에 있는 기능을 다 쓸 수 있다

### 양방향을 쓰는 경우

** 1:N 관계에서 cascade로 insert를 수행 시 양방향이 좋다.

- 하나의 트랜잭션으로 묶여 3개의 쿼리가 기대가 되나, update 쿼리가 5개가 발생 할 경우 → 양방향으로!
    
    (FK 지정을 위해 update 쿼리)
    
- 양방향 복합키를 사용할 때,
    - 복합키를 외래키로 지정할 때는 `@JoinColumn` 대신 `@Mapsld` 사용(연관관계 주인 설정)
- N+1은 eager fetch 때문에 발생하는 것이 아님
    - lazy라도 연관 엔티티 참조할 때 추가적인 쿼리가 발생
- findAll() → N+1 문제를 발생시키는 것 x

- fetch 전략은 단일레코드에만 적용된다.
- findAll() 같은 여러 레코드 조회는 fetch 전략이 적용되지 않음
- 하지만, 반환된 레코드 하나하나를 선택하면 연관 엔티티를 참조하는 순간 추가적인 쿼리가 수행되는 것
    
    → fetchJoin, `@EntityGraph` 로 해결
    

### FetchJoin으로 N+1 문제 해결 시 흔히 하는 실수

- Paginatation과 FetchJoin을 같이 쓸 때
    - limit 쿼리가 실행되는게 아님, 모든 레코드를 조회한 후 인메모리에 모든 레코드를 올려놓고, Pagination이 실행되는 것
    - Pagination과 FetchJoin은 분리해서 사용
- 하나의 엔티티에서 2개 이상의 연관관계를 FetchJoin 한 경우
    - **MultipleBagFetchException**
    - 하이버네이트의 Bag이 수행결과에서 만들어지는 카테시안곱에서 어떤 행이 유효한지 판단할 수 없어 발생함
    - 자바의 util.List 타입은 하이버네이트의 Bag으로 매핑됨
    - Bag 타입은 중복요소를 허용하는 unordered(비순차) 컬렉션이다.
    - List를 Set으로 변경하거나 `@OrderColumn` 을 사용해 순서 부여해서 해결한다.
- JPA Repository 메서드로 Join → “_” 사용 - 내부 속성값 접근
    - ex) findById_PK_Type
- Page와 Slice
    - page는 count, Slice는 limit + 1(다음 레코드 확인)
- JPA Repository 메서드로 DTO 주입 가능함
    - 인터페이스 기반 Projection
    - Dynamic Projection(제네릭)

### 연관관계

- 방향 Direction : 단방향, 양방향
- 다중성 Multiplicity : N:1, 1:N, 1:1, N:N
- 연관관계의 주인(Owner)

`@EntityGraph` → left outer join

⇒ 조인문 왼쪽의 테이블의 모든 결과를 가져오고 오른쪽 테이블 데이터를 매칭한다.

⇒ 카테시안 곱 발생 가능

해결방법

1. `@OneToMany` 필드 타입을 Set으로 선언
2. distinct 쿼리

### mappedBy

- 양방향일 때는 `@OneToMany` 에 쓴다.
- 보통은 referencing side에서 선언

### JoinColumn

- 외래키 매핑할 때 사용
- name 속성에 외래키 이름 지정
- 보통 owner side에서 선언
- 양쪽에서 모두 사용가능

### EntityManager

Jpa 쿼리 만드는 객체

### JpaQueryFactory

QueryDSL의 쿼리를 만드는 객체

### `@Formula`

조건절로 사용하거나 집계된 데이터가 필요할 때 사용

### Why we use JPA, Hibernate?

기존 개발 대부분이 RDBMS를 사용하고, SQL 작업이 필연적

→ 반복적인 쿼리 작성, SQL 의존적인 개발

→ SQL 쿼리문을 쓰지 않고 객체 중심의 SQL을 작성할 수 있을까?

→ JPA가 대신 해준다! → object와 relation(RDBM)간의 불일치를 해결

→ Domain에 해당하는 객체에 어노테이션을 붙여 DB 관리 → 비즈니스에 집중

### 단점은?

- 어노테이션 양이 증가하고 의존성이 발생한다.
- Layered Architecture에 위반함 → **아래서 자세히**
- JPA는 infra에 해당하는데, infra가 도메인을 알게 되는 결과 발생 → 이 문제 때문에 jooq 등을 사용하기도 함
- 모든 엔티티를 객체화 해서 도메인 모델이 빈약해진다.(빈약한 Bean에 생성)
- 우연한 복잡성이 발생
    - SQL 편하게 쓰려고 JPA 쓰는데, 다시 JPA, QueryDsl을 공부해야 하는 꼴
    

### Layered Architecture

단점 : 도메인이 인프라에 의존해 관심사가 섞이게 된다.

user interface(presentation) → application → **domain → infra(이 부분에서 domain이 infra에 의존)**

→ 목표는 관심사의 분리

→ 다른 계층이 각자 책임과 역할을 부여해 결합도를 낮추고, 과부하를 줄여 재사용성, 유지보수성을 향상

### Dependency Inversion Principle(DIP)

저수준 모듈이 고수준 모듈을 의존하게 해야 한다.

→ 즉, 인프라가 도메인을 의존하게끔 바꿔야 한다.

→ 레이어드 아키텍처는 DIP 원칙을 위반함

→ 그래서 해결책으로 나오는 것 중 하나가 헥사고날 아키텍처