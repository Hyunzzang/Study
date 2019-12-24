* 오브젝트 클래스의 메소드 뭐있냐?
  > **boolean equals(Object obj)** : 두 개의 객체가 같은지 비교하여 같으면 true를, 같지 않으면 false를 반환한다. </br>
  > **String toString()** : 현재 객체의 문자열을 반환한다. </br>
  > **protected Object clone()** : 객체를 복사한다. </br>
  > **protected void finalize()** : 가비지 컬렉션 직전에 객체의 리소스를 정리할 때 호출한다. </br>
  > **Class getClass()** : 객체의 클래스형을 반환한다. </br>
  > **int hashCode()** : 객체의 코드값을 반환한다. </br>
  > **void notify()** : wait된 스레드 실행을 재개할 때 호출한다. </br> 
  > **void notifyAll()** : wait된 모든 스레드 실행을 재개할 때 호출한다. </br>
  > **void wait()** : 스레드를 일시적으로 중지할 때 호출한다. </br>
  > **void wait(long timeout)** : 주어진 시간만큼 스레드를 일시적으로 중지할 때 호출한다. </br>
  > **void wait(long timeout, int nanos)** : 주어진 시간만큼 스레드를 일시적으로 중지할 때 호출한다. </br>

* 맵에 키를 객체로 사용하려면 어떻게 해야할것 같냐?
  >  HashMap의 Key 타입으로써 기능을 충족하기 위해서는 Object 클래스의 equals와 hashCode 함수를 재정의해야 함. </br>

* 배열과 링크드리스트의 차이?
  > 배열은 index만 있다면 O(1)에 접근. 연결리스트는 최소 한 번은 리스트를 순회하여야 하므로 O(n)에 접근. </br>
  > 만약 배열에 공간이 많이 남아있고 맨 끝에 삽입한다면, 삽입 속도 역시 O(1)에 가능. 하지만 이런 경우만 발생하는 경우는 꽤 드물기 때문에 연결리스트의 필요성이 대두됨. </br>
  > 삽입과 삭제가 번번히 이루어진다면, 연결리스트 사용이 좋음. 이미 만들어진 구조에서 데이터의 접근만 필요하면 배열이 좋음. </br>
  > Array는 index로 빠르게 값을 찾을 수 있다. LinkedList는 데이터를 삭제하고 삽입하는데 빠르다. ArrayList는 데이터를 찾는데 빠르지만 데이터의 삽입과 삭제가 느리다. </br>

* list와 set의 차이?
  > list : 인덱스, 중복 허용, 저장순서를 유지</br>
  > set : 중복 허용하지 않음, 저장순서를 유지 하지 않음 </br>

* 인덱스의 구조와 동작?
  > Range Scan : 인덱스는 키 컬럼순으로 정렬되어 있기때문에 특정값을 찾다가 해당 범위를 넘어서는 값을 만나면 멈춘다. </br>
  > 인덱스를 저장하는 블럭들이 트리구조를 이루고 있다.(B-tree) </br>
  > 인덱스는 select문의 where, join에서 좋은 성능을 발휘한다. 대신 insert, update, delete문에서 성능이 떨어진다. </br>

* join 종류와 설명?
  > **inner join** : 교집합, 기준테이블과 Join한 테이블의 중복된 값을 보여 줌 </br>
  > **left outer join** : 기준테이블의 값 + 테이블과 기준테이블의 중복된 값을 보여 줌(왼쪽 테이블을 기준으로 JOIN) </br>
  > **right outer join** : 오른쪽 테이블을 기준으로 JOIN </br>
  > **full outer join** : 합집합, 데이터 모두 검색</br>
  > **cross join** : 모든 경우의 수를 전부 표현해주는 방식, 기준테이블이 A일경우 A의 데이터 한 ROW를 B테이블 전체와 JOIN하는 방식</br>
  > **self join** : 자기자신과 자기자신을 조인, 자신이 가지고 있는 칼럼을 다양하게 변형시켜 활용할 경우에 자주사용</br>

