# Concurrency Control Protocols
## Lock Based Protocols
- Each transaction needs to acquire locks before accessing or modifying the data items
- Shared Lock
  - Read lock, no modification allowed
  - Allows multiple transactions to read the data simultaneously
- Exclusive Locks
  - Write lock, allows updation
  - Only one transaction can hold this lock on a data item at a time
- A transaction is allowed to upgrade or downgrade a lock if the conditions are met
- Simple lock based protocal (binary locking) don't guarantee serializability
  - Additional protocols for positioning of locking & unlocking operations are required
  - Which gives rise to two phase locking protocol
- Starvation and deadlocks are possible

### Locking
- Lock manager manages the locking requests made by transactions
- It relies on the process of message passing between transactions and lock manager
- Lock table
  - Hash table where names of data items are used as hashing index
  - Every locked data item has a linked list associated with it
  - Every node in the list represents a transaction that requested lock
    - Mode of lock requested (mutual/exclusive)
    - Current status of the request (granted/waiting)
  - Collisions are handled by separate chaining
  - A node is deleted after unlock or abort

## Two-Phase Locking Protocol
- Phases
  - Growing
    - The transaction starts acquiring locks before performing any modification to data items
    - Once a lock is acquired, it cannot be released until the end of the execution
    - Upgrading is allowed in growing phase only
  - Shrinking
    - The transaction releases all the acquired locks after all the modifications
    - Once it starts releasing the locks, it cannot acquire any locks further
    - Downgrading is allowed in shrinking phase only
- Lock Point
  - The point at which the growing phase ends
  - That is, when a transaction takes the final lock
- Cascading Rollback is possible if the dependent transaction's commit fails
- To claim an exclusive (write) lock
  - Transaction must acquire a shared (read) lock first
  - And then upgrade it to an exclusive lock
- Problems
  - Deadlock
    - Example: L1(A), L2(B), L1(B), L2(A)
      - T1 granted A, T2 granted B
      - T1 waiting for B, T2 waiting for A
  - Starvation
  - Does not ensure recoverability

### Strict 2PL Protocol
- In 2PL, transactions can release any lock before committing
- In strict 2PL, transactions can release exclusive locks only after they commit
- Recoverable, Cascadeless
- Deadlocks are possible
- Most popular version of 2PL

### Rigorous 2PL Protocol
- Transactions can release a shared or exclusive lock only after they commit
- Recoverable, Cascadeless
- Deadlocks are possible

### Conservative or Static 2PL Protocol
- The transaction should lock all the items before starting execution
  - By predeclaring its read-set and write-set
  - If any of the predeclared items cannot be locked
    - Then the transaction should not lock any of the items
    - And wait till all the items are available for locking
- Locks can be released at any time
- Not cascadeless, so does not ensure a strict schedule
- Deadlock free, since one deadlock condition (hold & wait) is nullified
- Difficult to use in practice because predeclaration is not possible in many situations

## Graph Based Protocols
- Transactions are represented as nodes in a graph
  - And the conflicts between them as edges
- If a transaction tries to acquire an exclusive lock on an item
  - And if that is already locked by another transaction
  - Then a conflict edge is added between their nodes
  - When the transaction is completed, its edges are removed
- Before granting a lock, graph is checked for any cycles
  - If a cycle exists, there is a conflict
  - And one of the transactions needs to be rolled back to break the cycle
- It can handle complex transactions better than two-phase locking
  - But it's computationally expensive
  - And may not scale well for large databases
- Tree Based Protocol
  - Simple implementation of graph based protocol
  - Data item A can be locked by T1 only if the parent of A is currently locked by T1
  - Data items can be unlocked at any time

## Multiple Granularity Locking
- Various concurrency control protocols perform synchronization on individual data items
  - If a transaction need to access the entire database
    - It will need to lock each item individually
  - This is inefficient and it would be simpler if a single lock can lock the entire database
  - But if another transaction needs to access a few data items, it should be able to do that
  - Locking the entire database in that case will result in loss of concurrency
- Granularity is the size of the data item allowed to lock
- Multiple granularity means hierarchically breaking up the database into blocks
  - That can be locked and can be tracked what needs to be locked & in what fashion
- How does the system determine if the root node can be locked
  - If it searches the entire tree, it will nullify the whole purpose of this locking scheme
  - A more efficient way is to introduce a new lock mode (intention lock)

