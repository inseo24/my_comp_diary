### 코루틴

- CoroutineScope 코루틴 블록
    - 쓰레드 1개에서 동시성 프로그래밍 가능(비동기처리)
    - CoroutineContext - Job, Dispatcher 어떻게 처리할지?
    - Dispatcher - CoroutineContext를 상속 받아, 어떤 스레드를 이용해 어떻게 동작할지 미리 정의됨
        - Default : CPU 사용량이 많은 작업
        - IO : 네트워크, 디스크 사용
        - Main : 안드로이드
        - Unconfined
    - launch
    

### Annotation Processor

: 어노테이션에 대한 코드베이스를 검사하거나 새로운 코드 생성에 사용

### KAPT

: kotlinc로 컴파일해 java로 작성한 어노테이션 프로세서가 동작하지 않는다.

: 이 어노테이션 처리를 도와주는게 KAPT

### apply, with, let, also, run (scope function)

scope function(범위 지정 함수)

- receiver
- block → lambda with receiver

### companion object

- object니까 객체다.
- 런타임에 실제 객체의 인스턴스로 실행된다. static 이 아니다!
- 해당 클래스가 메모리에 적재되면서 함께 생성되는 동반 객체(companion object)
- 클래스 이름만으로 참조가 가능하다.
- 인터페이스 내에도 정의할 수 있다.


### Jackson, GSON

### OkHttp, Retrofit

### kotlinModule, JavatimeModule(JSR310)

추후 정리