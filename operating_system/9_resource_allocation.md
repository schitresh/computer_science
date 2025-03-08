## Deadlock
- Situation where a set of processes are blocked because
  - Each process is holding a resource
  - And waiting for another resource acquired by some other process
- Example: P1 has R1 & waiting for R2 and P2 has R2 & waiting for R1
- Safe State: In which deadlock doesn't occur
- Deadlock Conditions: all four occur simultaneously
  - Mutual Exclusion: Two or more resources are non-shareable (only one process can use at a time)
  - Hold and Wait: A process is holding at least one resource and waiting for other resources at the same time
  - No Preemption: A resource cannot be taken away from a process unless the process releases it
  - Circular Wait: A set of processes waiting on each other in circular form
- Deadlock Handling Mechanisms
  - Prevention
  - Avoidance
  - Detection and Recovery
  - Ignorance

## Livelock
- When two or more processes continually repeat the same interaction
  - In response to changes in other processes without doing any useful work
- All processes are in running concurrently while in deadlock they are in waiting state

## Deadlock Prevention
- Achieved by solving or avoiding one of the four conditions
- Mutual Exclusion
  - May not be possible since some resources are inherently non-shareable (like printer)
- Hold and Wait
  - Allocate all resources at the start and release at the end of the process
  - Will lead to low utilization since other processes can't use it
  - May lead to starvation
- Preemption
  - Preempt the resources when required by high priority process
- Circular wait
  - Assign priority number to each resource
  - Process can't request a lesser priority resource, i.e. a resource being used by other process

## Deadlock Avoidance
- Checking if system is in safe state at every step
- Request for resource will be granted only for safe state
- If it is in unsafe state, OS will backtrack one step
- Ensure that all information about resources is known before the execution (Resource allocation state)
  - Available and allocated resources
  - Maximum resources demanded by the processes
  - Limitation: Process may not use all the resources demanded initially
- Achieves correctness of data but decreases performance
- Banker's algorithm is used

### Resource Allocation Graph (RAG)
- Process: circles
- Resources: rectangles, number of instances are denoted by dots
- Requesting: arrow from P to R,
- Allocated: arrow from R to P
- It's a deadlock if a cycle forms
  - If a resource has multiple instance, there must be that many cycles for deadlock

### Banker's algorithm
- Used in banking system to check if a loan can be sanctioned to a person
- Resource allocation and deadlock avoidance
- Input for resources: Maximum requirement, Allocated, Available, Requested
- Allows a request only if there's a safe state
  - Requested resources <= Max required resources
  - Requested resources <= Available resources
- Timeouts can be implemented to avoid deadlocks
- Example
  - There are 4 resources: [A B C D]
  - Total: [2 6 3 4]
  - Available: [1 3 1 0]
  - Allocated: [1 3 2 4]
    - P1 = [1 2 1 2]
    - P2 = [0 1 3 2]
  - Max:
    - P1 = [2 2 2 3]
    - P2 = [0 1 5 3]
  - Needed: Max - Allocated
    - P1 = [1 0 1 1]
    - P2 = [0 0 2 1]

## Deadlock Detection and Recovery
- Periodically check if deadlock occurred
- Detect deadlock
  - Resource Allocation Graph (complicated for multiple instanced resources)
  - Banker's Algorithm
  - System Modeling: Mathematical model of the system and states
  - Timestamping: If any process is waiting for a resource held by a process with lower timestamp
- Manual Intervention
  - Inform the operator and let them handle manually
- Automatic Recovery
  - Preempt the resources
  - Rollback to previous safe state
  - Abort all the processes: Computations may be lost
  - Abort one process at at time: The process can be selected based on
    - Priority, progress, process type, resources consumed, resources required
    - Only one process should not be targeted repeateadly which may cause starvation

## Deadlock Ignorance
- If deadlock is very rare, let it happen and reboot the system
- For normal users, windows, linux
- Performance will decrease if it uses deadlock mechanism

## Resource Allocation Techniques
- Resource Pool
  - There is a common pool of resources
- Resource Partitioning
  - OS decides beforehand about what resources should be allocated to which process
  - Divides resources to many resource partitions which are allocated as such
  - A resource table records the partition and its current allocation status
  - If a partition contains more resources than required, then they are wasted

## Deadlock in Distributed Systems
- In distributed systems, deadlock can neither be prevented or avoided
- Only deadlock detection can be implemented
- Approaches
  - Centralized: Only one responsible node to detect deadlock
    - But can lead to excessive workload on one node and single point of failure
  - Distributed: Different nodes work together to detect deadlock
  - Hierarchical: Most advantageous with combination of centralized and distributed approaches
    - Selected nodes are responsible for deadlock detection which are controlled by a single node
