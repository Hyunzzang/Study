# 자바
## jvm
* Java Virtual Machine 의 줄임말 이며 Java Byte Code를 OS에 맞게 해석 해주는 역할

> Java compiler는 .java 파일을 .class 라는 Java byte code로 변환 </br>
> JVM은 OS가 ByteCode를 이해할 수 있도록 해석 </br>
> JVM의 해석을 거치기 때문에 c언어 같은 네이티브 언어에비해 속도가 느렸지만 JIT(Just In Time)컴파일러를 구현해 이점을 극복 </br>
> OS상관없이 실행 </br>

### JVM 구조
#### Class Loader
* RunTime 시점에 클래스를 로딩하게 해주며 클래스의 인스턴스를 생성하면 클래스 로더를 통해 메모리에 로드하게 됨

#### Runtime Data Areas
* JVM이 프로그램을 수행하기 위해 OS로 부터 별도로 할당 받은 메모리 공간

> PC Register : CPU의 Register와 역할이 비슷 현재 수행 중인 JVM 명령의 주소 값이 저장 (각 Thread 별로 하나씩 생성) </br>
> Stack Area : Method 내에서 사용되는 값들 (매개변수, 지역변수, 리턴값 등)이 저당되는 구역으로 메소드가 호출 될 때 LIFO로 하나씩 생성되고, 메소드 실행이 완료되면 LIFO로 하나씩 지워짐 (각 Thread 별로 하나씩 생성)  </br>
> Native Method Stack : 다른 언어(C, C++등)의 메소드 호출을 위해 할당되는 구역으로 언어에 맞게 Stack이 형성되는 구역  </br>
> Method Area : 클래스, 변수, Method, static변수, 상수 정보 등이 저장되는 영역 </br>
> Heap Area : new 명령어로 생성된 인스턴스와 객체가 저장되는 구역(Garbage Collection 이슈 이 영역에서 일어나면, 모든 Thread가 공유)  </br>

#### Execution Engine



* VO : 사용 되는 값이 객체로 표현 되며, 값 변경이 없는 경우를 말한다.
* DTO : 데이터의 전송을 위한 객체이며, 비지니스 로직까지 담아서 사용하기 한다.

## CompletableFuture
- 완전한 비동기식 병렬 프로그래밍 
- 명시적 쓰레드 선언없이 쓰레드를 사용할수 있다.
-  함수형 프로그래밍방식으로 비동기적으로 동시성/병렬 프로그래밍을 가능하게 함으로서 의도를 명확하게 드러내는 함축적인 프로그래밍을 가능
- 각 타스크마다 순서적 연결을 할수도 있고, 타스크의 예외처리도 가능

## 자바정렬
* Comparable : 자연스러운 순서로 정렬할 때 사용
* Comparator: 원하는 대로 정렬 순서를 지정하고 싶은 곳에 사용

# Spring 
### DI
* Dependency Injection의 약자로 번역 하면 의존성 주입
* 객체를 직접 생성하는 게 아니라 외부에서 생성한 후 주입을 시켜주는 방식

### Ioc(Inversion of Control)
* 객체(Bean) 생명주기 관리(컨트롤)
* DI Pattern 제공
* 비즈니스 로직에 집중
* Bean이란 IoC Container에 저장된 객체
* DI나 Bean에 생명주기는 제어를 역전 시켜 Framework에서 제어

### AOP (Aspect-Oriented Programming)
* 관점(관심) 지향 프로그래밍
* IoC가 낮은 결합도와 관련된 것이라면 AOP 는 높은 응집도와 관련
* 기능을 핵심 비지니스 로직과 공통 모듈로 구분하고, 핵심 로직에 영향을 미치지 않고 사이사이에 공통 모듈을 효과적으로 잘 끼워넣도록 하는 개발 방법

### 자바빈즈(JavaBeans): 자바로 작성된 소프트웨어 컴포넌트

# Docker
* 컨테이너 기반의 오픈소스 가상화 플랫폼
* 컨테이너는 격리된 공간에서 프로세스가 동작하는 기술
* 도커 컨테이너는 일종의 소프트웨어를 소프트웨어의 실행에 필요한 모든 것을 포함하는 완전한 파일 시스템 안에 감쌈
* 가상 머신이라고 하기에는 격리된 환경을 만들어주는 도구

# Netty
* 비동기식 이벤트 기반 네트워킹 프레임워크

# Rest Api
* HTTP URI로 잘 표현된 리소스에 대한 행위를 HTTP Method로 정의
* 네트워크 기반의 아키텍쳐
* REST는 요소로는 크게 리소스,메서드,메세지 3가지 요소로 구성


# MSA(Micro Service Architecture)
* 마이크로 서비스 아키텍처 스타일은 단일 응용 프로그램을 나누어 작은 서비스의 조합으로 구축하는 방법

# Api Gateway
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


# DDD(Domain Driven Design)

### Entity
- 속성이 아닌 식별성을 기준으로 정의되는 도메인 객체

### Value Object
- 식별성이 아닌 속성을 이용한 정의된는 불변 객체
- Entity와 구별은 식별성

### Service
- Domain Object에서 위치시키기 어려운 operation을 가지는 객체
- 여러 Domain Object 다루는 연산 Service의 오퍼레이션은 알반적으로 stateless

### Module

### Aggregate

### Factory

### Repository