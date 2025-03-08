## ARP (Address Resolution Protocol)
- Finds the hardware address of a host from a known address
  - Network layer to data link layer mapping process
- Most applications use logical address (IP address) to send & receive messages
  - But having IP address is necessary but not sufficient
  - The actual communication happens over the physical address (MAC address)
- ARP Cache
  - After resolving the MAC address
    - ARP sends it to the source where it is stored in a table for future reference
  - The cached MAC address may timeout after sometime

## Working
- It broadcasts a discovery packet to all the devices of the source network
  - Requesting the MAC address of intended destination
  - The packet will be discarded by everyone except the intented receiver host
- The devices peel the header of the data link layer called frame
  - And transfer the packet to the network layer
  - Where network ID of the packet is validated with the destination IP's network ID
- If it's equal
  - It responds to the source with the MAC address of the destination using unicast packet
  - Sender updates ARP cache and starts sending unicast messages to the destination
- Else the packet reaches the gateway of the network
  - And broadcasts packet to the connected devices and validates their network ID

## ARP Spoofing or Poisoning
- Attacker sends a falsified ARP request over LAN
  - Which connects its MAC address to the legitimate server
- After that, the attacker will start receiving the data intended for that IP address
  - It can intercept data frames, modify traffic, stop data in transit
- Can act as the opening for other major attacks
  - Like man in the middle, denial of service, session hijacking

## Types
### Reverse ARP
- Used in LAN by client machines
  - For requesting IP address from the gateway router's ARP table
- Whenever a new machines comes
  - The machine sends a RARP broadcast packet containing its own MAC address
  - A special host configured inside LAN replies to these broadcast packages
  - If an entry is found in the mapping table
    - It sends the response packet with the IP address
- Has been replaced by BOOTP (Bootstrap Protocol) and DHCP

### Proxy ARP
- Resolves IP address to MAC address for devices separated into network segments
  - Connected through a router in the same IP or sub-network
- When devices are not in the same data link layer network but are in the same IP network
  - They try to transmit data to each other as if they were on the local network
  - But the router that separates the devices cannot broadcast messages
    - Because routers do not pass hardware-layer broadcasts
- The proxy router that resides between local networks responds with its MAC address
  - As if it were the router to which the broadcast is addressed
  - The sending device after receiving the MAC address of the proxy router
    - Sends datagram to the proxy router which in turn sends it to the destination device

### Inverse ARP
- Uses MAC address to find the IP address (inverse of ARP)
- Enabled by defualt in ATM (Asynchronous Transfer Mode) networks and frame relays

### Gratuitous ARP
- Used in advance network scenarios and detecting duplicate IP addresses
- Performed by computer while booting up
  - When NIC (Network Interface Card) is powered for the first time
  - It automatically broadcast its MAC address to entire network
- After that, MAC address of the computer is known to every switch
  - And allows DHCP servers to know where to send the IP address if requested

## Packet Flow
- First of all, it is checked if the destination is present in the same network or not
- How the source device will know that
  - AND operation is performed between
    - Source IP address and source subnet mask
    - Destination IP address and source subnet mask
  - If the resultant of both are same then the destination is present in the same network

### Same Network
- It is checked if the ARP has not been resolved or not
- To resolve ARP, ARP request is broadcasted to all the other hosts in the network
  - This generates two packets, one for ICMP & other for ARP
  - The broadcast is performed with the help of a switch
    - Routers don't forward broadcast packets
- The request is received by the target host
  - And it unicasts an ARP reply specifying its MAC address
- The reply is received by the switch and forwarded to the source host
  - The switch is able to do so because it has an entry
    - For the source host in its MAC table
    - This was added when the source host broadcasted the ARP request
- After resolution, the ICMP ack packet is unicasted from the destination to the source host

### Different Network
- The packet is delivered to the default gateway first
  - Which in turn delivers to the destination host
  - MAC address never crosses its broadcast domain
- At the source network
  - It is checked if the ARP has not been resolved or not
  - To resolve ARP, ARP request is broadcasted to all the other hosts in the network
  - This generates two packets, one for ICMP & other for ARP
  - The router accepts the request and unicasts the ARP reply back to the source
  - After resolution, ICMP packet is unicasted to the default gateway
- At the destination network
  - Now the ARP has to be resolved again
    - Because the router has to deliver the packet to the destination host
    - The ARP request is broadcasted in the destination network and the same process follows
  - ICMP echo-request packet is unicasted to the destination host
    - The destination host generates an ICMP echo reply in reponse
    - Which is delivered to the router and then unicasted to the source host
- The MAC addresses of the source & destination are used only till their respective router
  - After that, the router's MAC address is used
