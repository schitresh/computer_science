# Memory Management
- Memory management is the functionality which manages primary memory
  - Moves processes between main memory and disk during execution
  - Keeps track of each memory location whether it's allocated or free
  - Allocates memory dynamically to the programs when requested
    - And de-allocates for reuse when no longer needed
- Memory Management Unit (MMU) handles these tasks
- Requirements
  - Relocation: Relocate the process when swapped back if the previous location is occupied by another process
  - Protection: One process should not write to the address of another process (accidental or incidental)
  - Sharing: Allow controlled access to shared memory, share copy of process where required
  - Organization of logical & physical memory
- Programs always execute in main memory, so larger the main memory, larger the multiprogramming

## Memory Allocation and Partitioning
### Placement Algorithms
- OS decides which free block to allocate when a process is loaded into main memory
- First fit: First available block which is large enough
- Best fit: First smallest sufficient partition
  - Consumes a lot of process time to search
  - May not always be the best algorithm
    - It depends on how the memory can be distributed among all processes
- Worst fit: Largest sufficient partition
- Next fit: Similar to first fit, but will be searched from the last allocation point

### Allocation Methods
- Single Continguous: Except the reserved memory for OS, all memory is available to a process
- Partitioned: Memory is divided into different blocks or partitions and allocated based on requirements
- Paged: Memory is divided into fixed size units called page frames and used as virtual memory
- Segmented: Memory is divided into different segments
  - Segment is a logical grouping of the process data or code
  - Allocated memory doesn’t have to be contiguous
  - Most OS use segmentation with paging
    - A process is divided into segments and each segment has pages

### Fragmentation
- When many of the free blocks are too small to satisfy any request
- External: Memory not contiguous, requires memory shuffling
- Internal: Allocated memory larger than required
- Defragmentation

## Contiguous Partitioning
- Processes can only be allocated contiguous or adjacent blocks of memory

### Fixed or Static Partitioning
- Main memory is divided into fixed number of partitions but the sizes may vary with no overlaps
- Each partition is assigned to a specific process or user, OS occupies the first partition
- Typically allocated at boot time and remains dedicated to a process till it terminates or releases
- Advantages
  - Simple and easy to implement
  - Minimum memory can be ensured for each process
  - Prevents processes from interfering into each other's memory space
- Disadvantages
  - Internal fragmentation (memory in partition remains unused)
  - External fragmentation (since partitions are contiguous, some parts of memory may remain unused)
  - Process size limitation (cannot exceed than the allocated partition)
  - Limits the number of processes running concurrently (each process requires a dedicated partition)
- Used in embedded systems, real-time systems, limited memory systems

### Variable or Dynamic Partitioning
- Partitions are not made before execution but during run-time
- Partition is created depending on the process requirements avoiding internal fragmentation
- Number of partitions is not fixed and depends upon the incoming processes and the main memory size
- First partition is reserved for OS
- Keeping track of partitions: Bitmap, Linked List
- Advantages: No interal fragmentation, no limitation on multiprogramming, no limitation on process size
- Disadvantages: External fragmentation, complex memory allocation

## Non-Contiguous Partitioning
- Processes can be allocated a series of non-contiguous blocks of memory that can be located anywhere
- Pointers are used to link the blocks and track the blocks allocated to a process
- Use of pointers introduces an overhead in allocation & de-allocation
- Need to maintain page table for each process

### Paging
- Logical memory or process address space is divided into blocks of same size called pages
- Main memory is divided into small fixed sized blocks of physical memory called frames
- No external fragmentation since frame size is generally equal to page size
- Retrieving processes from secondary storage into main memory in form of pages is also called paging
- Internal fragmentation can happen in the last page of the process
- Logical address
  - Page number: Bits that represent the page in logical address space
  - Page offset: Bits that represent a particular word in a page
  - p|d (logical) -> f|d (physical)
- Physical address
  - Frame number
  - Frame offset
- Translation Lookaside Buffer (TLB) is special fast lookup hardware cache
  - It is used to track recently used page table entries

### Segmentation
- A process is divided into segments (main program, functions, procedures, variables, etc)
- Segments may not be of same sizes which can lead to external fragmentation
- It gives user's view of process which paging does not
- Segment table maps logical and physical addresses

## Address Spaces
### Logical or Virtual Address
- Virtual address generated by CPU during program execution relative to the program's address space
- Provides a layer of abstraction that allows processes to access memory without knowing physical addresses
- Memory management unit (MMU) translates logical addresses into physical addresses using page table
- Page table maps each logical page number to a physical frame number
- Process/logical address space
  - Set of logical addresses that a process references in its code
  - OS maps logical addresses to physical addresses at the time of memory allocation to the program
- Uses
  - Allows efficient memory management using paging and segmentation
  - Can extend physical memory by disk
  - Memory protection
  - Less I/O needed to load or swap program in memory

