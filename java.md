# 자바

--------------------------------------------------------------------
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

### Java Reference
1. WeakReference
 - GC가 언제든지 쓰레기 취급 할 수 있는 Reference : 따라서 메모리 처리에 크게 신경 쓸 필요가 없다.
 - new WeakReference(new Object()); 형태

2. SoftReference
 - GC가 메모리가 부족(OutOfMemory 상태 가기 직전) 일 경우, 쓰레기 취급 해버리는 Reference
 - new SoftReference(new Object()); 형태

3. StrongReference
 - GC가 처리 하지 않는 Reference : null 처리로 GC에 알려주는게 메모리 누수에 좋다.
 - new Object(); 형태

4. 기타
 - WeakReference에 StrongReference를 지정할 경우
   : WeakReference weakRef = new WeakReference(new Object()); 
     이렇게 생성 하고 나서 Object obj = weakRef.get(); 을 할 경우, obj는 StrongReference로 참조 된다.
     그래서 obj가 null 이 될때까지 GC가 쓰레기 취급을 하지 않게 된다.
     하지만, weakRef.get()하지 않을 경우에는 StrongReference가 아닌 WeakReference로 취급 되어
     GC가 쓰레기 취급을 하게 된다.

--------------------------------------------------------------------

* VO : 사용 되는 값이 객체로 표현 되며, 값 변경이 없는 경우를 말한다.
* DTO : 데이터의 전송을 위한 객체이며, 비지니스 로직까지 담아서 사용하기 한다.

--------------------------------------------------------------------

# Java 8
### 스트림이란
다양한 데이터 소스를 표준화된 방법으로 다루기 위한 라이브러리이다. 스트림은 데이터 소스를 추상화하고, 데이터를 다루는데 자주 사용되는 메서드들을 정의해놓았다.
스트림을 이용하면, 배열이나 컬렉션 뿐만 아니라 파일에 저장된 데이터도 모두 같은 방식으로 다룰 수 있다.

--------------------------------------------------------------------

## CompletableFuture
- 완전한 비동기식 병렬 프로그래밍 
- 명시적 쓰레드 선언없이 쓰레드를 사용할수 있다.
-  함수형 프로그래밍방식으로 비동기적으로 동시성/병렬 프로그래밍을 가능하게 함으로서 의도를 명확하게 드러내는 함축적인 프로그래밍을 가능
- 각 타스크마다 순서적 연결을 할수도 있고, 타스크의 예외처리도 가능

## 자바정렬
* Comparable : 자연스러운 순서로 정렬할 때 사용
* Comparator: 원하는 대로 정렬 순서를 지정하고 싶은 곳에 사용

## JPA
* JavaSE, JavaEE를 위한 영속성(persistence) 관리와 ORM을 위한 표준 기술

#### 장점
* 객체지향적으로 데이터를 관리할 수 있기 때문에 비즈니스 로직에 집중 할 수 있으며, 객체지향 개발이 가능하다.
* 테이블 생성, 변경, 관리가 쉽다. (JPA를 잘 이해하고 있는 경우)
* 로직을 쿼리에 집중하기 보다는 객체자체에 집중 할 수 있다.
* 빠른 개발이 가능하다.

#### 단점
* 어렵다. 장점을 더 극대화 하기 위해서 알아야 할게 많다.
* 잘 이해하고 사용하지 않으면 데이터 손실이 있을 수 있다. (persistence context)
* 성능상 문제가 있을 수 있다.(이 문제 또한 잘 이해해야 해결이 가능하다.)[etchType.EAGER, FetchType.LAZY]
--------------------------------------------------------------------

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

### spring 대표 어노테이션의 차이
  * @Component
    - sping에서 관리되는 객체임을 표시하기 위해 사용하는 가장 기본적인 annotation, scan-auto-detection과 dependency injection을 사용하기 위해서 사용되는 가장 기본 어노테이션, bean 인스턴스 생성
  * @Controller
    -  Web MVC에 사용되는 어노테이션, @RequestMapping 어노테이션을 해당 어노테이션 밑에서만 사용할 수 있음
  * @Repository
    - data repository를 나타내는 어노테이션, @Repository는 플랫품 특정 exception을 잡아 sping의 unchecked exception으로 뱉어냄
  * @Service
    - 비즈니스 로직이나 respository layer 호출하는 역할에 사용, @Component외 추가된 기능이 없음

### 자바빈즈(JavaBeans): 자바로 작성된 소프트웨어 컴포넌트

### Spring Web 비동기
1. Callable
   * Callable 인터페이스는 추상 메서드가 하나 있는 FunctionalInterface 이다. 해당 타입을 리턴하면 Spring에서 적절하게 리턴값을 만들어 준다.
   * 단점은 아무 설정을 할 수 없다. 타임아웃이라던지 어떤 스레드풀을 사용할지 결정할 수 없다.
