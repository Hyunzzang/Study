## Package naming 규칙
### Java Convension을 따른다
* 국가 / 회사 / 프로젝트 명이 먼저 정의되어야 한다.
* 예) kr.co.tmon.air
* 단 회사의 경우 굳이 co를 넣을 필요 없을 때에는  생략 가능

### 하위 package 명은 layer에 따라 명명

### Class 명명 규칙
* 각 Layer의 기능을 접미사를 둔다 (PacalCase)
* Controller : UserController, MapController
* Service : UserService, MapService
* DAO : UserDao(UserRepository), MapDao(MapRepository)
* Model : User, Map(vo를 붙일 필요 없음)
* DTO : UserDTO, MapDTO
* Utiltiy classes : ~Utils(StringUtils), ~Tool, ~s(Strings), Ex(StringEx)

#### Design Patterns 을 구현한 경우, 그 명칭을 활용
* ~Builder(Builder 패턴)
* ~Decorator(Decorator 패턴)
* ~Facade(Facade 패턴)
* ~Provider(Provider 패턴)
* ~Factory(Factory 패턴)

#### Business 업무를 표현하는 방식
* ~Aggregator(집계)
* ~Extractor(추출)
* ~Job(일반적인 작업을 Job, Task, Work로 많이 표현)
* ~Manager(작업들을 관리하는 기능)

### Interface / Class 간 명명규칙
* Java의 대표적인 Interface 명
  *  Serializable, Comparable(~할수 있다)
  *  Iterator, Serializer(~or --하는 자)
* Interface 를 구현하는 Class는
  * 목적구분용 명칭 + Interface 명 + Impi(꼭 이 규칙을 쓰지 않음)

### 메소드 명명 규칙
* 영어식 표현으로 (camelCase)
  * 동사 + 목적어 형식 (doJob(), executeJob(), makeUser(), newUser())
  * 전치사를 적극 활용해라
    * at / on / in / out, from-to, until, since, for, ago ...
    * up / down / on / off / over / under / through / into ...
    * by / with ...
* 메소드 명에서 인자형식 및 반환 형식을 추측
  * 예)
    * public User **find**ByName(String name)
    * public boolean **is**ActiveUser(User user)
  * can~, exists~, is~ 등은 boolean 을 반환
  * check~, assert~, validate~ 는 void 형이지만, 내부에서 예외 발생 시켜 처리

### Field 명명 규칙
* 일반 변수는 camel case
  * private boolean running -> public boolean isRuning()
  * private int age -> public int getAge()
* 한번 설정되어 바꿀 수 없다면 final을 지정
  * private final String companyName
* 상수에 해당하는 것은 대문자와 '_'를 조합
  * public static final int PAGE_SIZE = 10

### Enum 명명 규치
* 기본적으로 상수 명명규칙과 같음(요즘 Class 명명규칙을 사용하기도 함)

### 코드 구현
* 발생한 예외를 무시할 경우에는 'ignored'로 무시함을 표현해라
* 예)
  '''{.java}
  try {
    thread.join()
  } catch(Exception ignored) {
      log.debug("ignored로 명명하여 특별한 에러 처리시 없이 무시함을 표현한자.");
  }
  '''

* switch 구문에서는 꼭 default 를 이용하여, 처리되지 않는 case가 없도록 하자.
  * default 문에 특별히 처리 할게 없을 때에는 NotsupporedException 같은 예외 처리로
* static method 만 있는 static calss 는 private 생성자를 정의 하여 클래스가 인스턴스 생성 안도록 하자.
* Abstract class의 생성자는 protected 로 선언해라. 상속받는 concrete class에서 public constructor 를 정의 한다.


