# 반응형 프로그래밍이란?
반응형 프로그래밍은 데이터의 흐름과 변화에 반응하는 프로그래밍 패러다임입니다. 이는 이벤트 기반 시스템에서 유용하며, 데이터의 변경이 발생할 때마다 이를 감지하고 자동으로 업데이트를 수행합니다. 반응형 프로그래밍은 비동기적이며, 주로 사용자 인터페이스, 실시간 데이터 처리, 네트워크 요청 등에서 사용됩니다.

# Reactor 소개
* Reactor: 스프링에서 제공하는 반응형 프로그래밍 라이브러리입니다. Project Reactor는 Reactive Streams 표준을 구현하며, 비동기 데이터 스트림을 효율적으로 다루기 위한 다양한 연산자와 기능을 제공합니다.
* Flux: 0개 이상의 데이터를 방출하는 비동기 스트림입니다.
* Mono: 0개 또는 1개의 데이터를 방출하는 비동기 스트림입니다.
* Scheduler: 스레드 풀과 유사한 개념으로, 비동기 작업을 실행할 스레드를 관리합니다.

## 스트림 생성 방법
* just(): 단일 값을 포함하는 스트림을 생성합니다.
* generate(): 값을 반복적으로 생성하는 스트림을 만듭니다.
* create(): 스트림을 수동으로 생성하고 값을 발행합니다.
* fromCallable(): Callable을 사용하여 값을 비동기적으로 생성합니다.
* fromStream(): Java의 Stream을 Reactor의 Flux로 변환합니다.

## lazy
* React 애플리케이션에서 동적으로 로딩되는 컴포넌트를 생성하기 위한 API입니다. 코드 분할을 쉽게 구현할 수 있어 초기 로딩 시간을 줄일 수 있습니다.
* 스트림이 소비도기 전까지는 데이터 생성이나 처리가 수행되지 않습니다.

## Hot vs Cold
* Hot 스트림: 구독 시점에 관계없이 데이터를 방출하는 스트림입니다. 
    - 무언가를 새로 시작하지 않는
* Cold 스트림: 구독 시점에 데이터를 처음부터 방출하는 스트림입니다. (예: 파일 읽기)
    - 무언가를 새로 시작

## 기본 연산자
* map(): 각 요소에 대해 주어진 함수를 적용하여 새로운 요소를 생성합니다.
```java
Flux<Integer> numbers = Flux.just(1, 2, 3, 4);
Flux<Integer> squares = numbers.map(n -> n * n);
squares.subscribe(System.out::println);
```

* filter(): 조건을 만족하는 요소만을 남깁니다.
```java
Flux<Integer> numbers = Flux.just(1, 2, 3, 4);
Flux<Integer> evenNumbers = numbers.filter(n -> n % 2 == 0);
evenNumbers.subscribe(System.out::println);
```

* filterWhen(): 비동기 조건을 기반으로 필터링합니다.
```java
Flux<Integer> numbers = Flux.just(1, 2, 3, 4);
Flux<Integer> evenNumbers = numbers.filterWhen(n -> Mono.just(n % 2 == 0));
evenNumbers.subscribe(System.out::println); 
```

* flatMap(): 각 요소를 다른 스트림으로 변환하고, 이들을 병합합니다.
```java
Flux<String> words = Flux.just("hello", "world");
Flux<String> letters = words.flatMap(word -> Flux.fromArray(word.split("")));
letters.subscribe(System.out::println);
```

* handle(): 요소를 처리하고, 조건에 따라 새로운 요소를 생성합니다.
```java
Flux<Integer> numbers = Flux.just(1, 2, 3, 4);
Flux<String> result = numbers.handle((number, sink) -> {
    if (number % 2 == 0) {
        sink.next("Even: " + number);
    }
});
result.subscribe(System.out::println);
```

* take(): 처음 n개의 요소만을 취합니다.
```java
Flux<Integer> numbers = Flux.range(1, 10);
Flux<Integer> firstThree = numbers.take(3);
firstThree.subscribe(System.out::println);
```

* skip(): 처음 n개의 요소를 건너뜁니다.
```java
Flux<Integer> numbers = Flux.range(1, 10);
Flux<Integer> afterThree = numbers.skip(3);
afterThree.subscribe(System.out::println);
```

## doOn*() 연산자
* 스트림의 다양한 시점에서 사이드 이펙트를 처리할 수 있도록 합니다. 예를 들어, doOnNext(), doOnError() 등이 있습니다.
```java
Flux<Integer> numbers = Flux.just(1, 2, 3);
numbers
    .doOnNext(n -> System.out.println("Processing: " + n))
    .subscribe(System.out::println); 
```

