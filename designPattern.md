# 디자인 패턴
## 생성
### 추상 팩토리(Abstract Factory)
### 팩토리(Factory Method)
### 빌더(Builder)
### 프로토타입(Prototype)
### 싱글톤(Singleton)

## 구조
### 어댑터(Adapter)
### 브리지(Bridge)
### 컴퍼지트(Composite)
### 데커레이터(Decorator)
### 퍼사드(Facade)
### 플라이웨이트(Flyweight)
### 프록시(Proxy)

## 행위
### 책임 체인(Chain of Responsibility)
### 커맨드(Command)
### 인터프리터(Interpreter)
### 이터레이터(Iterator)
### 미디에이터(Mediator)
### 메멘토(Memento)
### 옵저버(Observer)
### 상태(State)
### 전략(Strategy)
### 템플릿메소드(Template Method)
### 비지터(Visitor)

# J2EE Pattern
### Intercepting Filter 패턴
* 요청 타입에 따라 다른 처리를 하기 위한 패턴

### Front Controller 패턴
* 요청 전후에 처리하기 위한 컨트롤러를 지정하는 패턴

### View Helper 패턴
* 프로젠테이션 로직과 상관 없는 비지니스 로직을 헬퍼로 지정하는 패턴

### Composite View 패턴
* 최소 단위의 하위 컴포넌트를 분리하여 화면을 구성하는 패턴

### Service to Worker 패턴
* Front Controller와 View Helper 사이에 디스패처를 두어 조합하는 패턴

### Dispatcher View 패턴
* Front Controller와 View Helper로 디스패처 컴포넌트를 형성, 뷰 처리가 종료될 때까지 다른 활동을 지연한다는 점이 Service to Worker 패턴과 다름

### Business Delegate 패턴
* 비즈니스 서비스 접근을 캡슐화하는 패턴

### Service Locator 패턴
*  서비스와 컴포넌트 검색을 쉽게 하는 패턴

### Session Facade 패턴
* 비즈니스 티어 컴포넌트를 캡슐화하고, 원격 클라이언트에서 접근할 수 있는 서비스를 제공하는 패턴

### Composite Entity 패턴
*  로컬 엔티티 빈과 POJO를 이용하여 큰 단위의 엔티티 객체를 구현

### Transfer Object 패턴
* 일명 Value Object 패턴이라고 많이 알려져 있음 데이터를 전송하기 위한 객체에 대한 패턴

### Transfer Object Assembler 패턴
* 하나의 Transfer Object로 모든 타입 데이터를 처리할 수 없으모로, 여러 Transfer Object를 조합하거나 변형한 객체를 생성하여 사용하는 패턴

### Value List Handler 패턴
* 데이터 조회를 처리하고 결과를 임시 저장하며, 결과 집합을 검색하여 필요한 항목을 선택하는 역할을 수행

### Data Access Object 패턴
* 일명 DAO라고 많이 알려져 있음, DB에 접근을 전담하는 클래스를 추상화하고 갭슐화 한다.

### Service Activator 패턴
* 비동기적 호출을 처리하기 위한 패턴