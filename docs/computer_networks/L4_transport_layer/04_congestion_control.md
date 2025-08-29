# Congestion Control
- Congestion is a situation when too many sources attempt to send data
  - And the router buffer starts overflowing
  - Due to which packets are lost
  - Retransmission of packets from the sources increases the congestion further

## Policy
### Slow Start Phase
- After every RTT, the congestion window size increments exponentially
- If congestion window is 1 segment & first segment is acked, window becomes 2 segments
- If next transmission of 2 segments is also acked, it doubles to 4, then 8, and so on

### Congestion Avoidance Phase
- After the threshold value, the congestion window increases additive
- If congestion window is 20 segments
  - And all segments are acked within RTT, it increases to 21 segments
- If the next transmission is also acked, it increases to 22, and so on

### Congestion Detection Phase
- If congestion occurs, the congestion window size is decreased multiplicative
- The only way a sender can guess that congestion has happened is the need to retransmit
- Retransmission can occur when
  - RTO timer times out
    - Congestion possibility is high
    - Threshold is reduced to half of the current window size
    - Congestion window is set to 1
    - Slow start phase is started again
  - Three duplicate ACKs are received
    - Congestion possibility is less
    - Threshold is reduced to half of the current window size
    - Congestion window is set equal to threshold
    - Congestion avoidance phase is started again

## Algorithms
- These two algorithms are used for traffic shaping
  - That is, control the amount & rate of traffic sent to network

### Leaky Bucket Algorithm
- Controls the rate at which traffic is sent to the network
  - And shape the burst traffic to a steady traffic stream
- Each network contains a leaky bucket
  - When host wants to send packet, the packet is thrown into the bucket
  - The bucket leaks (transmits packets) at a constant rate
  - Bursty traffic is converted to uniform traffic

### Token Bucket Algorithm
- When large bursts arrive, the leaky bucket algorithm can lose packets
  - This can happen if rate of traffic > rate of transmission of leaky bucket
  - Since leaky bucket converts traffic to uniform traffic (fixed rate)
- Bucket contains tokens which define a packet of predetermined size
  - Tokens in the bucket are deleted for the ability to share a packet
  - No token means no flow sends its packets
- Tokens are generated at a fixed rate
  - If there is no traffic, accumulated tokens could result in wasted resources

## Open Loop Techniques
- Applied to prevent congestion before it happens
- Retransmission Policy
  - Packets are retransmitted if a sent packet is lost or corrupted
  - To prevent congestion, retransmission timers must be designed efficiently
- Window Policy
  - Several packets in go-back-n window are resent
    - Although some of these packets may have been received successfully
  - This duplication may increase the congestion
  - Selective repeat window should be adopted
    - As it sends only the specific lost packets
- Discarding Policy
  - Routers can discard less sensitive or corrupted packages to prevent congestion
- Acknowledgement Policy
  - The receiver can send cumulative ack for n packets rather than single acks
  - It should send an ack only if it has to send a packet or timer expires
- Admission Policy
  - Switches in a flow should first check the resource requirement
    - Of the network flow before transmitting it further
  - If there is a chance of congestion
    - It should deny establishing a virtual network connection

## Closed Loop Techniques
- Used to alleviate congestion after it happens
- Backpressure
  - Node to node congestion control that propogates in the opposite direction of data flow
  - The congested node stops receiving packets from upstream node
  - This may cause upstream node to become congested and reject data from above nodes
  - Can be applied only to virtual circuit
    - Where each node has info of its above upstream node
- Choke Packet
  - Packet sent by a node to the source to inform about congestion
  - Applicable to both virtual network and datagram subnets
  - Each router monitors its resources and utilization at each of its output lines
  - Whenever the resource utilization exceeds the threshold value set by administrator
    - The router directly sends a choke packet to the source
    - Giving the source feedback to reduce the traffic
  - The intermediate nodes through which the packet has travelled
    - Are not warned about congestion
- Implicit Signaling
  - There is no communication between the congested nodes and the source
  - The source guesses the congestion (e.g. not receiving acks for several packets)
- Explicit Signaling
  - Node experiencing congestion explicitely sends a packet
    - To source or destination to inform about the congestion
  - Difference from the choke packet
    - The signal is included in the packets that carry data
    - Rather than creating a different packet (choke packet)
  - Forward signaling: in the direction of congestion (destination is warned)
  - Backward signaling: in the opposite direction of congestion (source is warned)
