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


# 자료구조
## list
## set
## map
## 이진트리

# 알고리즘
## Bubble sort
* 두 인접한 원소를 검사하여 정렬하는 방법
* 시간 복잡도가 O(n^{2})로 상당히 느리지만, 코드가 단순하기 때문에 자주 사용

## insertion sort
* 자료 배열의 모든 요소를 앞에서부터 차례대로 이미 정렬된 배열 부분과 비교하여, 자신의 위치를 찾아 삽입함으로써 정렬을 완성하는 알고리즘