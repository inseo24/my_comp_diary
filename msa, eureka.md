- service discovery
- client → load balancer → service discover(eureka) → instance A, B, C …

`@EnableEurekaServer`

→ 유레카 서버

### 서비스를 구동하는 방식

1. SpringBoot start
2. Edit configuation → 복사하고, 그 안에 vm options 에서 다른 port 부여해서 사용
3. 터미널 사용
    1. mvn clear → mvn compile package (target 파일 생성(jar))
    2. java -jar 로 port 번호 부여해서 run

### API Gateway, Service Registry

API Gateway 

- 클라이언트 요청에 대한 백엔드 API 통합 처리 및 관리
- 요청/응답 라우팅, 인증, 보안처리, 로깅 및 모니터링

Service Registry

- 서비스의 논리적인 이름과 물리적인 주소를 관리



### Antifragile

- auto scaling
- microservices
- chaos engineering
- continuous deployments : CI/CD

### microservice

Eureka → Service discovery

1. 서비스 등록
2. client → API Gateway → service discovery → service

### 0 port(random port)

- instance id 부여해 사용

### Discovery-service

1. eureka server 등록 - `@EnableEurekaServer`
2. yaml 
    1. server port 정보
    2. application 이름(ID)
    3. eureka : client : register-with-eureka : false, fetch-registry: false
        
        자기 자신 정보를 등록하지 않기 위한 설정 필요(서버의 경우, 서버로 두기 위해서)
        
    

### Client Service

1. eureka client 추가
    1. `@EnableDiscoveryClient`
    2. serivce-url : defaultZone : 유레카 서버 주소
    3. eureka-discovery-client(true) 

### API-Gateway (Spring Cloud Gateway)

- eureka discovery client
- gateway(Spring Cloud Routing)
- cloud.gateway.routes : ?
    - id : 서비스 이름
    - uri : lb://서비스이름(대문자)
    - predicates : 조건(gateway handler mapping)
- eureka-discovery-client(true) : 유레카 연동

