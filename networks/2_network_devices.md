## Domains
- The more the number of collision domains & broadcast domains
  - The better bandwidth the network provides

### Collision Domain
- When a device sends out a message to a network
  - All the other devices in its collision domain have to pay attention to it
  - No matter if it was destined for them or not
- When two devices send out their messages simultaneously
  - Collision will occur leading them to wait and retransmit their messages one at a time
  - It happens only in the case of half duplex mode

### Broadcast Domain
- When a device sends out a broadcast message
  - All the devices present in its broadcast domain have to pay attention to it
- It creates a lot of congestion in the network (commonly called LAN congestion)
  - It affects the bandwidth of the users present in that network

## Basic Network Devices
- Cables and connectors
- Modem: Connects computer to internet over telephone line

## Network Interface Card (NIC)
- Operates at physical and data link layer
- Helps computer to connect to network and communicate with other devices
- Contains hardware addresses (MAC address) used by data link layer
- Has a connector to connect a cable
  - That acts as an interface between the computer and the router or modem

## Repeater
- Basic info
  - Operates at physical layer
  - Two ports (input & output)
  - Collision domain and broadcast domain remains same
- Regenerates the signal over the same network before it becomes too weak or corrupted
- Not only amplifies the signal but also regenerates it by copying it bit by bit

## Hub
- Basic info
  - Operates at physical layer
  - Basically a multi-port repeater
  - Collision domain and broadcast domain remains same
- Connects multiple devices from different branches or wires
  - Computer request is sent to hub which distributes it to interconnected computers
- Cannot filter data so data packets are sent to all the connected devices
- Does not have capability to find out the best path for data packets

### Types
- Active Hub
  - Has their own power supply
  - Can clean, boost, relay signal along a network
  - Serves as a repeater as well as a wiring center
  - Used to extend the maximum distance between nodes
- Passive Hub
  - Collects wiring from nodes and power supply from the active hub
  - Relays signals onto a network without cleaning or boosting them
  - Can't be used to extend distance between nodes
- Intelligent Hub
  - Works like an active hub and includes remote management capabilities
  - Provide flexible data rates
  - Enables an administrator to monitor the passing network

## Bridge
- Basic info
  - Operates at data link layer
  - Two ports (input & output)
  - Breaks only collision domain, broadcast domain remains same
- Repeater with functionality of filtering content
  - By reading the MAC address of the source & destination
- Local internetworking device used to connect network segments together
  - Used where the full power of router is not required (e.g. within the same organization)
  - Uses MAC addresses to make forwarding decisions
  - Hosts are unaware of the bridges and it appears to them as a single network
- Also used to divide large networks into smaller segments
  - To improve network performance and reduce network congestion

### Types
- Transparent Bridge
  - Stations are completely unaware of the bridge's existence
  - Makes use of bridge forwarding and bridge learning
- Source Routing Bridge
  - Routing operation is performed by the source station
  - Frames specify which route to follow
  - Hosts can discover the frame by sending a special frame called discovery frame

## Switch
- Basic info
  - Operates at data link layer
  - Multiport bridge with a buffer and a better efficiency
  - Every port is in different collision domain but the broadcast domain remains the same
- Groups all devices over network to transfer data to another device
  - Can perform error checking before forwarding data
  - Doesn't broadcast over network like hub
- Sends message to the destination device based on the MAC address
  - Learns the MAC address of the device on the switch port on which it received the frame

## Types
- Unmanaged: Simple configuration, suitable for small networks
- Managed: Advanded configuration like VLAN, QoS, suitable for large networks
- Layer 2: Operate at data link layer, forwards data between devices on the same network segment
- Layer 3: Operate at network layer, can route data between different network segments
- There are many other types of switches for different functionalities

## Router
- Basic info
  - Operates at network layer
  - Most routers include many ports that can connect a variety of devices to internet
  - It separates both the collision domain and the broadcast domain
- Connects two or more network segments like LANs to a single network
  - Device like switch that routes data packets based on their IP addresses
- By sending data packets to their intended IP addresses
  - It manages traffic between different networks
  - And permits several devices to share an internet connection
- Whenever a web request (packets) is sent from a browser
  - It goes through a series of routers which accept these packets
  - And forwards them to a correct path
- Working
  - Examines the destination IP address from the header of a packet
    - And compares it to the routing database
  - A list of routing tables outline how to send data to a specific network location
    - Dynamic routing tables are updated by dynamic routers based on network activity
    - Static routing tables are configured manually

## Bridging Router (BRouter)
- Operates at data link and network layer
- Combines features of both bridge and router
- Capable of routing packets across networks as router and filtering LAN traffic as bridge

## Gateway
- Operates at network layer, also call protocol converters
- Passage to connect two networks that may work upon different networking models
- Works as messenger agent that take data from one system
  - Then interpret it and transfer to another system
- Generally more complex than switches or routers
