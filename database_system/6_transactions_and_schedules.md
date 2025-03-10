## Transaction
- Transaction
  - Collection of operations that performs a single logical function in database
- Operations: Read, Write, Commit, Rollback, Abort

## Transaction properties
- Atomicity
  - Either all operations should execute or none
  - No partial transactions
- Consistency
  - Data should be consistent everywhere
    - Debit, credit, sender, receiver, total, remaining, before, after
  - Any transaction should take the database from one consistent state to another
    - Maintaining the rules and constraints defined for the data
- Isolation
  - Operation permission should be granted to one transaction only
  - No two writes or one read & write should happen simultaneously
  - Ensures that multiple transactions can occur concurrently and independently
    - Without interference and without leading to inconsistency of database state
- Durable
  - Once committed, changes should be permanent even if a system failure occurs
  - Account updates shouldn't be lost
  - Multiple copies of the database should be stored at different locations

## Schedule
- Series of operations from one or more transactions
- Types
  - Serial
  - Concurrent
    - Serializable
      - Conflict Serializable
      - View Serializable
    - Non-Serializable
      - Recoverable
        - Cascading
        - Cascadeless
        - Strict
      - Non-Recoverable

### Serial Schedule
- When one transaction executes completely before starting another transaction
- It is always consistent
- Has low throughput and less resource utilization

### Concurrent Schedule
- When operations of a transaction are interleaved
  - With operations of other transactions of a schedule
- Can lead to inconsistency
- Serializable Schedules
  - Used to verify whether the scheduling will lead to any inconsistency
  - These are non-serial transactions that produce an equal outcome when executed serially

## Conflict Serializable
- If the schedule can be transformed into serial schedule
  - By swapping non-conflicting operations

### Conflicting Operations
- They belong to separate transactions
- Both operate on the same data item
- At least one of them is write operation

### Examples
- Example 1:
  - S: R1(A), W1(A), R2(A), W2(A), R1(B), W1(B), R2(B), W2(B)
  - Swapping non-conflicting operations
    - S1: R1(A), W1(A), R1(B), W1(B), R2(A), W2(A), R2(B), W2(B)
  - This can be represented as T1 -> T2
  - It can also be rearranged as T2 -> T1
- Example 2:
  - S: R2(A), W2(A), R1(A), W1(A), R1(B), W1(B), R2(B), W2(B)
  - A needs to be written by T2 first & then needs to be read by T1
  - B needs to be written by T1 first & then needs to be read by T2
  - Hence, it cannot be rearranged as T1 -> T2 or T2 -> T1
  - So it is not conflict serializable

### Conflict Equivalent
- Two schedules are conflict equivalent
  - If one can be transformed to another by swapping non-conflicting operations
- In example 1, S & S1 are conflict equivalent

## View Serializable
- A schedule is view serializable if it is view equivalent to a serial schedule
  - Serial Schedule
    - Transactions are executed one after another without interleaving
  - View Equivalent
    - If two schedules produce the same final state of the database
    - And ensure the same read/write behavior for all transactions
- There are no overlapping transactions
- Schedules that are conflict serializable are always view serializale
- Conditions in both the schedules
  - Read of initial value and write of final value must be same for a data item
  - W -> R conflict must be the same

### View Equivalence
- Two schedules are view equivalent
  - If they produce the same set of results when executed against the same state
- Order of any two conflicting operations in S1 should be same in S2
- Conditions
  - Initial Read
    - If T1 reads the data item A in S1
    - Then T1 should also read A in S2
  - Updated Read
    - If T1 reads A written by T2 in S1
    - Then T1 should also read A written by T2 in S2
  - Final Write
    - If T1 performs the final write on A in S1
    - Then T1 should also perform the final write on A in S2

## Recoverable Schedules
- Transactions commit only after all the transactions whose changes were read are committed
- It allows the system to return the database to a consistent state
- Example:
  - T1 reads A, modifies and writes A
  - T2 reads A, modifies and writes A
  - T1 is committed
  - T2 is committed (Committed after T1, A read by T2 was modified by T1)
- Cascading Schedule
  - If a transaction fails, all other dependent transactions rolled back or aborted
- Cascadeless Schedule
  - Transactions read values only after
    - All the transactions whose changes are to be read are committed
  - Avoids a series of transaction rollbacks due to abort of a single transaction
- Strict Schedule
  - A transaction can read or write updated value of another transaction
    - Only after it is commited or aborted

## Non Recoverable Schedules
- If a transaction T2 reads and commits changes made by another transaction T1
- But later if that transaction T1 is aborted, the value read by T2 will be wrong
- Since T2 already committed, the schedule is non-recoverable
