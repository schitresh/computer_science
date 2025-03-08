## Process Synchronization
- Communication/Coordination/Concurrency control
- Coordination of execution of multiple processes that use shared resources
- Ensures that shared resources are accessed in a controlled and predictable manner
- Resolves the problem of race condition, inconsistency, deadlocks
- Process types based on synchronization
  - Independent: Execution does not affect other processes
  - Cooperative: Execution affects other processes
- Goals
  - Avoid race conditions
  - Achieve rules for critical section
  - Performance

## IPC (Inter Process Communication)
- Mechanism through which processes can communicate with each other and synchronize their actions
- Communication mediums: Shared memory, Message passing

### Communication Methods
- Pipes
  - Unidirectional (similar to keyboard)
  - Data is usually buffered till it's processed by receiver
- Message Queuing
  - Used to send & receive messages between processes
  - Messages are coordinated via API
- Semaphores
  - Controls access to shared resource and avoids race condition
- Shared memory
  - Interchange of data through a defined area of memory
- Sockets
  - Network communication between processes running on different hosts
  - Allows for system independent connection
  - Each endpoint of a communication is a socket
  - Concatenation of IP address and port
- Remote Procedural Calls (RPC)
  - Used for distributed computing
  - Allows processes on different hosts to call procedures on each other
  - Program allows a procedure to execute on different address space
  - Primary client-server is implied
    - Remote process maintains a server component
    - Client processes send messages and get the output
  - When making a RPC call
    - The calling environment is suspended and procedure parameters are transferred across the network
    - Procedure is executed on the target environment
    - After execution, the results are transferred back to the calling environment
    - Execution resumes in the calling environment as if returning from a regular procedure call

### Shared Memory
- A process generates info and keeps it as a record in shared memory
- Other processes can check this record and use the info
- Example: Producer-Consumer problem where producer puts items in a common buffer and consumer picks them up

### Message Passing
- Establish a communication link and exchange messages using basic primitives
- At least two primitives are required: send & receive
- Message size can be fixed (easy for OS designer) or variable (easy for programmer)
- Message structure
  - Header
    - Message type & length
    - Source & destination
    - Control info: priority, sequence number, instructions if it runs out of buffer space
  - Body
- Example: Producer-Consumer problem where producer sends item as message to consumer

### Communication Link
- Capacity: Maximum number of messages that can reside in the queue
  - Can be zero, bounded, unbounded
- Direct Link
  - A specific process identifier is used for communication
  - It is hard to identify the sender ahead of time
- Indirect Link
  - A shared mailbox/port is used which consists of queue
  - Sender puts the message in the mailbox and reciever picks them up
- Multiple communication links with different types can be established between any two processes

### Communication Types
- Synchronous/Blocking passing where the message is processed right away
- Asynchronous/Non-blocking passing where the message kept in wait & processed when the process becomes free
- For a sender
  - Async passing is preferred so that it doesn't have to wait and can carry out other tasks
  - However, an acknowledgement from receiver is necessary in case it fails
- For a receiver
  - Sync passing is preferred so that it can send the return data or error message right away
  - Messages can keep failing if the error is not communicated to the sender

## Race Condition
- When multiple processes try to access a shared resource (same code, same memory, same variable)
- They are racing each other to access the resource
- The output of the shared resource can be wrong for these processes due to lack of clarity
- The order of these processes may be important to get the final output

## Program sections
- Entry Section: Decides the entry of a particular process
- Critical Section: Only one process is allowed to enter and access or modify shared variable
- Exit Section: Allows other processes waiting in entry section to enter CS
- Remainder Section: Everything else

## Critical Section
- Regions of program that access shared resources and may cause race condition
- It must be executed as an atomic operation

### Rules
- Mutual Exclusion
  - Only one process is allowed to run in CS at a time
- Progress
  - If no process is running in CS
  - Processes not in their remainder section should decide which process will enter its CS next
  - This should happen in a finite time and other processes should not wait indefinitely
- Bounded Waiting
  - After a process has made a request, there must be a limit for other processes to enter CS
  - A process shouldn't wait endlessly for access

### Problems
- Deadlock: When multiple processes wait for each other to release CS
- Starvation: When a process or thread is prevented repeatedly from entering CS
- Overhead: Acquiring & releasing locks or semaphores
- Impacts Scalability: CS becomes a bottleneck for scalability since access to shared resource is restricted

### Solutions
- Three important criterias
  - Correctness
  - Maximum concurrency
  - No busy waits: Prefer blocking over busy waits
- Hardware Approach
- Software Approach

## Hardware Solutions
### Disabling Interrupts
- When interrupts are disabled, no process is allowed to perform context switch
- As a result, it will allow only one process to enter CS
- Nothing can stop the process from doing its work
  - As OS only switches processes when it gets an interrupt from the clock
  - The CS can't be split between time slices
- Problems
  - Catastrophic if a process fails to enable its interrupts again
  - Effectively halting the CPU to let the program do everything
  - Ineffective in a multiprocessor system
    - Where disabling interrupts only seizes the processor that executes the instructions

### Test and Set Lock operation (TSL)
- Boolean value which is atomic in nature, i.e. no other interrupt is allowed to access
- Single instruction to load value of lock in register and set it to 1
- Provides mutual exclusion and progress but not bounded waiting
- Priority inversion
  - If process gets pre-empted from CS and leaves the lock, no other process can enter (spin lock)
- Busy Waiting

### Compare and swap operation
- Similar to test & set, but matches the passed value with the expected value