### Representation
- It can be represented graphically as a tree. Example:
  - Root: Entire database
  - 1st Level: Areas within the database
  - 2nd Level: Files within each area (each file can have only one area)
  - 3rd Level: Records within each file
- Each node can be locked (shared or exclusive) individually
- When a node is locked, it implicitly locks all the descendants in the same mode

### Intention Locks
- In addition to Shared (S) & Exclusive (X) locks, multiple granularity has 3 additional locks
- This ensures serializability
- Intention-Shared (IS)
- Intention-Exclusive (IX)
- Shared & Intention-Exclusive (SIX)

### Procedure for transaction to acquire lock
- Check the lock compatiblity
- Lock the root of the tree first in any mode
- Follows 2PL, so deadlocks are possible
- Locks are acquired top-down (root to leaf) and released bottom-up (leaf to root)
- Lock can be acquired only
  - If the parent is locked
  - If none of the children is locked
- Node can be locked in
  - S, IS if the parent is in IX, IS
  - X, IX, SIX if the parent is in IX, SIX

## Timestamp Based Protocols
- Each transaction has a timestamp attached to it
- The timestamps are usually assigned in the order of submission
- The conflicting pairs of operations can be resolved by their timestamps
- TS(T) – Timestamp of transaction T when submitted
- TS(W(X)): Latest timestamp when any transaction executed W(X) successfully
- TS(R(X)): Latest timestamp when any transaction executed R(X) successfully

### Deadlock Prevention
- Wait Die
  - An older transaction should wait for a younger transaction
  - If a younger transaction waiting for an older transaction
    - Younger transaction should be aborted and restarted with the same timestamp
  - Non-preemptive technique
- Wound Wait
  - A younger transaction should wait for an older transaction
  - If an older transaction is waiting for a younger transaction
    - Younger transaction should be aborted and restarted with the same timestamp
  - Preemptive technique
- In both cases, younger transaction is aborted
  - Based on the assumption that it will waste less processing effort

## Timstamp Ordering Protocol
- Ensures that the conflicting operations do not violate the ordering
- If R(X) and W(X) are conflicting operations
  - Then R(X) is processed before W(X) if and only if TS(T1) < TS(T2)
  - If a schedule doesn't follow a timestamp serializability, reject and rollback the transaction
- Each transaction is assigned a unique timestamp when it enters the system
  - Ensuring that all operations follow a specific order
  - Making the schedule conflict serializable and deadlock free
- Cascading rollbacks are possible
- If T2 occurs before T1
  - Allowed Operations
    - R1(X), R2(X)
  - Not Allowed Operations
    - R1(X), W2(X)
    - W1(X), R2(X)
    - W1(X), W2(X)
- Strict Timestamp Ordering
  - A variation where the read or write operation is delayed
  - Until the transaction that wrote the value of the data item is committed or aborted

### Working
- If a transaction Ti issues a read(X) operation
  - If TS(T) < TS(W(X)): Abort and rollback
  - If TS(T) >= TS(W(X)): Execute W(X) and set TS(W(X)) to TS(T)
  - All data-item timestamps updated
- If a transaction Ti issues a write(X) operation
  - If TS(Ti) < RTS(X): Operation rejected
  - If TS(Ti) < WTS(X): Operation rejected and Ti rolled back
  - Else: Operation executed

## Thomas Write Rule (Write Ahead Logging Protocol)
- Any modification to a database must be written to disk
  - Before the control is returned to a user
- This ensures that database remains consistent and durable
- Modification of the basic timestamp ordering protocol
- Does not enforce conflict serializability
  - But rejects fewer write operations by modifying the check operations for W(X)
- If T2 occurs before T1
  - Allowed Operations
    - W1(X), W2(X)
    - R1(X), R2(X)
  - Not Allowed Operations
    - R1(X), W2(X)
    - W1(X), R2(X)

### Working
- If TS(R(X)) > TS(T): Abort and rollback T
- If TS(W(X)) > TS(T): Skip the write operation and continue
  - Case of outdated of obsolete writes
  - A transaction has already updated the value of X
  - TO protocol aborts such a transaction
  - Example Schedule: T2(R(X)), T1(W(X)), T2(W(X)) but T1 already wrote X
- Else: Execute W(X) and set TS(W(X)) to TS(T)
