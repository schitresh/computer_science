# TCP (Transmission Control Protocol)
- Connection oriented protocol for communication between different devices in a network
  - Sender & receiver are connected till the completion of the process
  - Order of the data is maintained (order remains same before & after the transmission)
- Establishes and maintains full duplex connection between hosts
  - And generates a virtual circuit between sender & receiver
  - Works with IP that establishes the technique for sending data packets between devices
- Reliable communication using Positive Acknowledgement with Re-transmission (PAR)
  - Detects errors and retransmits the damaged frames
  - Segments are checked for error detection
    - Corrupted segment, lost segment management, out of order segment, duplicate segment
  - Before the transmission is completed
    - Ensures that all segments are received and acknowledged

## Working
- Sender
  - To ensure that each message reaches its target location intact
    - Data/message is divided into small segments
  - It keeps track of the segments by assigning sequence number
  - As opposed to sending everything in one go
    - This makes it simpler to maintain efficiency
- Segments may travel through multiple routes and arrive in different order
  - It makes it easier to route segments if one route is jammed
- Receiver
  - All segments are collected and reordered based on sequence numbers
  - Received segmments are assigned acknowledgement numbers
  - TCP then waits for the transmission to finish
    - And acknowledges once all packets have been received
- Flow control
  - Limits the rate at which a sender transfers data
  - The receiver continually hints on how much data can be received
    - Using a sliding window
- After the user request is received by the server
  - It sends back an HTML page using HTTP
  - HTTP requests TCP layer to set the required connection and send the HTML file

## Connection using 3 way handshake
- Step 1: SYN
  - When a client wants to establish a connection
    - It sends a segment with SYN (Synchronized Sequence Number)
  - This informs the server that the client is likely to start communication
    - And with what sequence number (32-bit number) it starts with
- Step 2: SYN + ACK
  - Server responds to the client request with SYN-ACK signal bits set
  - Acknowledgement (ACK) signifies that the response of the segment is received
  - SYN signifies with what sequence number it is likely to start the segments with
- Step 3: ACK
  - Client acknowledges the response of the server
  - And they both establish a reliable connection
    - With which they will start the actual data transfer

## TCP Timers
- TCP uses several timers during communications
  - To ensure that excessive delays are not encountered

### Retransmission timer
- Retransmission timeout (RTO) is used to retransmit lost segments
- Starts when TCP sends a segment and stops when the ack is received
- This is determined using RTT (Round trip time)
  - Measured RTT: Time taken by segment to reach destination & be acknowledged
  - Smoothed RTT: Weighted average of measured RTT

### Persistent timer
- Used to deal with a zero-window-size deadlock situation
- When TCP receives an ack with window size of zero, it starts a persistence timer
- When it goes off, TCP sends a special segment called probe
  - Probe contains only 1 byte of data
  - It has a sequence number but it's never acked
    - Also ignored in calculating sequence nuumber for rest of the data
- Probe causes the receiver to resend ack which was lost

### Keep alive timer
- Used to prevent a long idle connection between two TCPs
- Each time the server hears from client, it resets the timer (usually 2 hours)
- If the server does not hear from the client after timeout, it sends a probe segment
- If there is no response after 10 probes (75s apart)
  - It assumes that the client is down and terminates the connection

### Time wait timer or quiet timer
- Used during tcp connection termination
- Starts after sending the last ack and closing the connnection
- After connection is closed
  - It is possible for datagrams that are still their way through the network
    - To attempt to access the closed port
  - This timer prevents just closed port from reopening again quickly
    - And receiving these last datagrams
- Usually set to twice the maximum segment lifetime
  - Same value as time-to-live field in IP header

## Connection Termination
- Supports two types of connection releases
  - Like most connection-oriented transport protocols

### Graceful connection release
- Connection is open until both parties have closed their sides of connection
- Carried out by using the TCP header's FIN (finish) flag
- Step 1 (FIN from client)
  - Suppose that the client wants to close the connection
    - Server can also choose to do so
  - Client sends a segment to server with FIN bit set to 1
  - Client enters into FIN_WAIT_1 state and waits for ack from the server
- Step 2 (ACK from server)
  - When the server receives FIN bit segment, it immediately sends ack to the client
  - When the client receives the ack, it enters into FIN_WAIT_2 state
    - And waits for another segment from server with FIN bit set to 1
- Step 3 (FIN from server)
  - After some time of sending ack, server sends FIN bit segment to client
  - The time is taken due to some closing process in the server
- Step 4 (ACK from client)
  - When the client receives FIN bit segment
    - It sends ack to server and enters into TIME_WAIT state
  - TIME_WAIT state lets client resend the final ack in case its lost
    - Typically 30s, 1min, 2min
  - After the wait, the connection formally closes
    - And all resources on the client side (port numbers, buffer data) are released

### Abrupt connection release
- Either an TCP entity is forced to closed the connection
  - Or one user closes both directions of data transfer
- Carried out when an RST (reset) segment is sent
  - When an non-SYN segement is received for a non-exiting TCP connection
  - When a segment with an invalid header is received in an open connection
    - Prevents attacks by closing the corresponding connection
  - When some implementations need to close an existing TCP connection due to
    - Lack of resources or remote host is unreachable & has stopped responding
- RST segement should contain 00 if it does not belong to any existing connection
  - Else it should contain current value of the sequence number
  - And the ack number should be set to the next expected sequence number

## Wrap Around Concept
- At high rate of traffic, all the sequence numbers can get used up
  - Sequence number should be unique for each packet
  - Sequence number is of 32 bits (0 to 2^32 - 1 = 4 Giga numbers)
- Wrap around concept
  - Using the sequence number again and again once all of them get used up
  - In order to maintain the continuity of data transfer
- Wrap around time
  - Time taken to wrap around
    - If we start from sequence number n, after how much time is it used again
  - Depends on the sequence numbers and bandwidth (rate of bits being consumed)
  - It should be at least greater than the life time of a packet
    - For that time the sequence number will be in use
  - Wrap around time = Count of sequence numbers / Bandwidth
    - For 1 GBps = 2^32 numbers / 10^9 = 4.3 seconds
