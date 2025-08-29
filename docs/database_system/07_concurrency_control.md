# Concurrency Control
- To increase throughput and efficiency of the system
  - Concurrent schedules & transactions are used
- Concurrency Control Protocols
  - Set of rules maintained to solve the concurrency control problems
  - Ensures that schedules are serializable, recoverable and maybe cascadeless
- Categories of protocols
  - Lock Based
  - Graph Based
  - Timestamp Ordering
  - Multiple Granularity
  - Multi-version

## Concurrency Problems
### Dirty Read Problem (Write Read Conflict)
- When one transaction updates an item but it fails to commit later
- Meanwhile, another transaction reads the updated value, creating an inconsistency
- Example
  - T1 modifies database without committing the changes
  - T2 reads the uncommitted data by T1
  - T1 performs rollback
- To prevent them, SQL provides transaction isolation levels as discussed below

### Lost Update Problem
- When two or more transactions modify the same data resulting in overwritten or lost updated data
- Example
  - T1 reads value of an item from the database
  - T2 starts and reads the same database item
  - T1 updates the value and performs a commit
  - T2 updates the same item based on the initial read and performs a commit
  - Update committed by T1 gets overwritten by T2

### Non-repeatable Read
- When a transaction reads the same row twice and gets a different value each time
- This happens if another transaction updates the value between the two reads

### Phantom Read
- When a transaction executes a query twice but it retrieves different rows
- This happens if another transaction adds new rows that match the search criteria

### Isolation Levels
- These specify how transactions should be isolated from one another
  - Prevents the concurrency problems
  - The choice of isolation level depends on specific requirements
- Higher isolation offers stronger data consistency
  - But longer lock times and increased contention
  - Leading to decreased concurrency and perrformance
- Read Uncommitted
  - Allows to read uncommitted data from other transactions
  - Can lead to dirty reads, non-repeatable reads, phantom reads
- Read Committed
  - Allows to read only committed data (prevents dirty reads)
  - Transaction holds a lock on the current row
    - And prevents operations from other transactions
- Repeatable Read
  - Ensures that a transaction always reads the same data for a given query
  - Even if other transactions modify the data in the meantime
  - Prevents dirty reads and non-repeatable reads
  - Transaction holds read locks on the referencing rows
    - And write locks on the referenced rows
- Serializable
  - Ensures that transactions are executed serially
  - Provides highest level of isolation
  - Prevents dirty reads, non-repeatable reads, phantom reads

## Starvation
- When transaction is not able to get the required resources
  - And is continuously delayed or blocked
  - This happens when other transactions are given priority
- Causes
  - Waiting scheme for locked items is unfair (maybe priority queue)
  - The same transaction is selected as victim repeatedly
  - Resource leak
  - Denial of service attack
- Solutions
  - Increasing priority
  - Modify victim selection algorithm
  - First come first serve
  - Wait die and wound wait schemes
  - Timeout the waiting transaction after a certain amount of time
  - Resource Reservation: Start execution only when all resources are allocated
  - Preemption
  - Dynamic lock allocation by analyzing the lock requests
  - Parallelism

## Deadlock
- When two or more transactions are waiting for each other to release resources
- Both transactions require the lock being hold by the other and none can proceed
- Conditions
  - Mutual exclusion
  - Hold and wait
  - No preemption
  - Circular wait
- Avoidance
  - Suitable for smaller database
  - Aquire locks in the same order, wait for the previous transaction
- Detection
  - Draw a wait for graph and check if there is a cycle
- Prevention
  - Suitable for larger databases
  - Wait die
  - Wound wait
  - Discussed in detail in timestamp ordering protocol
