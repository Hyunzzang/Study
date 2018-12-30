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

<img width="" height="" src=./img/jvm.png></img>

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


* Jvm 메모리 할당 기술
  > **bump-to-pointer** </br>
  > **TLABs(Thread-Local Allocation Buffers)** </br>

스프링 ioc
스프링 컨테이너를 설계한다면?
스프링 빈의 옵션?
싱글턴 패턴의 장단점
프로토타입이란?
바이너리 서치란?
오버로딩과 오버라이딩



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

 


카카오
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