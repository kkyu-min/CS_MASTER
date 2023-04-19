# Garbage Collection 개요

GC란 힙에서 더이상 참조되지 않는(사용되지 않는) 객체를 제거하는 것이다.  
자바에서 GC에 대해서 공식문서에서는 Automatic Garbage Collection 라고 소개하고 있다. 즉, 자동으로 GC가 이루어진다.  
사실 메모리를 직접적으로 다루지 않음으로써 섬세한 메모리 관리는 불가능하지만, 이는 워낙 low level이고 개발자가 자주 실수하는 부분이므로 실수를 줄여준다는 장점이 있다.

### GC의 두가지 원칙
1. 반드시 모든 Garbage를 수집 해야한다.
2. 살아있는 객체(참조 가능한 객체)는 절대로 수집하면 안 된다.

### Mark and Sweep
자바의 GC 기본 알고리즘은 Mark and Sweep이다.  
Mark and Sweep 과정
1. JAVA 객체가 힙에 생성되면 0(또는 false)의 값을 가지는 마크 비트를 가진다.
2. Mark 단계에서 가비지 컬렉터는 root(메모리 풀 외부에서 내부를 가리키는 포인터)에서 시작하여 객체 트리를 순회함. 루트에서 객체에 도달할 수 있으면 마크 비트가 1(또는 true)로 설정됨
3. Sweep 단계에서 가비지 컬렉터는 힙을 순회하면서 마크 비트가 0(false)인 모든 항목에 대해서 메모리를 회수한다.

### 가비지 컬렉션 수행 시점
힙에서 가비지 컬렉션이 발생하는 조건은 각각의 환경에 따라 다르지만, 크게 아래의 조건을 따른다.
1. Allocation Failure(할당 실패) : 사용 가능한 공간이 부족하여 힙에 객체를 할당할 수 없는 경우, JVM은 GC를 수행함.
2. Heap Size : 힙이 특정 임계값에 도달하면 JVM은 가비지 컬렉션을 수행하여 메모리를 회수해 OutOfMemoryError를 방지함.
3. 강제 호출 : System.gc(), Runtime.getRuntime().gc()로 강제로 gc를 수행함(gc가 발생한다고 보장할 수 없음)
4. 시간 : 일부 GC 알고리즘은 시간에 기반하여 GC를 수행함.

### Weak Generational Hypothesis
여러 소프트웨어에서 객체 수명은 이원적 양상을 보이는데, 대부분의 객체는 매우 짧은 시간만 살아있고 나머지 객체들은 기대 수명이 훨씬 길다는 것이다.  
이러한 경험을 토대로 GC는 젋은 객체를 빠르게 수집해야 하고, 늙은 객체와 뗴어 놓는 것이 좋다는 것이라는 결론이 나왔다.

### Young Generation
위에서의 가설에 따라, 단명하는 객체들을 모아놓은 공간이다. 대부분의 객체가 이곳에서 소멸되고 새로 객체가 할당되기 때문에 GC가 자주 일어나는 공간이다.  
자바에서 GC가 일어나는 동안에, GC를 수행하는 스레드를 제외한 모든 스레드가 멈추는 'Stop the World' 가 자주 발생하므로 이곳의 GC는 수행 시간이 짧아야만 한다.
수행 시간이 짧아야 하므로, 수거해가는 객체의 수와 영역의 사이즈가 Old Generation에 비해 작다. (수행 시간이 짧으므로 Minor GC라고 부르는듯)  
Eden Space와 Survivor Space로 나뉜다.

Eden Space : 새로운 객체가 생성되는 메모리 풀(Eden Space보다 용량이 큰 객체는 다른 영역에 할당 됨). 이 공간이 가득 차면 가비지 컬렉터는 참조되지 않는 객체를 제거하거나(Minor GC) 사용중인 경우 Survivor space에 저장한다.
Survivor Space : Eden 영역의 GC로 인해 발생하는 오버헤드를 줄이고자 생긴 영역. From과 to라는 두 개의 공간으로 나뉘며 0, 1로도 구분한다. Eden Space보다 공간이 훨씬 작다.

### Minor GC
그럼 이제 Young Generation에서 발생하는 Minor GC에 대해서 생각해보자.
1. 새롭게 생성된 객체는 Eden Space에 할당된다. 이 때 객체의 나이(generational count)는 0이다.
2. 이 때, Eden Space에 공간이 없다면 Minor GC를 수행하게 된다. Stop the World가 발생한다.
3. Eden 영역에 할당된 객체를 순회하면서 root로 부터 접근 가능한 객체를 Mark한다 (마크비트를 1로 변경)
4. 생존한 모든 객체들은 나이가 1 증가하면서(aging) Survivor Space로 복사된다.
5. Eden space를 Sweep한다.
6. 위의 과정을 반복한다.
7. 그러다가, Survivor Space도 가득 차서 복사가 불가능하다면 From 공간에 있는 객체들을 To로 옮기고, Eden Space에서 생존한 객체들을 To로 옮겨준다.
8. 그 뒤에 From과 To의 이름을 바꾼다.
9. 그러다가, 어느정도 aging이 진행 된 객체는 Promotion하여 Old Generation으로 이동한다.

### Old Generation
수명이 긴 객체가 저장되는 공간이다. 특정 횟수의 가비지 컬렉션에서 살아남은 경우 결국 이 공간으로 이동한다. Tenured space라고도 부른다.  
앞에서의 가설에 의해 이 공간은 Young Generation보다 훨씬 크며, GC 발생 횟수가 더 적다.

### Major GC
Old Generation이 꽉 찼을 때 수행되는 GC이다. 기본적으로 이 공간의 메모리 할당률이 낮기 때문에 빈도가 적지만, Young Generation보다 훨씬 크기 때문에 GC의 수행 시간이 길다.

### Full GC
Minor GC와 Major GC가 같이 발생하는 것을 Full GC라고 부른다. (힙 전체에서 실행)

### Major GC와 Full GC의 알고리즘
Serial GC: 단일 스레드로 작동하는 GC이다. Old 영역에서만 사용된다. Minor GC에서는 Mark-Sweep-Compact 알고리즘이 사용되고, Major GC에서는 Mark-Sweep 알고리즘이 사용된다.

Parallel GC: Serial GC와 유사하지만 멀티 스레드를 사용하여 처리 속도를 높인다. Old 영역에서만 사용된다. Minor GC에서는 Mark-Summary-Compact 알고리즘이 사용되고, Major GC에서는 Mark-Summary-Compact와 Mark-Sweep-Compact 알고리즘이 사용된다.

CMS GC: Conncurrent Mark and Sweep GC로, Old 영역에서 작동하면서 멀티 스레드를 사용하여 작업을 병렬로 처리한다. 이 GC는 적은 일시 중지 시간을 가지고 있지만 메모리 단편화 문제가 발생할 수 있다.

G1 GC: Garbage First GC로, Heap 전체를 세그먼트로 분할하여 각 세그먼트를 병렬로 처리한다. 이 GC는 작은 크기의 세그먼트에서 작업을 수행하므로, 일시 중지 시간을 줄일 수 있다.

(너무 방대하고 어려운 내용이라 공부를 좀 더 하고 다시 써야할 듯...)
