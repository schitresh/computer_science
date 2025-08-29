## Application Layer
- Basic info
  - Packet: Data
  - Protocols: HTTP, DHCP, FTP, SSH, SMTP, DNS
  - Platforms: Network applications, Browser, Messenger, Gateways, Firewalls
- Features
  - Data produced by applications which needs to be transferred over the network
  - Provides services to the user like file transfer, mail services, etc.
  - Window for users and applications to access network services
  - Network transparency, resource allocation
  - Also called Desktop Layer
- Addressing
  - Socket: Process sends/receive message to/from its socket
- Functions
  - DNS (Domain Name System): Host Name to IP mapping
  - File transfer, access and management
  - Mail services
  - Directory services: distributed database sources

## NTP (Network Time Protocol)
- Helps computer clock times to be synchronized in a network
- Uses UTC to synchronize CPU clock time
- Provides consistent timekeeping for file servers
- Hierarchical system of time resources
  - At the topmost level, there are highly accurate time resources
    - Atomic or GPS clocks
  - These servers (stratum 0) are linked to the servers below
    - Stratum 1, 2, 3 & so on

## Quality of Service (QoS)
- Traffic control mechanisms
  - That differentiate performance based on application or network operator requirements
  - Or provide predictable or guaranteed performance
    - To applications, sessions, traffic aggregates
  - Basic phenomenon is in terms of packet delay and losses of various kinds
- Used for time critical applications in which bounded delay is an important factor
  - Video & audio conferencing or streaming requires bounded delay and loss rate

### Types
- Stateless solutions
  - Routers maintain no fine-grained state about traffic
  - Scalabe and robust
    - But no guarantee about the kind of delay or performance in a particular application
- Stateful solutions
  - Routers maintain per-flow state
  - Much less scalable & robust
    - But guaranteed services and high resource utilization

## Web Caching
- Substantially reduces response time and traffic for repeated requests
- Done by proxy server (intermediate entity between the original server & client)
  - If a request is cached
    - Proxy server forwards the cached result directly to the client
  - Otherwise it queries on behalf of the host
    - Caches it and forwards the result back to the host
- Usually installed by ISP, universities, corporate offices
- What if the content was modified on the original server
  - Conditional GET is used
    - Which queries the original server to get the last modified since
  - The original server returns the data
    - Only if the validator for last modified since passes
  - If the content was modified, it updates the cache and forwards to the client
