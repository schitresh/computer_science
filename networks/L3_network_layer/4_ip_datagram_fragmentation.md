## IP Datagram Fragmentation
- Different networks may have different maximum transmission unit (MTU)
  - For example, it can be due to differences in LAN technology
  - MTU determine the maximum size of a data packet that can be transmitted over that network
- When one network wants to transmit datagrams to a network with a smaller MTU
  - The routers on the path may fragment and reassemble datagrams
- Each of the fragments contain a portion of the original packet
  - Along with additional info that identifies a fragment's position in the original packet
  - And how it fits into the sequence of fragments
- Done by the network layer at the destination side, usually at the routers
- Source side does not require fragmentation due to segmentation by transport layer
  - Segmentation is done in such a way that
    - Resulting data can easily fit in a frame without the need of fragmentation

## Delays
- Fragmentation can cause delays and other network issues
- Increased processing and memory overhead from the network devices involved in transmission
- Increased likelihood of packet loss or corruption
  - Since each fragment is transmitted separately
- If any fragments are lost or corrupted
  - The entire packet must be retransmitted which can introduce delays & network congestion
- Reassembly delays especially if there are delays in receiving all the fragments
  - Or if they arrive out of order

## Avoiding Delays
- To avoid these issues, it is generally recommended to avoid fragmentation whenever possible
- By ensuring that packets are appropriately sized for the network links they will traverse
- This can be done through path MTU discovery
  - It allows devices to determine the maximum packet size
  - That can be transmitted without fragementation on a given network
- Additionaly, QoS mechanisms can be implemented
  - To prioritize traffic and reduce delays by congestion

## Working
- When a packet is received at the router, destination is examined and MTU is determined
- If the size of the packet is bigger than MTU
  - 'Do not fragment' (DF) bit is set to 0 in header
  - Packet is fragmented into parts and sent one by one
  - Maximum size of each fragment is (MTU - header size)
- Each fragment is converted to a packet
  - Total length field is changed to the size of the fragment
  - 'More fragment' (MF) bit is set for all the fragment packets except the last one
  - Fragment offset field is set based on the number of fragments, which is used to identify the sequence of frames
  - Header checksum is re-calculated
- Reassembly of fragment takes place only at the destination
  - And not at routers since packets take an independent path
