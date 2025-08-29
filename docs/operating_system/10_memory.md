# Memory
- Required to save data and instructions either temporarily or permanently
- Divided into cells or registers having an unique location or address
- Each register stores one bit of data
- Every data is converted to binary before storing
- Word
  - Group of bits where a memory unit stores binary information
  - Group of 8 bits is called a byte
- Memory Unit
  - Data lines: Provide the info to be stored
  - Control inputs: Specify the direction of transfer
  - Address selection lines: Specify the word chosen, 2^k words can be accessed using k address lines
- Units of Memory
  - Bit: Smallest unit that stores binary value (0 or 1)
  - Byte: 8 bits, can represent 2^8 = 256 values
  - KiloByte: 1024 Bytes
  - MegaByte: 1024 KB
  - GigaByte, TeraByte, PetaByte

## Memory Heirarchy
- Enhancement to organize the memory such that access time is minimized
- Based on program behavior known as locality of references
- Locality of references: Tendency of a processor to access the same set of memory locations
  - Repetitively over a short period of time
- Some types of memory like cache and main memory are faster than others
  - But have less size and are more expensive
- Types
  - Internal or Primary Memory
    - Directly accessible by the processor
    - Main memory, cache, CPU registers
  - External or Secondary
    - Peripheral storage devices accessible by the processor via an I/O module
    - Magnetic disk, optical disk, magnetic tape

## Hierarchy Design
### Registers
- Small high-speed memory units located in CPU that stores most frequently used data and instructions
- Have fastest access time and smallest storage capacity (16 to 64 bits)

### Cache
- Small fast memory unit located close to CPU
  - That stores recently accessed data from the main memory
- Minimizes access time for CPU by storing temporary data
  - Or acting as a middleware between CPU & original location
- Typically integrated directly into CPU chip
  - Or placed on a separate chip with a bus interconnect with CPU

### Main Memory
- Primary memory of a computer system, has larger capacity than cache memory but is slower
- RAM
  - Read write memory that is volatile and stores data & instructions currently in use by CPU
  - Writing data is faster
  - Static RAM
    - Stores binary info in flip flops and requires constant power supply
    - Faster access time and used to implememt cache memory but expensive than DRAM
    - Complex internal circuitry and less capacity than DRAM
  - Dynamic RAM
    - Stores binary info as a charge in capacitor
    - Requires refreshing circuitry to maintain the charge after a few milliseconds
    - Contains more memory cells per unit area compared to SRAM
- ROM
  - Read only memory that is non-volatile and stores important info used to operate the system
  - Writing data is slower
  - Masked ROM: Hard wired devices with a pre-programmed collection of data, were the first ROMs
  - Programmable ROM: Modifiable once by the user, initially blank and can't be erased once written
  - Erasable PROM: Extension of PROM that can be erased using UV rays
  - Electrically Erasable PROM: Can erase (using electric field) and reprogramme upto 10,000 times

### Secondary Storage
- Non volatile memory that has a large storage capacity and stores data not currently in use by CPU
- Has the slowest access time and typically least expensive type of memory
- Example: Hard disk drive (HDD), Solid state drive (SSD)
- Virtual Memory: Using secondary memory as if it was a part of the main memory if there's a shortage
- Magnetic storage devices use magnetic fields to store and retrieve data
- Solid state storage devices use semiconductor based memory chips to store data

### Magnetic Disk
- Circular plates fabricated with metal or plastic or magnetized material
- Works at high speed inside computer and frequently used

### Magnetic Tape
- Magnetic recording device covered with plastic film, generally used for backup of data
- Access time is slower and requires some time for accessing the strip
