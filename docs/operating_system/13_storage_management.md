## File System
- Method used by OS to store, organize and manage data on a storage device using files and directories
- Types
  - FAT (File Allocation Table): Older file system
  - NTFS (New Technology File System): Modern file system that supports permissions, compression, encryption
  - Ext (Extended File System): Commonly used in linux and unix
  - HFS (Hierarchical File System): Used by mac OS
  - APFS (Apple File System): New file system for mac OS
- File: Collection of related information used to store and manage data in the computer system
- Directory: Collection of files
  - Contains information about files: attributes, location, ownership
  - Directory is itself a file accessible by file management routines
  - Helps in grouping files and locating files quickly

## File Allocation Methods
- Continuous Allocation
  - A single continuous set of block is allocated at the time of file creation
  - Pre-allocation strategy using variable size portions
  - File allocation table needs a single entry for each file, with starting block and length
- Linked or Non-contiguous Allocation
  - Individual blocks contain pointer to the next block, any free block can be added to the chain
  - Although pre-allocation is possible, it is more common to allocate as needed
  - If the pointer of any block is lost, the file will be truncated
  - Supports only sequential access of files
  - File allocation table needs a single entry for each file, with starting block and length
- Indexed Allocation
  - File allocation table contains a separate one-level index for each file
  - The index has one entry for each block allocated to the file
  - The allocation can be on basis of fixed-size or variable-size blocks
  - Supports both sequential and direct access to the file

## Disk Free Space Management
- Space not allocated to any file also needs to be managed
- To know what blocks are available on a disk, a disk allocation table is required
- Bit Tables
  - A vector containing one bit is used for each block on the disk: 0 for free blocks, 1 for occupied blocks
  - Works well with any file allocation method, and easy to find contiguous free blocks
- Free Block List
  - Each block is assigned a number sequentially
  - List of the numbers of all free blocks is maintained in a reserved block of the disk

## Unix File System
- Files are organized in multi-level hierarchy structure called directory tree
- At the top of the file system is the root directory (represented by '/')
  - All other files are descendants of root
- Each file and directory has an owner, a group, and permissions
- Supports symbolic links: pointers to other files or directories
  - Without the need of physically moving them around

### Structure
- /: root
- /bin (binaries): fundamental utilities like ls, cp
- /boot: files required for successful booting
- /dev (devices): contains file representations of peripheral & pseudo devices
- /etc: system wide configuration files & system databases
- /home: home directories for users
- /lib: system libraries, critical files like kernel modules or device drivers
- /media: default mount point for removable devices like USB drives
- /mnt (mount): file system mount points, used if the system uses multiple hard disks or disk partitions
  - Also used for file remote/network file systems, CD/DVD drives
- /proc: procfs virtual file system showing info about processes as files
- /root: home directory for the super user 'root'
  - Not kept in /home in case specific maintenance needs to be performed
  - During which other file systems are not available
- /tmp: temporary files, many systems clear it upon startup
- /usr: originally held user home directories which is now done by /home
  - Now holds executables, libraries, shared resources that are not system critical
  - /usr/bin: stores binary programs distributed with OS not residing in /bin & /sbin
  - /usr/include: stores development headers used throughout the system, mostly used by #include in C/C++
  - /usr/lib: required libraries and data files for programs stored in /usr
- /var (variable): files that may change often especially in size
  - /var/log: system log files
  - /var/mail: stores incoming mails
  - /var/spool: contains print jobs, mail spools and other queued tasks
  - /var/tmp: temporary files which should be preserved between system reboots

### Types of Unix Files
- Ordinary files: Files containing data, text, program instructions
- Special files: Represents a physical device used for I/O like printer, tape drive
  - Character special file: Data is transferred one character at a time (raw device access)
  - Block special file: Data is transferred in large fixed-size blocks (block device access)
- Directories: Store both special & ordinary files
- Pipes: UNIX allows linking commands using a pipe
  - The pipe acts as a temporary file which holds data from one command until read by another
- Sockets: Special file that allows for advanced inter-process communication
  - It is a stream of data, similar to network stream & network sockets
  - But all transactions are local to the file system
- Symbolic link: Used to reference some other file in the file system

## File Access Methods
- Sequential Access
  - Information in the file is processed in order, one record after the other
  - Most common and simplest access method
  - Read: It moves the pointer ahead by one
  - Write: It allocates memory and moves the pointer to the end of the file
  - Advantages
    - Less prone to data corruption as the data is written sequentially and not randomly
    - More efficient method for reading large files, as it only reads the required data
    - Reliable method for backup and restore operations
  - Disadvantages
    - Does not allow quick access to a specific record in the file
    - Not suitable for applications that require frequent updates or modifications to the file
    - Space between records cannot be used by other records
- Index Sequential Access
  - Constructs an index for the file, which contains the pointers to various blocks
- Direct Access (or Relative Access)
  - A fixed length logical record that allows to read and write record rapidly in no particular order
  - The file is viewed as a numbered sequence of block or record
- Relative Record Access
  - Records are accessed relative to the current position of the file pointer
  - Requires fixed length records and may not be flexible enough for some applications
  - Difficult to insert or delete records in the middle of a file
    - Without disrupting the relative positions of other records
- Content Addressable Access
  - Hash function is used to calculate a unique key for each record or block based on its content
  - Any record or block can be accessed by specifying its key
  - Ideal for searching large databases or file systems
  - Allows easy insertion and deletion of records or blocks
  - There is an overhead of calculating hashes and possibility of collision

## Disk or I/O Scheduling
- Only one I/O request can be served at a time by the disk controller
- Two or more requests may be far from each other which can result in greater disk arm movement
- Hard drives are one of the slowest parts of the system and needs to be accessed in an efficient manner
- Key Terms
  - Seek time: Time take to locate the disk arm to a specified track where the data is to be read or written
  - Rotational Latency: Time taken by the desired sector to rotate into a position
    - So that read/write heads can be accessed
  - Transfer time: Time taken to transfer data, depends on rotating speed and size of data
  - Disk access time = Seek time + Rotational latency + Transfer time
  - Disk Response time: Average time spent by a request to wait for I/O

## Spooling
- SPOOL: Simultaneous Peripheral Operations On-Line
- Similar to a buffering mechanism in which data is temporarily held
  - To be used and executed by a device, program or system
- Data is sent to and stored in memory or other volatile storage until the program requests for execution
- Devices like printers, keyboard, mouse are slow relative to the rest of the system creating a bottleneck
  - Spooling resolves this by accumulating data, instructions & processes from multiple sources in a request queue
  - Which is then processed in a FIFO manner
- Batch processing systems also use spooling to maintain a queue of ready-to-run jobs
  - Which can be started as soon as the system has resources
- Allows multiple processes to write documents to a print queue without waiting and resume their work

### Difference from Buffering
- Main memory has an area called buffer to store or hold data temporarily
  - That is being transmitted between two devices or between a device & an application
- Helps in matching the speed of data stream between the sender and the receiver

## RAID:
- 0
- 1 – Clone
- 2 – Error correcting code and bits
- 3 – Byte level stripking with parity disk
- 4 – Block level striping with parity disk
- 5 – Block level striping with distributed parity
- 6 – extends 5 with one more parity block
- 10 – combine raids 1 and 0
