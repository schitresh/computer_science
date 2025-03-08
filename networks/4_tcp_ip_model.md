## TCP/IP Model
- Basic info
  - The OSI model just acts as a reference model because of its late invention
  - Used to transfer data reliably and accurately from one device to another
  - Divides data into packets at the sender and recombines them at the receiver
- Protocols
  - TCP (Transmission Control Protocol): Sends an receives data
  - IP (Internet Protocol): Finds the destination of the data

## Network Access Layer
- OSI counterparts: Data link, Physical
- Physical layer: Responsible for generating the data and requesting connections
- Data link layer: Error prevention and dividing data into frames

## Network or Internet Layer
- OSI counterparts: Network
- Protocols: IP, ICMP, ARP
- Responsible for routing data packets from one device to another across a network

## Transport Layer
- OSI counterparts: Transport
- Protocols: TCP, UDP
- Exchanges data receipt acknowledgements
- Retransmits missing packets to ensure that packets arrive in roder and without error

## Application Layer
- OSI counterparts: Application, Presentation, Session
- Protocols: HTTP, HTTPS, FTP, SSH, SMTP, DNS, DHCP
- Responsiible for end to end communication and error free delivery of data
- Shields the upper layer applications from the complexities of data
- Also called Process or software layer
