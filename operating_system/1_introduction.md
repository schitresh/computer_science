## Introduction of OS
- Interface between users and hardware
- Provides an environment to execute programs in a convenient and efficient manner
- Prevents interfering with proper operation of a system
- A program running at all times (kernel), with all else being application programs
- Provides convenience, efficiency (of using resource), throughput (tasks per unit time)
- Supports developing new system functions without interfering with the system

## Responsibilities
- Execution of processes (management, scheduling, synchronization)
- Allocation of resources & services (memory, processors, devices, data)
- Management of resources (CPU, memory, files)

## Characteristics
- Device Management: Tracks all devices, and decide which process gets access, when & for how much time
- Processor Management: Allocates processor to process and de-allocates when no longer required or job is done
- Memory Management: Tracks & allocates primary memory
- Storage Management: Stores data in various tracks of hard drive
- File Management: Allocates & de-allocates resources
- System Performance: Records delays between requests of a service and the system
- Job Accounting: Tracks time & resources used by various jobs
- Error Detection & Debugging: Dumps, traces, error messages, etc.
- Security management: Prevents unauthorized access by applications & users
- Compiles & translates high level language to machine language
- Provides loader to move compiled code to memory for execution
- Provide routines that handles details of I/O programming

## Computer system
- User Interface: Users, application programs
- System: Utilities, system programs (compilers, loaders, editors), OS
- Extended Machine: Context save, dispatching, swapping, I/O initiation
- Hardware: Machine language, micro-programming, CPU, memory, devices

## Drivers for Hardware
- I/O
  - I/O traffic controller keeps track of status of devices
  - Each device has a handler that resides in a separate process associated with that device
  - It has memory management that includes buffering, caching, spooling and a device driver interface
- Assemblers
  - Converts an assembly code to object/machine code & instructions required by loader
- Compiler &
  - Converts all the given high level code to machine code and then executes. Ex: C, C++, Rust, Go
- Interpreter
  - Converts high level code to machine code line by line and simultaneously executes it. Ex: Python, Ruby
- Loader
  - A routine that loads an object/machine program in memory and prepares for execution

## Components of OS
- Shell
  - Outermost layer that handles user interaction
- Kernel
  - Core component that provides services to other components
  - Primary interface between OS & hardware that manages system resources
  - Addresses low level functions:
    - I/O management, device drivers, memory management, application management
    - System calls, process & cpu scheduling

## Types of OS
- Batch
  - Groups jobs into batches based on similar requirements. Ex: Payroll & bank systems
- Single Tasking
- Multi Programming
  - Can execute multiple programs in main memory
- Multi Tasking
  - Mult-programming OS having round robin scheduling
  - Preemptive: OS can interrupt and switch to another process
  - Cooperative: OS never interrupts to switch to another process
- Multi Processing
  - Multiple CPUs are used execution
- Time Sharing
  - Each task is given some time to execute
  - Processor's time is shared among multiple users
  - Switching jobs is very fast
- Distributed
  - Multiple computers connected via high-speed buses and share resources
  - Centralized OS over multiple networks that uses single communication channel
- Network
  - Independent systems connected over a single network and share resources
- Real Time
  - Processes data and events that have critically defined time contraints
  - Provides ultra-fast performance

## Memory
### Primary Memory: RAM & ROM
- RAM (Random Access Memory)
  - Main memory or read-write memory
  - Temporarily stores the data that's currently being used or processed
  - Volatile Memory: Data is lost when power is turned off
  - Faster than ROM & Consumes less power than secondary memory
  - Data can be accessed and edited quickly
- ROM (Read Only Memory)
  - Permanently stored memory
  - Non-Volatile Memory
  - Data cannot be modified easily
  - Used to stored: BIOS (Basic Input/Output System), firmwares for hardware devices
  - Used in embedded systems, calculators, peripheral devices
  - Consumes less power than secondary memory

### Secondary Memory: Hard-drive, SSD, USB

## CPU Registers
- A CPU register stores memory addresses, which is how a processor accesses data from RAM
- One bit in a register can reference an individual byte in memory
- Based on how much memory can be accessed by a CPU register, there are 32-bit & 64-bit processors

- 32-bit
  - Can access 2^32 memory addresses (4 GB of RAM or physical memory)
  - For more than 4 GB of RAM, the system should be 64-bit
- 64-bit
  - Can access 2^64 memory addresses (17 * 10^9 GB of RAM or physical memory)


## System Startup
### BIOS (Basic Input Output System)
- Initialization
  - BIOS is loaded from ROM and initialises POST
- POST (Power On Self Test)
  - Initializes hardware devices, runs checks and handles bootable device
- Bootloader
  - BIOS searches for Master Boot Record (MBR) in 1st sector.
  - MBR contains the code that loads OS called bootloader (LILO, GRUB in Linux)
  - Bootloader is pulled into memory and started
  - Bootloader loads OS in memory
- Kernel
  - OS starts running and initialises hardware drivers, and then launches kernel
  - Kernel starts the init system
- Init
  - Determines the run-level of the system (single user, multi user with network, without network, etc)
  - Starts services daemons that support networking, display, devices (keyboard, mouse)

### UEFI (Unified Extensible Firmware Interface)
- Initialization
  - Doesn't look for MBR
  - Maintains a list of valid boot volumes called EFI service partitions
- POST
  - UEFI scans all of the bootable storage devices for GUID Partition Table (GPT)
  - GPT is an improvement over MBR
- GPT
  - Doesn't contain boot loader
  - UEFI scans GPT for EFI service partition to boot from
  - Directly loads OS from the right partition
  - If it fails, goes to BIOS type booting called legacy boot (backward compatible)

### BIOS vs UEFI
- BIOS runs in 16-bit mode, UEFI runs in 32-bit & 64-bit mode
- BIOS only supports drives less than 2TB, UEFI has much higher limit
- UEFI comes with improved boot times, efficient power management, and support for larger hard drives & partitions
- BIOS is stored in ROM, UEFI is stored in non-volatile memory on motherboard
- BIOS loads OS from bootloader, UEFI directly loads OS from hard drive
