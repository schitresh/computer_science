## Virtual LAN (VLAN)
- Dividing devices in a network logically on layer 2 (data link layer)
- Broadcast domain
  - Broadcast domain is a network segment
    - In which all the devices in that domain receive a packet broadcasted by a device
  - But it is limited to switches only as routers don't forward a broadcast packet
  - Generally, layer 3 devices divide the broadcast domain
    - But it can also be divided by switches using VLAN
- Through VLAN, different small sized sub-networks are created
  - Which are comparatively easy to handle
  - Devices that understand VLAN formats & membership are called VLAN aware
- Three ways to connect devices in a VLAN
  - Trunk link: All connected devices must be VLAN aware
  - Access link: Connects VLAN unaware devices to VLAN aware bridge
  - Hybrid link: Both VLAN aware & unware devices are attached
- Reduces the need to send traffic to unnecessary destinations and saves bandwidth
  - For example, the traffic is intended for 2 devices
    - But 10 devices are present in the broadcast domain
- Useful to form virtual groups in an organization based on departments like sales, finance
  - Allows to control broadcast domains, set up firewalls & restrict access
  - Eliminates the need for expensive routers to create specific broadcast domains

## Inter VLAN Routing
- Required for communication between different VLANs
- Switch Virtual Interface (SVI)
  - Logical interface on a multilayer switch that processes packets on all switch ports
  - Provides only management services like creating VLAN or telent/SSH services on layer 2
  - Provides both management and routing services on layer 3

## Private VLAN
- Used when some hosts should not be able to communicate with other hosts in the same VLAN
- There is a primary or promiscuous VLAN to which all the ports are connected
- Secondary VLANs provide isolation between the ports
  - Isolated VLANs
    - Cannot communicate with other hosts directly
    - Can communicate only with with associated promiscuous port
  - Community VLANs: Can communicate with each other and associated promiscous port

## Switch Ports
- Access ports
  - Carry the traffic of only the one native VLAN (known as VLAN 1)
- Trunk ports
  - Carry the traffic of more than one VLAN
  - Useful if required to exchange traffic between more than one switch
  - VLAN identification method is used to identify traffic for a VLAN