### Physical Address
- Actual address in main memory where data is stored
- Physical addresses are not exposed to processes or users
- Physical address space does not change
- Example
  - Physical address = 12 bits, physical address space = 2^12 = 4 * 1024 = 4K words
  - Logical address = 13 bits, physical address space = 2^13 = 8 * 1024 = 8K words

## Address Binding
- Process of mapping one address space to another address space
- Done by Memory management unit (MMU) (address translation unit in particular)

### Contiguous Memory Allocation
- In contiguous memory allocation, it is not a difficult task
- If the base address of the process is known, next addresses can be found out
- MMU is a combination of two registers: Base register & limit register
- Base Register (Relocation Register)
  - Contains starting physical address of the process
- Limit Register
  - Mentions the limit relative to the base address on the region occupied by the process
  - Logical address generated by CPU is first checked by limit register
  - If the value of the logical address is less than the limit register
    - The base address stored in the relocation register is added to the logical address to get the physical address
  - If the value of the logical address is greater than the limit register
    - CPU traps to the OS and OS terminates the program by giving fatal error

### Non-contiguous Memory Allocation
- Processes can be allocated anywhere in the available space
- The address translation is difficult, some techniques are Paging & Segmentation
- Different data structures and hardware support like TLB are required

### Types
- Compile Time
  - If it is known at the compile time where the process will reside in memory
    - Then an absolute address is generated
  - Physical address is embedded to the executable of the program during compilation
  - Loading executable as a process in memory is very fast
  - If the generated address space is preoccupied by other processes, then the program crashes
    - The program needs to be recompiled to change the address space
- Load Time
  - If it is not known at the compile time where the process will reside
    - Then a relocatable address is generated
  - The loader translates the relocatable address to an absolute address
  - To generate an absolute address
    - The base address of the process in main memory is added to all logical addresses by the loader
  - If the base address of the process changes, the process needs to be reloaded
- Execution Time
  - The stage where instructions are in memory and are being processed by CPU
  - Additional memory may be allocated and de-allocated
  - Used if a process can be moved from one memory to another during execution

### Page Table
- Data structure used by OS to keep track of the mapping between logical and physical addresses
- Contents of Page Table Entry (PTE)
  - Frame Number (or Address Translation Bit): Frame number in which the page is present (physical address)
  - Present/Absent Bit (or Valid/Invalid Bit): If the page is not present, it is called Page Fault
  - Protection Bit: Specifies protection like read, write, etc.
  - Reference Bit: Whether the page was referred in the last cycle or not
  - Caching Enabled/Disabled: Caching is disabled when the latest info is required
  - Modified Bit (or Dirty Bit): If a page is modified, it has to be written or saved somewhere on page replacement
- The size and format of PTE can vary depending on the architecture of the system and the OS

## Allocating Kernel Memory
### Buddy System
- Divides memory into blocks of fixed size, each block has size in the power of two
- Follows best fit strategy
- On getting a request, it finds the smallest available block with sufficient size
  - If the block is larger than required, it is split into two smaller blocks of equal size (buddies)
  - This is repeated till the requested size is achieved
- Split strategies: Binary, fibonacci, weighted, tertiary
- Advantages
  - Easy to implement and can handle wide range of memory sizes
  - Coalescing (how quickly adjacent buddies can be combined to form a larger segment)
  - Address calculation is easy
- Disadvantages: Internal fragmentation, can be inefficient in allocating small amounts of memory

### Slab System
- Divides memory into slabs of fixed size consisting of a set of objects of the same type
- Slab
  - Made up of one or more physically contiguous pages
  - Container of data associated with objects of specific kind of the containing cache
  - Possible states depending on the available objects: full, empty, partial
- Cache
  - Small amount of very fast memory, consists of one or more slabs
  - Single cache for each unique kernel data structure (e.g. file objects, semaphores, process descriptors)
- On getting a request, it attempts to assign free object from a partial slab and then from an empty slab
  - If these slabs are not available, a new slab is allocated from contiguous physical pages and assigned to a cache
  - When the object is released and marked free, it returns to its cache
- Advantages:
  - Efficient in allocating small amounts of memory since objects are created in advance
  - Prevents fragmentation
- Disadvantages: Complex to implement, may require more memory overhead

## Garbage Collector
- Prevents memory leaks and fragmentation
- Dynamic approach to automatic memory management and heap allocation
  - That processes and identifies memory no longer referenced
- Dynamic memory management process that finds dead memory blocks and reallocates them
- 3 primary approaches
  - Mark and sweep: Reclaiming available memory
  - Reference counting
    - Allocated object contains reference count of referencing number
    - When memory count is 0, object is garbage and destroyed
    - Freed memory returns to heap memory
  - Copy collection: Two partitions. When one is full, relocate and compact to second
- Buffer Overflow

### Memory Leak
- When memory which is no longer needed is not released
- When an object is stored in memory but cannot be accessed by running code
