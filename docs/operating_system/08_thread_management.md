## Thread
- Basic unit of CPU utilization
  - Flow of execution through the process code
  - Execution unit in a process
- Process has its own memory space and resources
- Threads operate within the same process with shared memory space and resources
  - Separate flow of control with parallelism/concurrency
  - Enables multiple threads to collaborate and work efficiently within a single program
  - Fast communication due to shared memory
- Threads are most effective in multi-processors, otherwise context switch can be an overhead
- Each thread has Thread Control Block (TCB) and can be assigned priority
- Shares with peer threads: Code segment, Data segment, Open files
- Have its own: Program Counter (PC), System Registers, Stack
- Advantages
  - Communication and Response
  - Fast Context Switch
  - Resource Sharing
  - Enhanced Throughput
- Daemon
  - Disk and Execution Monitor
  - It is a long running background process that acts on request

## Types
- User level
  - Not created using system calls and kernel does not manage them
  - More efficient than kernel-level, context switch time is less, easier implementation
  - If one thread causes a page fault, the entire process blocks
  - Cannot benefit from multiprocessing
  - Application dependent and OS independent
- Kernel level
  - Have their own thread table to keep track and kernel helps in their management
  - Slower than user-level, context switch time is more, complex implementation
  - Can schedule multiple threads of the same process on different processors
  - OS dependent

## Threading Issues
- Fork and Exec calls
  - fork(): Does the new process duplicate all the threads or keep it single threaded
  - exec(): The program specified as parameter will replace the entire process including all the threads
- Signal Handling
  - Signal is used to notify a process that a particular event has happened
  - Every signal has a default signal handler that the kernel runs when handling the signal
  - This default action can be overriden by a user defined signal handler
- Thread Cancellation
  - A browser often loads a web page using several threads (each image is loaded in a separate thread)
  - When stop button is pressed, all threads loading the page are cancelled
  - Cancellation may occur in 2 different scenarios
    - Async: One thread immediately terminates the target thread
    - Deferred: Target thread continuously checks whether it should terminate
- Thread Local Storage
  - In some circumstances, a thread might need its own copy of data (e.g. in transaction processing)
- Scheduler Activations
  - One scheme of communication between user level thread and kernel
  - Kernel provides an application with a set of virtual processors
    - The application can schedule user threads onto an available virtual processor

## Multi-tasking
- Multi-tasking OS gives the perception of running multiple processes simultaneously
  - By dividing system resources and switching very fast between them
- Process based multi-tasking
  - Process is the smallest unit
  - Example: listening music and browsing internet at the same time
- Thread based multi-tasking
  - Thread is the smallest unit
  - Example: In a browser, navigating through a webpage and downloading a file at the same time

## Zombie Process
- Once a process is executed or terminated, its process descriptor stays in memory
- It sends a signal (SIGCHILD in linux) to its parent and enters into zombie state (EXIT_ZOMBIE in linux)
- The parent process then executes wait() system call to read the dead process's information
- After wait() is called, the zombie process is completely removed from memory
- This normally happens very quickly, so zombie processes are not accumulated in the system
- If zombie processes accumulate, they will take space in process table
  - The process table has finite size and the system won't be able to generate new processes