* Java Garbage Collection 구조?
  > GC가 수행되는 영역이 Heap 영역, JVM은 Heap 영역과 Non Heap 영역으로 구분 </br>
  > **JVM Heap** :  Young, Old, Permanent로 크게 3개의 영역 구성 </br>
  > **Young Generation** : </br>
  > - **Eden** </br>
  >   - new 연산자로 생성된 객체가 가장 처음 메모리에 할당되는 영역 </br>
  >   - Eden 영역이 가득차면 Survivor 영역 중 하나로 이동 </br>
  > - **Survivor** </br>
  >   - Survivor0(S0), Survivor1(S1)으로 2개로 분리 </br>
  >   - Eden 영역에서 살아남은 객체가 Survivor 영역 중 하나로 이동 </br>
  >   - S0, S1 중 하나는 반드시 비어있어야한다. </br>
  >   - S0, S1의 우선순위가 있는 것은 아니다. </br>
  >   - 객체가 S0과 S1을 이동하며 오랫동안 살아남은 객체는 일정 기준에 의해 Old 영역으로 이동한다. </br>
  > **Old Generation** : </br>
  >  - age bits 기준이 넘었거나, Young 영역이 가득찬 객체가 Old 영역으로 이동됨,</br>
  >  - Old 영역에서 발생한 GC를 Major GC(또는 Old GC) 라고 함 </br>
  > **Permanent Generation** : 클래스 메타데이터를 저장하는 공간, static class, static variable, String Pool, JIT Compiler의 최적화 정보 </br>

<img width="" height="" src=./img/jvm_heap.png></img>

* Gc 알고리즘 종류?
  > * Serial GC (-XX:+UseSerialGC) 
  >   - CPU 코어가 하나만 있을 때 사용하기 위해서 만든 방식(GC를 처리하는 스레드가 하나) </br>
  >   - Old 영역의 GC는 mark-sweep-compact이라는 알고리즘을 사용 </br>
  >   - Serial GC는 적은 메모리와 CPU 코어 개수가 적을 때 적합한 방식 </br>

  > * Parallel GC (-XX:+UseParallelGC) </br>
  >   - Parallel GC는 Serial GC와 기본적인 알고리즘은 같음 </br>
  >   - GC를 처리하는 쓰레드가 여러 개 </br>
  >   - Parallel GC는 메모리가 충분하고 코어의 개수가 많을 때 유리 </br>

  > * Parallel Old GC(-XX:+UseParallelOldGC) </br>
  >   - Parallel Old GC는 JDK 5 update 6부터 제공한 GC 방식 </br>
  >   - Parallel GC와 비교하여 Old 영역의 GC 알고리즘만 다름(Mark-Summary-Compaction 단계를 거침) </br>

  > * CMS GC (-XX:+UseConcMarkSweepGC) </br>
  >   - 힙 메모리 영역의 크기가 클 때 적합 </br>
  >   - Mark-Sweep-Remark-ConcurrentSweep 단계 </br>
  >   - 다른 GC 방식보다 메모리와 CPU를 더 많이 사용한다. </br>
  >   - Compaction 단계가 기본적으로 제공되지 않는다. </br>

  > * G1(Garbage First) GC </br>
  >   - G1 GC는 바둑판의 각 영역에 객체를 할당하고 GC를 실행 </br>
  >   - 해당 영역이 꽉 차면 다른 영역에서 객체를 할당하고 GC를 실행 </br>
  >   - Young의 세가지 영역에서 데이터가 Old 영역으로 이동하는 단계가 사라진 GC 방식 </br>
  >   - G1 GC의 가장 큰 장점은 성능 </br>

* Jvm 구조?
  > 

<img width="" height="" src=./img/jvm.png></img>


* Jvm 메모리 할당 기술
  > **bump-to-pointer** </br>
  > **TLABs(Thread-Local Allocation Buffers)** </br>

