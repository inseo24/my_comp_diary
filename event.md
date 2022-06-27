
### 이벤트

- 이벤트 : 다른 서비스에 영향을 미치는 데이터 수정/추가/삭제 처리
- 이벤트 버스 : 발생한 이벤트들을 저장하는 저장소 개념, 이벤트의 통합관리 + 비동기처리
- 이벤트 스트리밍 : 이벤트가 지속적으로 일어남
- 이벤트 소싱 : 이벤트의 지속적인 수집, 처리

### 메시지 큐

- 메시지 큐 : FIFO의 데이터 구조로 되어있음
- Producer : 메시지 생산자
- Consumer : 메시지 소비자, polling vs listening 방식으로 메시지 수신
    - polling - 주기적으로 조회
    - listening - 접속 포트에 응답 대기
- 1:1 유니캐스트 방식의 메시지 전송에 적합


- pub/sub messaging
    - publisher(pub) → topic → subscriber(sub)
    - publisher : 메시지 게시자
    - subscriber : 메시지 구독자, topic에 구독함
    - 1:N 브로드캐스에 적합