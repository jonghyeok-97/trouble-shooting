# Process Memory Model

----
* 프로세스마다 가상메모리로 부터 메모리를 할당받는다.
* 할당 받은 메모리(프로세스)에 `Stack, Heap, TEXT영역, GVAR/BSS영역`이 있다.
  * TEXT영역은 코드, 제어문, 상수를 포함하며 로딩되면 바뀌지 않는다.
    * 다만, JVM은 TEXT영역이 없다.
  * GVAR/BSS 에는 전역변수가 저장된다.

## 프로세스 메모리의 구성 요소
### Stack
#### `Stack Frame`
* **각 함수 호출마다 생성**되는 메모리 블록으로 함수의 **지역 변수**, **매개변수**, **반환 주소**가 있다.
```angular2html
  함수 A가 함수 B를 호출했을 때의 스택 프레임 구성.
  |----------------------|
  | function B's locals  |  <-- function B의 로컬 변수와 매개변수
  |----------------------|
  | return address       |  <-- function A로 돌아가기 위한 주소
  |----------------------|
  | function A's locals  |  <-- function A의 로컬 변수와 매개변수
  |----------------------|
```
#### `Call Stack`
* 여러 개의 Stack Frame 으로 구성됨.
#### `Stack Pointer`
* Call Stack의 최상단을 가리키는 CPU 레지스터로, CPU가 이 레지스터의 값으로 Call Stack에 Stack Frame 을 추가하거나 제거한다.
#### `Pointer`
* Stack Frame 에 저장되어있는 변수로 특정 힙의 메모리 주소를 저장하고 있다.
* 포인터란 개념은 스택,힙에 국한된 것이 아니라 페이지테이블 등 다양한 영역에서 사용됩니다.
  * ex) 프로세서(CPU)가 포인터를 이용해서 메모리(가상메모리)에 접근도 가능합니다.

## 기타
### MMU(Memory Management Unit)
* 마이크로프로세서(CPU와 메모리 및 IO가 같이 패키징되어있지 않는 칩)에 있는 복잡한 하드웨어.
* MMU의 시스템은 **가상주소**와 **물리주소**를 구분하여, 가상메모리의 가상주소를 물리메모리(RAM)의 물리주소로 매핑한다.

### 캐시메모리
* 자주 사용되거나 최근에 사용된 데이터를 저장하는 곳
* CPU와 주 메모리 사이나, CPU내부에 존재합니다.
* 레지스터보다는 느리지만, RAM보다는 빠릅니다.
* 종류에는 L1, L2, L3캐시가 있으며, L1으로 갈수록 속도는 빠르지만, 데이터를 저장할 용량이 작습니다.

### JDK 11이상의 MetaSpace
* 네이티브 메모리를 사용함 -> OS가 관리하는 힙.
* 네이티브 메모리를 사용하는 공간이 계속 커지면 OS가 데이터를 RAM에서 가상 메모리로 옮겨 애플리케이션 속도를 늦출 수 있음.

### GB와 GiB
* GB 는 10진수, GiB 는 2진수를 뜻함.

#### code패키지 설명
* 프로세스의 메모리 중에서 힙과 스택 영역만 구현했습니다.
* 구현 요구사항을 코드스쿼드 미션을 참고하였습니다.

