# MSA(Micro Service Architecture)
* 마이크로 서비스 아키텍처 스타일은 단일 응용 프로그램을 나누어 작은 서비스의 조합으로 구축하는 방법

## Api Gateway
* API서버 앞단에서 모든 API 서버들의 엔드포인트를 단일화하여 묶어주고 API에 대한 인증과 인가 기능에서 부터 메세지에 따라서 여러 서버로 라우팅 하는 고급기능 까지 많은 기능을 담당

> 인증/인가에 관련된 기능 </br>
> - API 토큰 발급 </br>
> - 엔드포인트별 API 호출 인증 </br>
> - 엔드포인트별 API 요청 인가 </br>
> API 라우팅 </br>
> - 백엔드 API 서버로의 로드 밸런싱 </br>
> - 서비스 및 클라이언트 별 엔드포인트 제공 </br>
> - 메세지 또는 헤더기반 라우팅 </br>
> 공통 로직 처리 </br>
> 메디에이션 기능 (Mediation) </br>
> - 메세지 포맷 변환 (Message format transformation) </br>
> - 프로토콜 변환 </br>
> - 메세지 호출 패턴 변환 (Message Exchange Pattern : MEP) </br>
> - 어그레게이션 (aggregation) </br>
> 로깅 및 미터링 </br>
> - API 호출 로깅 </br>
> - API 미터링 & 차징 (Metering & Charing) </br>
> - QoS 조정 (Quality of service) </br>

## Spring Cloud Netelix OSS
### Hystrix
* Circuit Breaker

### Eureka
* Service Discovery
* Ribbon과 같이 쓰면 효과적

### Ribbon
* Client Side Load Balancer

### Zull
* API Gateway(Router and Filter)

### turbine
* 스트림 메시지 수집

### feign
* 서비스 호출

### Monitoring
* Trace 모니터링
    - Zipkin
* Hystrix 모니터링
    - Hystrix Dashboard
* Spring Boot Admin
    - Actuator(메모리, GC 등등)

### Zipkin
* 분산 트렌젝션이랑 여러개의 서비스를 걸쳐서 이루어 지는 트렌젝션을 추적하는 기능을 정의
* 트위터에서 개발
* API간의 호출 추적
* Trace, Span
* Spring Cloud Sleuth

### 모놀리식에서 마이크로서비스 전환 - 방법
* 도메인에만 개발만 할 수 있도록 제공
* API Helper 제공
* 트랜잭션은 MQ로 전환