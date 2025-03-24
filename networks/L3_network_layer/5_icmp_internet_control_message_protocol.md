## ICMP (Internet Control Message Protocol)
- Mostly utilized on network equipment like routers for error handling
  - Provides hosts with information about network problems
  - Encapsulated within IP datagrams with specific headers & data
  - Helps in network diagnosis by using traceroute and ping utility
- IP depends on ICMP for sending error and control messages
  - Because it does not have an inbuilt mechanism for it
- Connection-less protocol
  - Doesn't need to establish a connection
    - With the destination device before sending a message

## Types of Messages
- Source Quench Message
  - Request to decrease traffic rate for messages sent to the host destination
  - When the congested router is far away from the source
    - ICMP will send this message hop by hop
    - So that every router reduces the speed of transmission
- Parameter Problem Message
  - When a packet comes to a router
    - The calculated header checksum should be equal to the received header checksum
    - If there is a mismatch, the packet is dropped by the router
  - ICMP informs the source about this by sending a parameter problem message
- Redirection Message
  - If a host tries to send data through router R1
  - And if R1 sends data to R2 and there is a direct way from the host to R2
  - Then R1 will send a redirect message to the source to inform about the best route
- Other messages
  - Time exceeded
  - Destination unreachable

## Traceroute
- Traces a packet from computer to host
  - And shows the number of hops & time required to reach there
- Works by sending packets with low survival time i.e. time to live (TTL)
  - It specifies how many hops can the packet survive
  - When the packet expires
    - The node where it expired returns the packet and identifies itself
  - By increasing the TTL gradually, it is able to identify intermediate hosts
  - If any of the hops returns with 'request timed out', it denotes netowork congestion

## Ping
- Helps to check if a particular IP address is accessible or not
- Works by sending a packet to the specified address and waits for a reply
- Measures round trip time and reports errors
- Also used to check if the computers on a local network are active
