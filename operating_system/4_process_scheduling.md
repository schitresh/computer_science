## Timings
- Arrival Time: At which arrives in ready queue
- Completion Time: At which execution is completed
- Burst Time: Required for CPU execution
- Turnaround time: Arrival to Completion
- Waiting time: Time spent in ready queue waiting (Turnaround - Burst)
- Response time: Submission to first response
- Throughput: Number of processes that complete execution per unit time

## Objectives
- Maximum utilization of CPU (percentage in use)
- Fair allocation of CPU
- Maximum throughput
- Minimum turnaround time
- Minimum waiting time and avoid starvation
- Minimum response time

## Categories
- Non-preemptive
  - Process is removed from CPU only when it has finished execution or switches to wait state
  - High throughput rate
  - Bugs can freeze up the system
  - Wastes CPU time while the process is interacting with I/O
- Preemptive
  - Process runs for a limited amount of time in CPU and then switched
  - Better average response time
  - Avoids starvation
  - Overhead of more context switching

## Schedulers
- Long Term (Job Scheduler)
  - Which process should be brought in ready queue
  - How many process should be kept in ready state (decides degree of multi-programming)
  - Maintains balance between CPU bound & I/O bound processes
  - Once a decision is taken, it lasts for a long time
- Short Term (CPU Scheduler)
  - Which process should be executed next (scheduling algorithms are used)
  - Calls dispatcher
  - Runs frequently
- Medium Term (Swapping Scheduler)
  - Used for swapping (moving process from main to secondary memory & vice versa)
  - Reduces degree of multiprogramming

## Dispatcher
- Module that gives control of CPU to the process selected by scheduler
- Responsible for moving process from ready to run state & vice versa
- Takes care of switching context, switching to user mode, jumping to proper location in user pogram

## Convoy Effect
- Few slow processes slow down the entire system
- Solution: preeemptive algorithms
- Example
  - I/O bound process runs in CPU and moves to I/O
  - CPU bound process runs in CPU
  - I/O bound process moves to CPU & waits for CPU bound process
  - CPU bound process runs to I/O
  - I/O bound process moves to I/O & waits for CPU bound process

## Priority Inversion
- Happens when a high priority task ends up waiting for a low priority task
- Example
  - We have 3 tasks defined by priority: L (Low), M (Medium), H (High)
  - H is waiting on L for I/O
  - So M will run first, then L, and then finally H
- Priority Inheritance
  - Process holding the shared resource inherits the priority of highest priority process waiting for it
  - This is done only till the lock is released
  - So L will run first, then H, and then finally M

## Algorithms
### First Come First Serve (FCFS)
- Also known as First In First out (FIFO)
- Waiting time is high
- Convoy effect can happen (Few slow processes slow down the entire system)
- Used by other algorithms in case of conflict

### Shortest Job First (SJF)
- Burst time can't be known in advance but can be approximated
  - Process size
  - Process type
    - OS process: compiler, program manager
    - User process: editors, utility software
    - Interactive process: which have high I/O frequency
  - Can approximate by averaging last run-times
- Minimum waiting time among all algorithms
- Starvation can happen if short jobs keep coming
- Starvation can be solved using ageing, but defining ageing rate can be challenging
- Preemptive version: Shortest Remaining Time First (SRTF)

### Longest Job First (LJF)
- May lead to convoy effect due to high average waiting time & average turnaround time
- Preemptive version: Longest Remaining Job First (LRJF)

### Priority Scheduling
- If a higher priority process comes, current process is suspended
- May lead to starvation (Can be solved using ageing or dynamic priority)
- Priority inversion can happen (Low priority process holds a resource required by high priority process)
- Inversion avoidance techniques (priority inheritance, priority ceiling protocals) can make it more complicated

### Round Robin (RR)
- Preemptive version of FCFS
- Fixed time slots/quantum/slice over all the processes in a circular fashion
- High response time for high time quantum
- High context switch overhead for low time quantum
- High wait time and reduced throughput depending on time quantum
- Deciding perfect time quantum is a task

### Selfish Round Robin (SRR)
- Round robin that give better service to existing processes than the new ones
- Processes in ready list are partitioned into: New and Accepted
- Priority of new processes increases at rate 'a' and that of accepted processes increases at rate 'b'
- When priority of a new process reaches that of an accepted process, it becomes an accepted process
- Poor response time and priority handling

### High Response Ratio Next (HRRN)
- Modification of SJF to reduce starvation
- Response Ratio = (Waiting Time + Burst Time) / Burst Time

### Multilevel Queue
- Divides the ready queue into several separate queues (having their own priority)
- Different types of processes are queued based on their priority
- Each queue uses its own scheduling algorithm
- Starvation may happen
- Example:
  - System Processes: CPU itself has its processes
  - Interactive Processes: Processes with the same type of interaction
  - Batch Processes: Collecting similar programs in a batch before executing

### Multilevel Queue Scheduling with Feedback
- Allows processes to move between queues
- More CPU overhead and complexity
- Useful because burst time approximation may become more accurate later
