## Open Systems Interconnection (OSI) Model
- Basic info
  - Acts as a reference model
  - Not implemented on internet because of its late invention
  - The current model being used is the TCP/IP model
- Software or Upper layers
  - Application, presentation, session layers
  - Responsibility of host
- Hardware or Lower layers
  - Transport, network, data link, physical layers
  - Responsibility of network

## Flow of Data
- The data to be transferred travels through 7 layers of the model
  - First it travels down the layers from the sender
  - And then climbs back the layers towards the receiver

### Example: X sends an email to Y
- Application: X sends an email using an application like gmail
- Presentation: Mail application prepares for data transmission like encryption & formatting
- Session: Connection is established between the sender and the receiver on internet
- Transport
  - Email data is broken into small segments
  - Sequence number and error checking info is added to keep the data reliable
- Network: Addressing of packets is done to find the best route for transfer
- Data Link
  - Data packets are encapsulated into frames
  - MAC address is added for local devices
  - Errors are detected
- Physical
  - Data is transmitted in the form of electrical or optical signals
  - Over a network medium like ethernet or wifi
- After the email reaches the receiver
  - The process is reversed
  - The email content is decrypted and shown to the receiver

## Physical Layer
- Physical medium through which bits are transmitted
- PDU (Protocol Data Unit): Bit
- Devices: Cables, Fibers, Wirelessm Modem, Repeater, Hub

## Data Link Layer
- Error free transfer of data frames
- PDU: Frame
- Devices: NIC/Adaptor/Chip, Device driver, Bridge, Switch
- Addressing: MAC address

## Network Layer
- Moving packets from source to destination
- PDU: Packet, Datagram
- Devices: Router, Brouter
- Addressing: IP address
- Protocols: IP, ICMP, ARP

## Transport Layer
- Reliable message delivery from process to process
- PDU: Segment
- Devices: OS, Gateways, Firewalls
- Addressing: Port Number
- Protocols: TCP, UDP

## Session Layer
- Establish, manage and terminate sessions
- Packet: Data
- Devices: OS, Gateways, Firewalls
- Protocols: SSL, API

## Presentation Layer
- Translation, compression, encryption
- Packet: Data
- Devices: OS, Gateways, Firewalls
- Protocols: SSL, SSH, IMAP

## Application Layer
- Services for the user
- Packet: Data
- Devices: Network applications, Browser, Messenger, Gateways, Firewalls
- Protocols: HTTP, DHCP, FTP, SSH, SMTP, DNS
