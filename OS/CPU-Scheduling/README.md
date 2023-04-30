### CPU 스케줄링

-   선점
    어떤 프로세스가 CPU를 할당받아 실행중에 있어도 다른 프로세스가 CPU를 할당받아 작업을 처리할 수 있음

-   비선점
    선점과 반대로 한 프로세스가 CPU를 할당받아 실행중에 있으면 작업이 끝나기 전까지 다른 프로세스가 작업을 할당받지 못함

## CPU 스케줄링의 목적

-   **No starvation** : 각각의 프로세스들이 오랜시간동안 CPU를 할당받지 못하는 상황이 없도록 한다.
-   **Fairness** : 각각의 프로세스에 공평하게 CPU를 할당해준다.
-   **Balance** : Keeping all parts of the system busy

1. FCFS
   First Come First Service라는 뜻으로 준비 큐에 프로세스가 도착한 순서대로 작업을 처리함
2. SJF
   작업의 시간이 작은 순서대로 작업을 처리하는 스케쥴링 기법

    - 기아현상(Starvation)
      계속해서 CPU할당을 받지 못해서 준비 큐에 계속 남아있느 현상

3. HRN
   작업에 유리한 SJF의 단점을 보완한 알고리즘.
   오랫동안 대기하는 프로세스의 우선순위를 증가시키는 방법 (대기시간 + 서비스시간 / 서비스시간)

4. Round Robin
   각 프로세스별 동일한 CPU할당시간(Time-Quantum)만큼 작업을 진행하는 스케줄링 기법

5. MultiLevel Queue
   각 큐들이 우선순위를 지니는 여러개의 큐를 사용하는 스케줄링 기법

6. MultiLevel Feedback Queue
   각 큐들이 우선 순위를 지니고 큐 사이 프로세스들이 이동을 할 수 있음