* Spring Container
  > 주입을 이용하여 객체를 관리하는 컨테이너
  > Container : Bean 클래스를 관리하는 주체
  > Bean : 스프링이 IOC방식으로 관리하는 오브젝트
  > BeanFactory: 스프링의 IOC를 담당하는 핵심 컨테이너를 가리킨다. 빈을 등록하고, 생성하고, 조회하고, 돌려주고 등 부가적인 빈을 관리하는 기능을 담당
  > ApplicationContext : 빈팩토리와 유사하지만 향상된 형태의 컨테이너(추가기능으로 국제화 지원 텍스트 메시지 관리, 이미지 파일 로드, 리스너로 등록된 빈에게 이벤트 발생 통보)
  > 객체를 재사용하는 방식으로, 기본적으로 Singleton 패턴으로 객체가 생성
  > 종류로 Bean Factory, Application Context가 있는데 Application Context를 가장 많이 사용

* ioc(Inversion of Control)
  > 객체(Bean)생성 생명주기 관리(컨트롤) </br>
  > Bean이란 IoC Container에 저장된 객체 </br>
  > DI나 Bean에 생명주기는 제어를 역전 시켜 Framework에서 제어 </br>

* DI(Dependency Injection)
  > 객체를 직접 생성하는 게 아니라 외부에서 생성한 후 주입을 시켜주는 방식 </br>
  > 의존관계가 발생함으로서 결합도를 낮춰, 코드 수정을 피할 수 있다. </br>

* 스프링 컨테이너를 설계한다면?
  > 

* 스프링 빈의 옵션?
  > **init-method** : @PostConstruct </br>
  > **lazy-init** : Bean을 최초로 호출할 때 초기화합니다. 최초 호출 시점에 따라 초기화 시점이 다름 </br>
  > **destroy-method** : @PreDestroy </br>

* Spring Bean Scope 종류
  > **singleton scope** : 스프링 IoC 컨테이너 당 하나의 객체 인스턴스에 하나의 빈을 정의한 스코프 </br>
  > **prototype scope** : 여러 개의 객체 인스턴스에 하나의 빈을 정의한 스코프(의존성 관계의 bean에 주입 될 때 새로운 객체가 생성) </br>
  > **Request scope​** : 한 HTTP 요청의 생명주기에 하나의 빈을 정의한 스코프 </br>
  > **Session scope​** : 한 HTTP 세션의 생명주기에 하난의 빈을 정의한 스코프 </br>
  > **Global session scope​** : 한 글로벌 HTTP 세션의 생명주기에 하난의 빈을 정의한 스코프</br>
  > **Application scope​** : 싱글톤 bean과 다소 비슷하지만 중요한 두 가지가 다름, ServletContext 마다 싱글톤이지만, ​스프링 ApplicationContext ​마다는 아니고(또는 특정 웹 응용 프로그램에서 여러 가지가있을 수 있다) 실제로 노출되는 것은 ServletContext 의 속성에 따라 볼 수 있음</br>

  * 싱글톤 패턴의 장단점?
  > 단 하나의 인스턴스를 생성해 사용하는 디자인 패턴 </br>
  > 고정된 메모리 영역을 얻으면서 한번의 new로 인스턴스를 사용하기 때문에 메모리 낭비를 방지할 수 있음 </br>
  > 전역 인스턴스이기 때문에 다른 클래스의 인스턴스들이 데이터를 공유하기 쉽음 </br>
  > 두 번째 이용시부터는 객체 로딩 시간이 현저하게 줄어 성능이 좋아지는 장점 </br>
  > 너무 많은 일을 하거나 많은 데이터를 공유시킬 경우 다른 클래스의 인스턴스들 간에 결합도가 높아져 "개방-폐쇄 원칙" 을 위배하게 됨 </br>
  > 멀티쓰레드환경에서 동기화처리를 안하면 인스턴스가 두개가 생성된다든지 하는 경우가 발생할 수 있음 </br>

