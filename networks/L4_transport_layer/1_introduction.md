## Transport Layer
- Basic info
  - Packet: Segment
  - Protocols: TCP, UDP
  - Platforms: OS, Gateways, Firewalls
- End to end communication layer
  - Reliable message delivery from process to process
  - Ensures messages are in order and without duplication
  - End-to-end (not across single link) delivery, flow control and error control
  - Acknowledges successful data transmission
  - And re-transmits the data if an error is found
- Provides services to application layer by making system calls
  - And takes services from network layer
- Service-point addressing
  - Allows computers to run several programs simultaneously
  - Logical communication between processes

### Process to process delivery
- Requires port number to correctly deliver the segments of data
  - To the correct process amongst the multiple processes running on a particular host
- Port number is 16-bit address used to identify any client-server program uniquely
- This is similar to data link layer requiring MAC address
  - And network layer requiring IP address

## Workflow
- At the sender side
  - Receives the formatted data from the upper layers and performs segmentation
  - Implements flow & error control
  - Adds source and destination port numbers (or service point address) in the headers
    - This is called service point addressing
    - The destination port number is configured either by default or manually
  - Forwards the segmented data to the network layer
- At the receiver side
  - Receives data from the network layer
  - Reads the port number from the header and forwards the data
  - Performs sequencing and reassembling of the segmented data
  - Forwards the message to appropriate port in the application layer

## Services
- Connection-oriented service
  - Three phase process: establish connection, transfer data, disconnect
  - Reliable and secure
  - Receiving device sends an acknowledgement to the source
  - Before delivering the packets
    - Connection is made with transport layer at the destination
  - All the packets travel in the single route
- Connection-less service
  - One phase process: data transfer
  - Receiving devices does not acknowledge receipt of a packet
  - Faster communication
  - Each segment is treated as an individual packet
  - Packets travel in different routes to reach the destination

## Multiplexing/Demultiplexing
- Multiplexing (many to one) at sender
  - Data is acquired from several processes (or sockets) from the sender
    - And merged into one packet along with headers
    - And sent as a single packet
  - Allows simultaneous use of different processes running on a host over a network
    - The processes are differentiated by their port number
- Demultiplexing (one to many) at receiver
  - Header info is used to deliver segments to correct sockets or processes
    - That are running on the receiver's machine
  - Host receives IP datagrams
    - Source IP, destination IP, segment(source port, destination port)

## Error and Flow Control
- Checks errors in messages coming from the applcation layer by
  - Using error detection codees
  - Computing checksumes
  - Checking if the received data is corrupted
  - Using ACK & NACK services to inform the sender

### Protocols
- Stop-and-wait
- Sliding Window
- Go-back-N
  - Receiver sends cumulative ack
  - Sender can have up to N unacked packets in pipeline
  - Sender has timer for oldest unacked packet
  - When timer expires, it retransmits all packets starting from the unacked one
- Selective repeat
  - Receiver sends individual ack
  - Sender has timer for each unacked packet
  - When timer expires, retransmit the unacked packet only
