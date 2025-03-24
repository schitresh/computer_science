## Process Management
- Program: Collection of instructions that performs a specific task when executed by a computer
- Process
  - Program in execution with allocated time and resources
  - Can have multiple dynamic instances of the program in execution
- Process sections
  - Stack: Temporary data like function parameters, return addresses, local variables
  - Heap: Dynamically alloted memory to process during its run time, stores functions
  - Text: Current activity represented by program counter, contents of processor registers
  - Data: Global and static variables
- Process groups: parent, children, fork, exec, merge

## Process States
- OS maintains separate queue of PCB for each state
- New: Process being created in secondary memory
- Ready: After creation, process is loaded in main memory and marked ready for execution
- Run: Currently running in CPU
- Wait (or Block): Requesting access for I/O or critical region
- Complete (or Terminated): Execution completed and PCB deleted, allocated resources will be released
- Suspended Ready: Ready process swapped out of main memory, usually when ready queue is full
- Suspended Wait: Wait process swapped out of main memory, usually when wait queue is full

## States for Systems
- Single Tasking Systems: not running, running
- Multi-programming Systems: ready, running, wait
- 5-States Model (general): new, ready, running, wait, terminated
- 7-States Model: new, ready, running, wait, terminated, suspend ready, suspend wait

## Context Switching
- Saving context of one process into PCB and loading context of another process
- Unloaded process is marked from running to ready
- It happens when
  - High priority task comes to ready state
  - Interrupt occurs
  - Sometimes when user & kernel mode switch
    - If another process carries out privileged instructions
  - Preemptive CPU scheduling

## CPU vs I/O Bound
- CPU bound process: Requires more CPU time (spends more time in running state)
- I/O bound process: Requires more I/O time (spends more time in waiting state)

## Process Control Block (PCB)
- Pointer: Retains current position when switched from one state to another
- Process state
- PID
- PC (Program counter): Pointer to next instruction
- CPU registers: Current working variables
- CPU scheduling info: Privileges, priority
- Memory management info: Page table, memory limits, segment table
- Accounting info: CPU usage, time limits, execution ID
- IO status