* 바이너리서치(Binary Search)란?
  > 오름차순으로 정렬된 리스트에서 특정한 값의 위치를 찾는 알고리즘 </br>
  > 처음 중간의 값을 임의의 값으로 선택하여, 그 값과 찾고자 하는 값의 크고 작음을 비교하는 방식을 채택하고 있다. 처음 선택한 중앙값이 만약 찾는 값보다 크면 그 값은 새로운 최댓값이 되며, 작으면 그 값은 새로운 최솟값이 된다. 검색 원리상 정렬된 리스트에만 사용할 수 있다는 단점이 있지만, 검색이 반복될 때마다 목표값을 찾을 확률은 두 배가 되므로 속도가 빠르다는 장점 </br>

* 오버로딩과 오버라이딩?
  >

* Java volatile
  > volatile keyword는 Java 변수를 Main Memory에 저장하겠다라는 것을 명시하는 것 </br>
  > 매번 변수의 값을 Read할 때마다 CPU cache에 저장된 값이 아닌 Main Memory에서 읽는 것 </br>
  > 변수의 값을 Write할 때마다 Main Memory에 까지 작성하는 것 </br>
  > Multi Thread 환경에서 하나의 Thread만 read & write하고 나머지 Thread가 read하는 상황에서 가장 최신의 값을 보장 </br>
  > 하나의 Thread가 아닌 여러 Thread가 write하는 상황에서는 적합하지 않음 </br>

* 자바 1.8 의 특징
  > **Lambda expressions** : </br>
  >  - 람다 표현식은 Anonymous Function </br>
  >  - 람다를 이용하여 코드를 간결하게 할 수 있음 </br>
  > **Method Reference** : </br>
  >  - 특정 람다 표현식을 축약한 것으로 볼 수 있음 </br>
  >  - 메서드 정의를 활용하여 람다처럼 사용 가능 </br>
  > **Stream** : </br>
  >  - 다양한 데이터 소스를 표준화된 방법으로 다루기 위한 라이브러리 </br>
  >  - 스트림은 데이터 소스를 추상화하고, 데이터를 다루는데 자주 사용되는 메서드들을 정의 </br>
  >  - 배열이나 컬렉션 뿐만 아니라 파일에 저장된 데이터도 모두 같은 방식으로 다룰 수 있음 </br>
  > **Parallel Stream** : </br>
  > **Default Method** : </br>
  > **Optional** : </br>
  > **CompletaleFuture** : </br>
  > **New date / time APIs** </br>
  >  - Joda-Time의 많은 기능을 java.time 패키지로 추가</br>

* 프로세스와 스레드의 차이
> 프로세스는 운영체제로부터 자원을 할당받는 작업의 단위이고 스레드는 프로세스가 할당받은 자원을 이용하는 실행 단위 </br>
> 


-------------------------------------------------------------------------------

디자인패턴 : Singleton 손코딩, Builder Pattern, 

collections 설명

hashtable collision

linked list 중간삽입 스도코드

gc종류 및 설명

outer join sql query작성

JPA n+1

Spring bean scope

spring 구조

Checked, Upchecked exception

stringbuilder stringbuffer string 차이

dfs bfs, 스택, 큐

olap oltp
* OLTP (Online Transaction Processing) - 온라인 트랜잭션 처리
* OLAP (OnLine Analytical Processing) - 온라인 분석 처리

OLAP 와 OLTP 의 차이점 
OLTP :  현재 업무의 효율적인 처리에만 관심이 있음
OLAP : 의사결정에 도움되는 데이터 분석에 관심이 있음

oom 경험, 해결방법

memory leak, memory dump

msa써봤냐

redis 구성 어떻게 했었냐

ES5, ES6 말해봐라

closure를 설명할 수 있는 코드 짜봐라

람다 Functional Interface 종류 말해봐라

mysql innodb myisam 차이

tomcat gc 튜닝 




