# IP (Internet Protocol)
- Responsible for delivering packets from the source host to the destination host
  - IP addresses are included in the packet headers
  - Connection-less protocol used for packet switched networks
  - Operates on a best effort delivery model
    - Neither delivery is guaranteed
    - Nor proper sequencing nor avoidance of duplicate delivery
  - Host-to-host communication: Determines the path of transmission
- Data Encapsulation and Formatting
  - Accepts data from transport layer protocol
  - Ensures that data is sent and received securely
  - Encapsulates data into message known as IP datagram
- Routing
  - When IP datagram is sent over the same local network (LAN, MAN, WAN)
    - It is known as direct delivery
  - When source and destination are on distant network
    - Then the IP datagram is sent indirectly using routers

## Fragmentation
- Maximum Transmission Unit (MTU)
  - Limit imposed on the size of IP datagram by data link layer protocol
- If datagram > MTU, datagram is split into smaller units
  - So that they can travel over the local network
- Fragmentation can be done by the sender or intermediate router
- At the receiver side
  - All the fragments are reassembled to form an original message

## IP Addressing
- Logical or software based address to reach a specific host
- IP addresses are used by internet & higher layers
  - To identify devices and provide internetwork routing
- 32 bits (4 bytes) unique address having address space of 2^32
- Can be written in two notations: dotted decimal & hexadecimal
- Dotted decimal notation
  - Each segment (byte) can have any value from 0 to 255 (2^8 - 1)
  - No zeroes precede the value in any segment (054 is wrong, 54 is correct)

## Classful Addressing
- The 4 bytes of the address are divided into two parts
  - Network ID (Identify the network)
  - Host ID (Identify the host within a network)
- The class of IP address determines the bytes used for network ID & host ID
  - And the number of total networks and hosts possible
  - More number of bytes assigned for host ID means that more number of hosts are possible
- Each ISP or network administrator assigns an IP address to each connected device
  - The first address of any network is the network number
    - So in host ID, all bits cannot be set 0
  - The last address is reserved for broadcast IP
    - So in host ID, all bits cannot be set 1
- Problems
  - Millions of class A and many of class B addresses are wasted
  - Number of addresses available in class C is small (254 hosts)
    - And cannot cater to the needs of an organisation
  - Class D & E are reserved and cannot be used
- Due to these problems
  - Classful addressing was replaced by classless inter-domain routing (CIDR) in 1993

### Classes
- Class A
  - Network ID: 1 byte, Host ID: 3 bytes
  - Starting bits: 0
  - Format: 0, Network ID (7 bits), Host ID (24 bits)
  - Range: 0.0.0.0 - 127.255.255.255
- Class B
  - Network ID: 2 bytes, Host ID: 2 bytes
  - Starting bits: 01
  - Format: 01, Network ID (14 bits), Host ID (16 bits)
  - Range: 128.0.0.0 - 191.255.255.255
- Class C
  - Network ID: 3 bytes, Host ID: 1 byte
  - Starting bits: 110
  - Format: 110, Network ID (21 bits), Host ID (8 bits)
  - Range: 192.0.0.0 - 223.255.255.255
- Class D
  - Multicast addresses
  - Starting bits: 1110
  - Range: 224.0.0.0 - 239.255.255.255
- Class E
  - Reserved for military & experimental purposes
  - Starting bits: 1111
  - Range: 240.0.0.0 - 255.255.255.255

## Classless Addressing
- Invented to keep internet running out of IP addresses and reduce its wastage
- Also known as Classless Inter-Domain Routing (CIDR)

### Subnetting
- Partitioning a single physical network into smaller logical sub-networks
- Divides a large block of addresses into several contiguous sub-blocks
  - And assigns them to smaller networks
  - A subnet or subnetwork is a network inside a network
- Reduces network traffic & complexity
  - Traffic can travel shorter distance without passing through unnecessary routers

### Subnet Mask
- 32-bit number that masks an IP address by dividing it into network and host address
  - Used to identify the subnet to which an IP address belongs
  - Subnet mask: Network bits are set to 1 and host bits are set to 0
  - Network address: Bitwise AND is performed on the IP address and the mask
  - Broadcast address: Bitwise OR is performed on the network address and the inverted mask
  - Number of hosts per subnet: 2 ^ (32 - given bits for mask) - 2
- The address includes the number of bits for mask (assigned to the network address)
  - Usually represented by /n
- Classes
  - Class A: /8, 255.0.0.0
  - Class B: /16, 255.255.0.0
  - Class C: /24, 255.255.255.0
- Two addresses are reserved
  - First address is the network address
  - Last address is the broadcast address

### Example
- 216.3.128.12/25
  - 32 bits = 25 bits (network) + 7 bits (host)
  - Put 25 bits as 1 and 7 bits as 0 to get the subnet mask
- 216.3.128.12 with subnet mask of 255.255.255.128
  - Network address: 216.3.128.0
  - Broadcast address: 216.3.128.127
  - Host IP range: 216.3.128.0 to 216.3.128.126
  - IP class: C

## Supernetting
- Combining multiple networks to form a bigger network
- Process of aggregating routes for multiple smaller networks
- Saves storage space in routing table
  - Simplifies routing decisions
  - Reduces route advertisements to neighboring gateways
- Conditions
  - All the networks should be contiguous
  - The block size of every network should be equal and must be in form of 2^n
  - First network ID should be exactly divisible by whole size of supernet
