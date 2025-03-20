## Switching
- Technique by which nodes control or switch data
  - To transmit it between specific points on a network
- There are three common switching techniques
  - Circuit switching
  - Packet switching
  - Message switching

## Circuit Switching
- Network resources (bandwidth) are divided into pieces
- Before the data transmission begins
  - A dedicated path (circuit) is established between sender & receiver
  - The circuit remains dedicated for the session and provides a guaranteed data rate
- The bandwidth is reserved even when no data is being transmitted
  - Which might be inefficient
- The connection is not required to be established for each packet
  - Hence data can be transmitted without any delays
  - That's why it's used in real time communication like voice & video
- The number of circuits that can be established is finite
  - So it has limited scalability
  - And also expensive because it requires dedicated resources
- Examples: Telephone system network

### Multiplexing Methods
- Frequency Division Multiplexing
  - Bandwidth is divided into a series of non-overlapping frequency sub-bands
  - Each sub-band carry different signal
  - Used in radio spectrum & optical fibre
- Time Division Multiplexing (Digital Circuit)
  - Independing signals are transmitted over a common signal path by synchonized switches
  - Used for long distance communication links and bears heavy data traffic

## Packet Switching
- Transferring data to a network in the form of packets
- Data is broken into small pieces of variable length called packet
  - To transfer the data efficiently and minimize the transmission latency
  - These packets may travel through different routes
  - They are reassembled at the destination
- Uses the store and forward technique
  - Packets may get discarded at any hop for some reason
  - So while forwarding the packet, each hop first stores the packet and then forwards
- Advantages
  - Efficient use of bandwidth since it's shared
  - Less expensive than circuit switching since resources are shared
  - Resources are allocated only during data transmission
  - Flexible: Can handle a wide range of data rates and packet sizes
  - Scalable: Can handle large amounts of traffic in a network
- Disadvantages
  - Higher latency than circuit switching since packets are routed through multiple nodes
  - May result in packet loss due to congestion or errors in transmission
  - There can be transmission delay & packet loss, so not ideal for real time communication
- Types of delays
  - Transmission: Time taken by station to transmit data to the link
  - Propogation: Time spent to propogate data through the link
  - Queueing: Time for which a packet waits at the destination's queue
  - Processing: Processing time at the destination

### Connection-oriented Packet Switching (Virtual Circuit)
- Before starting the transmission
  - It establishes a logical path or virtual connection using a signaling protocol
  - Virtual circuit ID is provided by switches/routers
    - To uniquely identify this virtual connection
- There are three phases: connection setup, data transfer, tear down
  - Address information is transferred only during the setup phase
  - Once the route is decided, entry is added
    - To the switching table of each intermediate node
- Resources like buffers, CPU, bandwidth are reserved
  - For the time in which the virtual circuit will be used
  - If many clients are trying to reserve a router's resources simultaneously
    - It can become problematic
- The first sent packet reserves resources at each server along the path
  - Subsequent packets follow the same path as the first packet during the connection
  - Only the first packet requires a global header
  - Since all packets follow a specific path
    - They are received in order at the destination
    - Packets are also appended with sequence numbers
- Used by ATM (Asynchronous Transfer Mode) network, specifically for telephone calls

### Connection-less Packet Switching (Datagram)
- Packet belonging to one flow may take different routes
  - Because routing decisions are made dynamically
  - So the packets arriving at the destination might be out of order
  - All packets are associated with a header
    - Which contains all necessary addressing information
    - Like source & destination address, port numbers
- There is no connection setup, teardown phase, resource reservation like virtual circuits
  - Cost efficient and easy to implement than virtual circuit
- Packet delivery is not guaranteed
  - Packet is discarded if resources like buffer, CUP, bandwidth are not available
  - So reliable delivery must be provided by end systems using additional protocols
- Generally used by IP network, which is used for data services like the internet

## Message Switching
- Developed as an alternative to circuit switching before packet switching was introduced
  - Many major networks used are packet switched or circuit switched
  - But their delivery processes can be message switched (like email systems)
- End users communicate by sending & receiving messages
  - That include the entire data to be shared
  - Each message has a header with information about message routing, source, destination
- Store and forward
  - Intermediate nodes transfer the entire message to the next node
  - Since messages are stored indefinitely, switches require large storage capacity
  - Message is delivered only if sufficient resources are available
    - The next hop and the link connecting it both should be available
- It is slow
  - Each node waits for the entire message to be received
  - After processing the next node depending on availability & traffic
    - It must store & transmit the message
  - Cannot be used for real time communication
- Efficient traffic management by assigning priorities to the messages
