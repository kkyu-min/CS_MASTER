# GC가 무엇인지, 필요한 이유는 무엇인지, 동작방식에 대해 설명해주세요.

1. 동적으로 할당했던 메모리 영역 중 필요 없게 된 영역을 알아서 해제

장점

1. 메모리 누수
2. 해제된 메모리에 접근
3. 이중 해제를 막을 수 있다

단점

1. GC 작업 자체가 오버헤드
2. GC가 언제 메모리를 해제하느지 모름 → 실시간성이 중요한 프로그램이면 안함

GC 알고리즘

1. Reference Counting

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c9147d0f-82f5-43cd-beb5-cddcd1ee4f5a/Untitled.png)

→ 순환 참조 발생 가능

1. Mark ans Sweep

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a5a23944-ecd0-4e55-82e6-cc75028aa890/Untitled.png)

reachable : 

unreachable : 

compaction : 

→ 의도적으로 GC를 실행시켜야 한다.

→ 어플리케이션 실행과 GC 실행이 병행된다.

1. Root Space의 위치
- stack의 로컬 변수
- method area에 저장된 static 변수
- Native method stack의 C/C++로 작성된 JNI 참조
- JNI
    
    [https://mommoo.tistory.com/71](https://mommoo.tistory.com/71)
    

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/2583f88c-3671-4930-9b62-a297b2b552af/Untitled.png)

1. JVM의 HEAP 영역
    1. Young generation : minor GC
    2. Old generation : magor GC