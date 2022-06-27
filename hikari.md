## hikari 

spring-datasource-hikari 프로퍼티

- pool-name
- connection-timeout
    
    pool에서 커넥션 할 때 대기시간
    
    대기시간 안에 못 구하면 exception이 발생(최소값 250)
    
    기본값 30000(30초)
    
- maximumPoolSize
    
    유휴상태 + 사용중인 커넥션을 포함해 풀이 허용하는 최대 커넥션 개수
    
    DB에 대한 실제 커넥션의 최대 개수를 결정
    
    풀이 이 크기에 도달하고 유휴 커넥션이 없을 때 connectionTimeout이 지날 때까지 getConnection() 호출을 blocking 된다. 
    
    기본값은 10
    
- minimum-idle
    
    풀이 유지할 유휴 커넥션의 최소 개수 설정
    
    기본값 10
    
- max-lifetime
    
    커넥션의 최대 유지 시간을 밀리초 단위로 설정
    
    이 시간이 지난 커넥션 중 사용중인 커넥션은 종료된 이후에 풀에서 제거한다.
    
    DB나 infra에서 제한한 커넥션 제한 시간보다 최소 30초는 짧아야 한다.
    
    기본값은 1,800,000(30분)