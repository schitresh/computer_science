## Kernel Operations
- Kernel mode (mode bit 0)
  - CPU can execute certain instructions only in kernel mode (privilege instructions)
  - Privilege instructions usually peform operations that required direct access to hardware or privileged resources
  - Example: setting up memory mapping, accessing I/O devices, remove a process from memory
- Context Switch
- User mode (mode bit 1)
  - Prevents user program from interfering with OS program
  - Non privileged instructions
    - Performing computations, accessing user-level resources like files & memory, managing process control
- Concept of modes can be extended beyond two
  - Requires more than a single bit mode CPU that support virtualization
  - One of these extra bits is used to indicate when virtual machine manager (VMM) is in control
  - VMM has more privileges than user program but not so many as full kernel

### System call
- Programmatic way for a program to request a service from kernel
- Program is temporarily switched from user mode to kernel mode
- Implemented in the form of software interrupts
  - Which causes hardware's interrupt handler to transfer control to an appropriate interrupt handler (part of OS)
  - And switches the bit mode to kernel mode
- Interrupt handler
  - Checks which interrupt was generated and additional parameters (passed through registers)
  - Then calls appropriate kernel service routine to handle the service requested by service call
  - Illegal instuctions are trapped and control is transferred to OS to issue error message & log

## Monolithic Kernel
- All OS services run in kernel space and share the same memory space
- Faster than micro-kernel due to direct calls & same memory space
- If any service fails, it leads to entire system failure
- Structure
  - Application (Outside Kernel)
  - VFS, System calls
  - IPC, File System
  - Scheduler, Virtual Memory
  - Device driver, Dispatcher
  - Hardware (Outside Kernel)

## Micro-Kernel
- Provides only the most basic services (memory management, process scheduling)
  - Reduces the attack surface making it more secure & stable
- Other services (device drivers, file systems) are implemented as user level processes
  - They communicate with kernel using message passing rather than shared memory
  - Easier to add or remove services making it more modular & flexible but can increase complexity
  - Message passing can be slower than direct system calls in monolithic kernel

## Kernel I/O Subsystem
- Services provided: scheduling, caching, spooling, device reservation, error handling
- I/O Scheduling
  - Each device has a wait queue for requests
  - When an application issues a blocking I/O system call, it's placed in the queue of the device
  - I/O scheduler rearranges the order to improve the efficiency
- Buffering
  - Memory area that stores data being transferred between devices or a device & an application
  - Copes with speed mismatch between producer & consumer
  - Provides adaptation for data with different data-transfer sizes
  - Supports copy semantic for the application I/O
    - Copy semantic
      - If an application wants to write data from buffer to a disc
      - It calls write() system call providing pointer to the buffer
        - And an integer specifying number of bytes to write
- Caching
  - Fast memory that holds a copy of data for faster access
- Spooling
  - A buffer that holds the output of a device that cannot accept interleaved data streams
  - For example, a printer where several applications send output concurrently
    - Without mixing their outputs
