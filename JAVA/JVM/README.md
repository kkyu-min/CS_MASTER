# JVM의 구조와 java의 실행방식을 설명해주세요

## JVM

<aside>
💡 자바 프로그램 실행환경을 만들어 주는 소프트웨어

</aside>

- 역할
    1. 자바 바이너리 코드(.class) 를 읽는다
    2. 자바 바이너리 코드를 검증한다.
    3. 자바 바이너리 코드를 실행한다.
- JAVA가 플랫폼에 영향을 받지 않게 해준다.
- JVM은 플랫폼에 종속적
- JVM은 바이트코드를 명령어 단위로 읽어서 해석

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/1c4fbd26-83ce-4379-b1a3-adf28f7a9c9b/Untitled.png)

### JVM 동작 방식

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/eb2f72f6-61dd-4a01-90ed-f00af616cac2/Untitled.png)

1. Class Loader : 
- 실행 시점에서 클래스 파일을 로딩 하게 도와줍니다. 로딩은 실행하도록 도와준다고 이해하시면 더 쉽겠네요.
- 바이트코드를 읽고, 클래스 정보를 메모리의 heap/method Area에 저장
1. Runtime Data Access  : 메모리에 관련된 부분으로서 위에서 메모리에 적재를 받는 공간안에 PC레지스트, Stack 영역, Method 영역, heap 영역, 네이티브 메소드 스택 등 5개의 영역으로 나눠진다고 이해하시면 됩니다.
    1. **Method Area**: 클래스정보, 변수정보, Method정보, static변수정보, 상수정보 등이 저장되는 영역. `모든 Thread가` 공유한다.(클래스의 멤버 변수, 데이터 타입, 접근 제어자, constant Pool, static변수, final class), 
        1. 프로그램의 클래스 구조를 메타 데이터처럼 가지고 있고, 메서드의 코드들을 저장
    2. **Heap Area**: new 명령어로 생성된 인스턴스와 객체가 저장되는 구역, **Garbage Collection 이슈는 이 영역에서 일어난다**. `모든 Thread`가 공유한다.(지역변수, 파라미터, 리턴 값, 연산)
    3. **Stack Area**: Method 안에서 사용되는 값들(매개변수, 지역변수, 리턴값 등)이 저장되는 구역. 메소드가 호출될 때 LIFO로 하나씩 생성되고, 메소드 실행이 완료되면 LIFO로 하나씩 지워진다. 각 `Thread별로` 하나씩 생성된다.
        1. 메서드 호출을 스택 프레임이라는 블록으로 쌓으며, 로컬 변수 중간 연산 결과 들이 저장되는 영역
    4. **PC Register Area**: CPU의 Register와 역할이 비슷하다. 현재 수행 중인 JVM 명령의 주소값이 저장된다. `각 Thread별로` 하나씩 생성된다.
        1. 쓰레드가 현재 실행할 스택 프레임 주소 저장
    5. **Native Method Stack**: 다른 언어(C/C++등)의 메소드 호출을 위해 할당되는 구역 언어에 맞게 Stack이 형성되는 구역이다. `각 Thread별로` 하나씩 생성된다.
        1. 로우 레벨 코드를 실행하는 스택
2. ExecutionEngine : 이것은 실제 실행을 시키는데 실질적인 도움이 되는 영역입니다.
    - 바이트 코드를 네이티브 코드로 변환
    - GC를 실행됨
    - Interpreter : 바이트코드를 한 줄씩 해석, 실행하는 방식(초기방식, 속도가 느리다)
    - JIT : 실제 실행하는 시점에 각 OS에 맞는 Native COde로 변환하여 실행 속도 개선
        
        ⇒ JVM은 모든 코드를 JIT 컴파일러 방식으로 실행하지 않고, 인터프리터 방식을 사용하다가 일정 기준이 넘어가면 JIT 컴파일 방식으로 명령어를 실행합니다.
        
        - 동작원리
            
            JIT 컴파일러는 같은 코드를 매번 해석하지 않고, 실행할 때 컴파일을 하면서 해당 코드를 캐싱해버립니다. 이후에는 바뀐 부분만 컴파일하고, 나머지는 캐싱된 코드를 사용합니다. 이렇게 JIT 컴파일러는 운영체제에 맞게 바이트 실행 코드로 한 번에 변환하여 실행하기 때문에 이전의 자바 해석기(Java interpreter) 방식보다 성능이 10배 ~ 20배 정도 더 좋습니다.
            

## JRE와 JDK

### JRE(****Java Runtime Environment)****

- 자바로 만들어진 프로그램을 `실행`시키는데 필요한 라이브러리 각종 API, JVM이 포함되어있다.

### JDK(Java Development Kit)

- 개발자들이 자바로 `개발`하는 데 사용됩니다.
 JDK안에는 개발 시 필요한 라이브러리들과 javac, javadoc 등의 개발 도구들을 포함되어 있고 개발을 하려면 당연히 실행도 시켜줘야 하기 때문에 JRE (Java Runtime Environment)도 함께 포함되어 있습니다

*※ 정리하자면 Java로 프로그램을 직접 개발하려면 JDK가 필요하고 Java로 만들어진 프로그램을 실행시키려면 JRE가 필요합니다.*

## 참조