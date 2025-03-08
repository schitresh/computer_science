## Computer Networks
- Collection of computers & devices connected together to enable communication and data exchange
- System connected to network and ready for communication is called open system (vs closed system)
- Basic building blocks of a computer network are nodes and links
  - Nodes: Devices capable of sending & receiving data like computers, servers, printers, routers, switches
  - Links: Wires, cables, wireless networks

## Basic Terminology
- Protocol
  - A set of rules and standards that govern how data is transmitted over a network
  - Examples: TCP/IP, HTTP, FTP
  - Protocol Data Unit: Single unit of information transmission among peer entities
- Topology
  - Physical and logical arrangement of nodes in a network
  - Examples: Bus, star, ring, mesh, tree
- IP Address (Internet Protocol Address)
  - Unique numerical identifier that is assigned to every device in a network
  - Used for identification & communication
- MAC Address (Media Access Control Address)
  - Unique identifier of each host associated with its Network Interface Card (NIC)
  - Used to identify a device in a local network
- DNS (Domain Name System)
  - Translates human readable domain names to IP addresses that computers can understand
  - For example, getting the IP address of www.google.com
- Dynamic Host Configuration Protocol (DHCP)
  - Automatically assigns IP addresses and network configuration settings to devices in a network
- Firewall
  - Monitors & controls incoming & outgoing network traffic
  - Protects networks from unauthorized access and other security threats

## Network Criteria
- Performance
  - Transit time: Time for a message to travel from one device to another
  - Response time: Time elapsed between an inquiry and a response
  - Throughput: Rate of message delivery
  - Delay
  - Factors
    - Number of users
    - Transmission medium and distance
    - Hardware or software limitations
    - Bandwidth (Capacity of network)
    - Topology and protocols
    - Congestion
- Reliability
  - Failure frequency
  - Recovery time after failure
  - Reducing single points of failure
- Security
  - Authentication
  - Authorisation
  - Damage and recovery

## Internet
- Global network of smaller networks interconnected using standardized protocols
- Allows people to communicate, share information, and access resources from anywhere in the world
- Consists of private, public, academic, business and government networks of local to global scope

## World Wide Web (WWW)
- Provides a way to access information through internet
- Only a subset of internet is connected through the web
- System of internet servers that support specially formatted documents in HTML
  - Which are interlinked using hypertext links and are accessible via internet
- HTML (HyperText Markup Language): Markup language in which the documents are formatted
- HTTP (HyperText Transfer Protocol): Transfer protocol
- URI (Uniform Resource Identifier): Address of resource, can be a name or location or both
- URL (Uniform Resource Locator)
  - Human readable text designed to substitute the IP addresses
  - protocol://website_name.top_level_domain/path
  - https://youtube.com/videos/id

## Working of Browser
### Step 1: Client-side
- We type a URL and the browser converts it to a file containing
  - GET /HTTP/1.1 (1.1 refers to the version of HTTP)
  - Host (www.google.com)
  - Other information
- If connected to ethernet
  - It is converted to binary code and sent down the wires
- If connected to wifi
  - It is converted to a radio-signal which is decoded by a router in a very low level
  - It is then converted to binary code and sent to the servers
- It is transmitted through routers until it reaches the destination

### Step 2: Server-side
- Receives the binary code and decodes it
- Generates a response
  - HTTP/1.1 200 ok
  - Content-type: type/html
  - Body of the page
- Converts it to binary and sends it to IP requesting it

### Step 3: Client-side
- Receives the response and decodes it
- Checks the status
- Starts reading the html and constructs a tree like structure
- The HTML tree is converted to binary code and rendered on screen
