Виды репликации:

- Master-Slave
- Tree
- Master-Master
- Buddy-replication

Виды репликации:

- Active (Push)
- Passive (Pull)
    - Data not available, read it from peer, store locally
    - Works well with timeout-based caches. ==Why?==

# Designing Data-Intensive Applications

Reliability (works correctly in the face of faults and user errors), Scalability, Maintainability.

AWS VMs sometimes become unavailable: flexibility and elasticity over single-machine reliability.

# Foundations of Data systems

## Ch 1. Reliable, Scalable, and Maintainable Applications

_Reliability_ means making systems work correctly, even when faults occur. _Scalability_ means having strategies for keeping performance good, even when load  
increases.  

### Scalability

In order to discuss scalability, we first need ways of describing load and performance quantitatively.

Какими параметрами можно описать performance?

Head of line blocking — когда сервер занят обработкой медленных запросов, а другие, возможно более быстрые, ждут в очереди.

Tail latency amplification — if an end-user request requires multiple backend calls. В итоге в целом для пользователей latency увеличивается.

Scaling up = vertical scaling. Scaling out = horizontal scaling. Compromise: several fairly powerful machines.

Elastic: can automatically add computing resources when they detect a load increase.

Different systems - different architecture - different common operations (assumptions).

### Maintainability

3 principles:

- Operability (smooth operation)
    - Operations team responsibilities
        - Monitoring health, restoring the service in case of fault
        - Tracking down failures, performance problems
        - Updates, patches
        - Capacity planning, anticipating future problems
        - Establishing good practices, tools
        - Complex maintenance, e.g. moving from one platform to another
        - Preserving knowledge about the system
- Simplicity (engineers inderstanding). There may be accidental complexity. Way to reduce: abstraction
- Evolvability/Extesibility.

## Ch 2. Data Models and Query Languages

### Relational Model vs Object Model

Object–relational impedance mismatch

RDMS: joins are easy, Document DBs: join support is often weak