2. CompletableFuture
   * mvc에서 리턴 타입으로 정의하면 Spring에서 적절하게 리턴해준다.
   * CompletableFuture.supplyAsync 경우에는 Executor를 추가로 파라미터로 받고 있다. 그래서 좀 더 나은 설정을 할 수 있다.
3. ListenableFuture
   * AsyncRestTemplate의 리턴타입은 ListenableFuture로 정의 되어있다.
   * 비동기 적으로 특정한 API를 호출할 때 유용한 AsyncRestTemplate은 리턴 타입 그대로 spring mvc에게 넘겨줘도 된다.
4. WebAsyncTask
   * Callable 인터페어스보다 좀 더 나은 설정을 갖고 있음 실제로 WebAsyncTask 클래스 안에는 Callable을 사용하고 있으며 타임아웃 설정, executor 등을 설정 할 수 있다.
5. DeferredResult
   * 이건 전혀 다른 스레드에서도 사용가능하다.
   * DeferredResult를 생성해서 큐에 담고 바로 리턴하면 된다. 그리고 나서 전혀 다른스레드에서 setResult를 호출하면 그때 뷰에 전달된다.

## Spring Boot
* 단독으로 실행되면 상용화 수준의 스프링 기반 애플리케이션을 쉽게 만들 수 있음.
* Spring 프로젝트가 제공하는 다양한 라이브러리와 프레임워크로 빨리게 사용할 수 있게 하는 프레임워크.
* Web 어플리케이션의 경우, 내장 Tomcat을 시작 (Jetty와 Undertow로 전환 가능).
* 보통의 Java 프로그램으로도 동작 가능 

## Spring Batch
* 배치란 일괄처리
* 대용량 데이터, 자동화, 견공성, 신뢰성, 성능

## Spring Cloud

--------------------------------------------------------------------
# Reactive 
--------------------------------------------------------------------

# Docker
* 컨테이너 기반의 오픈소스 가상화 플랫폼
* 컨테이너는 격리된 공간에서 프로세스가 동작하는 기술ㅍ 것을 포함하는 완전한 파일 시스템 안에 감쌈
* 가상 머신이라고 하기에는 격리된 환경을 만들어주는 도구

--------------------------------------------------------------------

# Netty
* 비동기식 이벤트 기반 네트워킹 프레임워크

--------------------------------------------------------------------

# Rest Api
* HTTP URI로 잘 표현된 리소스에 대한 행위를 HTTP Method로 정의
* 네트워크 기반의 아키텍쳐
* REST는 요소로는 크게 리소스,메서드,메세지 3가지 요소로 구성

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

--------------------------------------------------------------------

### Non-blocking
* Non-blocking이란, 어떤 쓰레드에서 오류가 발생하거나 멈추었을 때 다른 쓰레드에게 영향을 끼치지 않도록 만드는 방법들을 말한다
* 공유 자원(메모리, 파일 등)를 사용하는 멀티 쓰레드 프로그래밍을 할 때, 특정 공유 자원을 사용하는 부분에서 뮤텍스나 세마포어 등을 사용하여 여러 쓰레드에서 동시에 접근하지 못하도록 개발자가 보장하는 것이 전통적인 방법이었다. 반면 Non-blocking algorithm(Wait-freedom, Lock-freedom 등)을 사용하면 공유 자원을 안전하게 동시에 사용할 수 있다.
* Non-blocking I/O란, 입출력 처리는 시작만 해둔 채 완료되지 않은 상태에서 다른 처리 작업을 계속 진행할 수 있도록 멈추지 않고 입출력 처리를 기다리는 방법을 말한다. (Polling, Callback function )

1. Wait-freedom (기다림이 없으나 호출수 한정)
   * 모든 호출이 한정된 수의 단계로 끝나도록 보장되는 경우 메소드는 대기하지 않아도됩니다.
   * wait-free 메소드는 결코 블로킹되지 않으며 교착상태가 발생하지 않으며 참여자는 제한된 수의 호출후에 진행할수 있으므로 궁핍(기아)현상이 발생하지 않습니다.

2. Lock-freedom (Lock이 없음)
   * Lock이 없기때문에 교착상태가 발생하지 않지만 호출이 결국 완료되는것을 보장하지 않기때문에 궁핍(기아)현상을 보장하기에는 충분하지 않습니다.

3. Obstruction-freedom (기다림/Lock등 방해요소가없음)
   * 메소드가 격리되어 작동하다가, 특정 시점을 (Write중) obstacle-free(방해가 없는상태)라고 하며 ,다른 스레드가 접근시 아무런 조취를 하지 않기때문에 진행작업이 중단될수가 있습니다. ( access violation at address )

4. 낙관성 동시성 제어 (OCC-Optimistic concurrency control)
   * 발생가능성이 거의 없을것으로 예상하고(충돌로 인해 문제 발생시,스케쥴을 조정해버려서 해결) 일정에따라 다시 시도하여 작업 성공으로 간주합니다.

---------------------------------------------------------------------