500개의 서버를 주겠다. 배포관리 어떻게 할것이냐? jenkins 근데 안써봤다 -> 공부해서 사용하는데 얼마나 걸리겠냐?

2차원배열 평면에 점을 흩뿌려놨다. 외곽선을 찾고 싶은데 어떤 알고리즘으로 어떻게 찾아낼것인가 ?

-------------------------------------------------------------------------------

전략패턴

싱글톤

JPA OSIV

Java Strong, Weak, Soft Reference

L4, L7

Unix nice명령어

자바 변수 - 프리미티브, 레퍼런스 변수의 차이

오버라이딩, 오버로딩

JVM구조

GC 동작원리

프로세스랑 스레드차이

동기화란?

safe한 thread를 코딩하는방법

jdbc preparedStatement, Statement의 차이

DI

Java8 7과 차이점 - stream, optional, 람다표현식

interface default

context switching

객체지향 프로그래밍 5대원칙

metaspace pergem

udp/ tcp 차이

네트워크 keepAlive

optional이렁 interface의 default 메소드

네트워크 각 tcp app 계층의 keep alive 차이

httprequest의 리턴타입중에 청크드정체 아는지

-> 길이를 알수 없는 경우 여러 청크드로

gc를 모니터링 해야 하는 이유

old영역의. gc가 이루어지는 겅우 서버가 중단하기 때문에

db커넥션풀 사용 이유

인터페이스를 사용해야 하는 이유

스프링 기본 원칙에 대해선 이해하셔야져

멀티스레드 프로그래밍 해봣냐

hashcode와 equlas의 차이

restful api

post put 차이

serializable

 


-------------------------------------------------------------------------------

1. 프로젝트 설명
2. 자바 1.8 의 특징
3. 왜 람다를 쓰는가
4. 스트림을 왜 쓰는가
5. gc가 어떻게 동작하는가
6. gc가 멀티쓰레드로 돌면 어떨까
7. javascript 의 em3 5 6 매서드를 섞어놓으면 구분할 수 있겠는가
8. 패턴 3가지만 설명해달라.
9. 싱글턴 패턴에서 멀티쓰레드의 순서를 보장하려면 어떻게 해야할까
10. 이직사유
11. 지원동기
12. 관심 직무
13. 만약 전환이 안된다면?
14. 만약 본인이 팀장이라면 어떻게 이끌것인가?
15. jvm 메모리 구조
16. msa를 어떻게 할 생각인가
17. 타임아웃으로 msa를 할 경우  생기는 문제를 어떻게 할 것인가
18. 큐로 msa를 할경우 실패를 어떻게 처리할 것인가
19. 지금 하고있는 프로젝트에 대해서 개선사항을 생각해보았는가
20. 어떤점이.제일 견디기 힘든가
21. msa를 할 경우 한번의 롤백이 아니라 여러 서비스에 대해 롤백이 필요할템데 어떻게 생각하는가
22. msa의 장점은 무엇인가
23. 가장 자신있는 언어
24. 현재 프로젝트에서 트랜젝션 처리를 어떻게 하였는가
25. 자바의 장점은 무엇이라고 생각하는가
26. tdd를 해보았는지와 설명


-------------------------------------------------------------------------------

객체지향 특징및 설계
jvm(gc 튜닝)
jdk8 + (람다 스트림)
thread safe
jpa
쿼리튜닝
캐쉬
git 브랜치 관리 전략
test 코드
성능 테스트
대용량 처리 
기초자료구조 및 시간복잡도
알고리즘 
tcp/ip http
비동기동기 block nonblock
msa
리팩토링
기존에 했던 업무
트러블슈팅
정적 테스트 
애자일
gcp나 aws 애저
ci cd devops
클라우드 네이티브 앱
디자인 패턴

스프링, 스프링부트, 스프링클라우드
그리고 msa에 추가해서 api g/w, service mesh, chaos engineering

SOLID 개념, 
ELK 혹은 EFK , 
JPA ,
MQ,
Akka,
REDIS