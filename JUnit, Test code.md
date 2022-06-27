쥬피터는 5지원, 

Vintage는 4.3 지원, 테스트엔진 제공

JUnit Platform → 테스트 실행런처 제공, 테스트 API 제공

### 어노테이션

- `@Test` - 테스트 메서드를 나타냄, 어떤 속성도 선언 x
- 생명주기 어노테이션
    - `@BeforeAll`  `@AfterAll` → 1번만
    - `@BeforeEach` `@AfterEach` → 1 or more
- `@Disabled` - 테스트 하지 않는 것 표시
- `@DisplayName` - 테스트 표현
- `@RepeatedTest` - 특정 테스트 반복
- `@ParameterizedTest` - 여러 다른 매개변수를 대입해가면서 반복 실행
    - `@CsvSource(value = ....)`
- `@Nested` - 테스트 클래스 안에 내부 클래스를 정의
- Assertion - 수행 결과 판별
    - static
- AssertAll - 끝까지 실행
- assertThrows(expectedType, executable) - 예외 발생 확인 테스트
- assertTimeout(duration, executable) -  특정 시간 안에 끝나는지
- Assumption - 전제문이 true면 실행, false면 종료
    - assumeTrue - false 일 때, 테스트 전체가 실행되지 않음
    - assumingThat
    

### Why

- 안정감
- 다른 개발자들에게 코드 흐름을 보이기 쉬움
- **설계를 테스트 할 것**

### test 하기 힘든 것

Non-testable → 의도한 전략대로 반환

- random, shuffles, LocalDateTime.now()
- 외부 세계 - HTTP, 외부 저장소

### Stub

테스트하는 대상이 의존하는 요소의 동작을 시뮬레이션한다.

실제 코드와 준비되지 않은 코드를 미리 정해진 답변으로 가장한다.

### 단위테스트 -  Why we use @Mock

- 이미 검증된 라이브러리 클래스를 호출하는 것은 문제가 되지 않음
- 검증 안 된 다른 팀원이 구현한 클래스를 호출하는 것은 문제가 된다!
- 예를 들어, mapper 객체는 service를 테스트 할 때 `@Autowired` 되야 한다. → mapper 를 남이 구현한 상태에서 아직 완성되지 않은 경우 어떻게 테스트할까?
    - 내가 구현한 service 로직 테스트 할 때 mapperfmf 최소한의 기능만 하는 mock 객체로 만들자

Mockito → 테스트 mock 객체를 쉽게 구현하게 도와주는 framework