## 기타 연산자
* window(): 스트림을 여러 개의 작은 스트림으로 나눕니다.
```java
Flux<Integer> numbers = Flux.range(1, 10);
Flux<Flux<Integer>> windows = numbers.window(3);
windows.flatMap(seq -> seq.collectList()).subscribe(System.out::println);
// 출력: [1, 2, 3], [4, 5, 6], [7, 8, 9], [10]
```

* buffer(): 요소들을 모아서 리스트로 만듭니다.
```java
Flux<Integer> numbers = Flux.range(1, 10);
Flux<List<Integer>> buffered = numbers.buffer(3);
buffered.subscribe(System.out::println);
// 출력: [1, 2, 3], [4, 5, 6], [7, 8, 9], [10]
```

* distinct(): 중복 요소를 제거합니다.
```java
Flux<Integer> numbers = Flux.just(1, 2, 2, 3, 3, 3, 4);
Flux<Integer> distinctNumbers = numbers.distinct();
distinctNumbers.subscribe(System.out::println);  
// 출력: 1, 2, 3, 4
```

* cast(): 요소의 타입을 변환합니다.
```java
Flux<Number> numbers = Flux.just(1, 2, 3);
Flux<Integer> integers = numbers.cast(Integer.class);
integers.subscribe(System.out::println);  
// 출력: 1, 2, 3
```

* ofType(): 특정 타입의 요소만을 선택합니다.
```java
Flux<Object> items = Flux.just(1, "two", 3, "four");
Flux<String> strings = items.ofType(String.class);
strings.subscribe(System.out::println);  
// 출력: two, four
```

* index(): 각 요소에 인덱스를 추가합니다.
```java
Flux<String> letters = Flux.just("a", "b", "c");
letters.index().subscribe(indexed -> System.out.println(indexed.getT1() + ": " + indexed.getT2()));
// 출력: 0: a, 1: b, 2: c
```

* timestamp(): 각 요소에 타임스탬프를 추가합니다.
```java
Flux<String> letters = Flux.just("a", "b", "c");
letters.timestamp().subscribe(ts -> System.out.println(ts.getT1() + ": " + ts.getT2()));
// 출력: [타임스탬프]: a, [타임스탬프]: b, [타임스탬프]: c
```

* elapsed(): 각 요소의 발행 간격을 측정합니다.
```java
Flux<String> letters = Flux.just("a", "b", "c").delayElements(Duration.ofMillis(100));
letters.elapsed().subscribe(elapsed -> System.out.println(elapsed.getT1() + "ms: " + elapsed.getT2()));
// 출력: 100ms: a, 100ms: b, 100ms: c (시간은 대략적인 값)
```

* zip(): 여러 스트림을 결합하여 요소를 병합합니다.
```java
Flux<String> words = Flux.just("a", "b", "c");
Flux<Integer> numbers = Flux.just(1, 2, 3);
Flux<String> zipped = Flux.zip(words, numbers, (word, number) -> word + number);
zipped.subscribe(System.out::println);  
// 출력: a1, b2, c3
```

* merge(): 여러 스트림을 하나의 스트림으로 병합합니다.
```java
Flux<String> flux1 = Flux.just("a", "b", "c");
Flux<String> flux2 = Flux.just("d", "e", "f");
Flux<String> merged = Flux.merge(flux1, flux2);
merged.subscribe(System.out::println);  
// 출력: a, b, c, d, e, f
```

## 오류 처리
* timeout(): 특정 시간 내에 데이터가 방출되지 않으면 에러를 발생시킵니다.
* retry(): 에러가 발생했을 때 스트림을 재구독합니다.
* retryBackoff(): 재시도 간에 지연 시간을 추가합니다.
* onErrorReturn(): 에러 발생 시 대체 값을 방출합니다.
* onErrorResume(): 에러 발생 시 대체 스트림을 방출합니다.
* onErrorMap(): 에러를 다른 에러로 변환합니다.

## 블로킹과 반응형, 상호 전환
* block(): Mono 또는 Flux의 결과를 동기적으로 가져옵니다. (블로킹)
* Mono.fromFuture()/Flux.fromIterable(): 블로킹 코드를 Reactor 스트림으로 변환합니다.
* publishOn(): 스트림의 다음 연산자를 특정 스케줄러에서 실행합니다.
* subscribeOn(): 스트림의 구독을 특정 스케줄러에서 실행합니다.

## 동시성 (Concurrency)과 스레드 풀 (subscribeOn(), parallel())
subscribeOn(): 스트림의 구독 및 데이터 요청을 특정 스레드 풀에서 실행합니다.
parallel(): 스트림을 병렬로 처리합니다.

## 유닛 테스트
* StepVerifier: Reactor 스트림의 동작을 검증하는 데 사용되는 유틸리티 클래스입니다.
  - expectNext(): 다음 데이터를 예상합니다.
  - expectComplete(): 스트림 완료를 예상합니다.
  - expectError(): 에러 발생을 예상합니다.
