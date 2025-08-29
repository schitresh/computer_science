# Sliding Window Protocol
## ARQ (Automatic Repeat Request or Automatic Repeat Query)
- ARQ is an error-control strategy used in a two-way communication system
- It is a group of error-control protocols to achieve reliable data transmission
  - Over an unreliable source or service
- These protocols
  - Reside in the transport layer and data link layer
  - Responsible for the automatic retransmission of packets
    - That are found to be corrupted or lost during the transmission process

### Working Principle of ARQ
- The sender receives an acknowledgment from the receiver before timeout
  - Implying that the frame or packet is received correctly
- Timeout is a specific period within which the acknowledgment has to be sent
  - By the receiver to the sender
- If a timeout occurs
  - It is implied that the frame or packet has been corrupt or lost during the transmission
  - And the sender retransmits the packet
  - This process is repeated until the correct packet is transmitted

## Stop and Wait ARQ
- Error and flow control used in connection-oriented communication
- Used in data link layer and transport layer
- Implements sliding window protocol with window size 1

### Metrics
- Propogation Delay: Time taken by a packet from one router to another router
- Round Trip Time (RTT)
  - Time taken by a packet to reach the receiver
  - And the acknowledgement to reach the sender
- Time Out: 2 * RTT
- Time to Live (TTL): 2 * Time Out (Maximum TTL is 255 seconds)

### Simple Stop and Wait
- Sender
  - Sends one packet at a time
  - Sends the next packet only after receiving acknowledgement for the previous one
- Receiver
  - Sends acknowledgement (ack) after receiving and consuming a packet
- Problems
  - If a packet is lost
    - Sender keeps waiting for ack and receiver keeps waiting for packet
  - If an ack is lost, sender keeps waiting for ack
  - If a packet or an ack is delayed (after timeout)
    - It might be considered wrongly for some other recent packet

### Stop and Wait with ARQ (Automatic Repeat Request)
- Solves the problems of the simple stop & wait
  - Sequence number is added to each packet
    - Which solves the delayed packet or ack problem
  - If a packet is lost, the packet is retransmitted after time out
  - If an ack is lost
    - Receiver sends ack instead of negative ack by considering sequence number
  - If an error is detected
    - Receiver sends a negative acknowledgement (nak) to request retransmission
- Working
  - Sender sends a packet with sequence number 0
  - Receiver sends an ack with sequence number 1
    - That is the seq number of next expected packet
  - 0 or 1 is a one bit seq number
    - It implies that both sender & receiver have a buffer for one packet only
  - So, the sender will send seq number 0, then 1, then 0, and so on
- May cause performance issues
  - Due to sequenced sending of packets and waiting for ack

## Sliding Window Protocol
- Handles the performance & efficiency issue in stop & wait ARQ
  - By sending multiple packets at a time
- Types
  - Go back N ARQ
  - Selective repeat ARQ

### Metrics
- Transmission Delay
  - Time to transmit the packet from the host to the outgoing link
  - T(t) = D / B (D = data size to transmit, B = bandwidth of the link)
- Propagation Delay
  - Time taken by the first bit from host to reach the destination
  - T(p) = d / s (d = distance, s = wave propagation speed of the medium)
- Total Time
  - Transmission (data + ack) + Propagation (data) + Propagation (ack)
  - TT = T(t) + 2 * T(p)
- Efficiency: Useful time / Total time, i.e. T(t) / TT
- Effective Bandwidth or Throughput
  - Number of bits sent per second
  - Throughput = D / TT = Efficiency * Bandwidth

### Pipelining
- Window size = Number of packets in one cycle
  - One packet is transmitted in T(t) time
  - W = TT / T(t) = 1 + 2 * (T(p) / T(t))
  - W = 1 + 2a, where a = T(p)/T(t)
- After receiving ack for packet 0
  - Sequence number are reused so that header size can be kept minimum
  - Window slides and next packet is assigned seq number 0
- Can be represented with a diagram
  - Draw a vertical line on LHS for sender (S) and another one on RHS for receiver (R)
  - The vertical axis represents time starting from the top as the initial time
  - For packet 0, draw a line from S at T(0) which touches R at T(p)
  - Draw similar lines for all the packets in a window and for acks

## Go Back N ARQ
- Window sizes
  - Sender window (WS) = N
  - Receiver window (WR) = 1
- Example with sender window size as 4
  - Sender sends packets 0, 1, 2, 3
  - Receiver sends ack for 0, 1 and is expecting packet 2
  - After receiving ack for 0, 1, the sender window slides to transmit packets 4, 5
  - Let's say the packet 2 is lost in the network
    - So, the receiver will discard all the packets after packet 2
    - On the sender side, the time-out timer will expire for packet 2
  - Hence, the sender window will go back to the packet 2 and resend all packets till 5
    - So, it goes back N times (packets 2, 3, 4, 5) from the last transmitted packet
- Acknowledgements
  - Cumulative ack
    - One ack is used for many packets
    - It reduces the traffic but is less reliable
      - Because if this one ack is lost, all the sent packets are treated as lost
  - Independent ack
    - Each packet gets an ack independently
    - Reliability is high but traffic is also high
- Minimum sequence numbers required = N + 1
  - Let's say receiver gets all the packets (0, 1, 2, 3) for window size 4
  - While it's waiting for packet 0 again, let's say cumulative ack is lost in the network
  - After timeout on the sender side, all the 4 packets will be transmitted again
  - And the receiver is also waiting for new set of packets starting from 0
  - Which will result in duplicates (old 0 is retransmitted and new 0 is expected)
  - To avoid this, one extra sequence number is required

## Selective Repeat ARQ
- Go back N protocol works well if errors are less
  - But if the line is poor, it wastes a lot of bandwidth on retransmitted frames
- Allows receiver to accept & buffer the frames following a damaged or lost one
  - Retransmits only those packets that are actually lost
  - Receiver must be able to accept packets out of order
- Retransmission requests
  - Implicit
    - Receiver acks every good packet
    - Packets that are not acked before time-out are assumed lost or erred
  - Explicit
    - NAK (selective reject) requests retransmission of just one packet
    - This can expedite retransmission but is not strictly needed
- Window sizes
  - Sender window = Receiver window
  - Window size should be less than or equal to half the sequence number
  - This is to avoid packets being recognized incorrectly
    - Receiver may recognize new packets as retransmissions
- Efficiency is same as Go back N
