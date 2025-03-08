## Network Layer
- Basic info
  - Packet: Packet, Datagram
  - Protocols: IP, ICMP, ARP
  - Devices: Router, Brouter
- Features
  - Data Route Layer
  - Transmission of data from one host to another located in different networks
  - Packet Routing: Selects shortest path to transmit packets from the available routes
  - Adds the IP addresses of the sender & the receiver in the header

## Functions
- Device Addressing
  - Adds source & destination addresses to the header
  - Identifies devices and tracks device location
- Routing: Determine optimal route based on factors like network condition & priority
- Internetworking: Logical communication between hosts
- Data plane (Forwarding): Within router, move packets from router's input to output
- Control plane (Routing): Determine route of packets from source to destination

## Synchronous Optical Network (SONET)
- Communication protocol used to transmit a large amount of data over large distances
  - Transfers multiple digital streams at the same time over optical fibre
  - Converts electrical signal to optical signal so that it can travel longer distances
- Synchronous network
  - A single clock called PRC (Primary Reference Clock) is used
  - To handle the timing of transmission of signals & equipments across the entire network
- Components
  - Multiplexer: Converts electrical signals to optical signals
  - Demultiplexer: Converts optical signals to electrical signals
  - Regenerator: Repeater that takes an optical signal and increases its strength
  - Add/drop multiplexer
    - Allows to add or remove signals coming from different sources into a given path
- Functional layers
  - Path layer: Movement of signal from optical source to optical destination
  - Line layer: Movement of signal across physical line (between multiplexers)
  - Section layer: Movement of signal across physical section (neigbouring devices)
  - Photonic layer: Physical specifications for the optical fibre channel
