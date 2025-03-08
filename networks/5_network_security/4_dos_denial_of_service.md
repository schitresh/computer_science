## Denial of Service (DoS)
- Renders a network, host or other pieces of infrastructure unusable by legitimate users
- May target servers, routers or communication links
- Example
  - Ping of death: Uses pings with malformed ICMP packets of non standard sizes
  - Smurf attack: Sending emails with fake return addresses and automatic responses

### Types
- Vulnerability attack
  - Well-crafted messages are sent to a vulnerable application or operating system
    - Running on a targeted host
    - To stop or crash the service
- Bandwidth flooding

  - Target's access link becomes clogged and legitimate packets cannot reach the server
- Connection flooding
  - A large number of half or fully open TCP connections are established
  - The host becomes bogged down with these bogus connections
    - And stops accepting legitimate connections

## DDoS (Distributed DDoS)
- Multiple compromised systems are used to target a single system causing a DoS
- Can leverage botnets with thousands of comprised hosts
- Harder to detect and defect against than DoS attack from a single host

### Types
- Application layer attacks
  - Responding to a request takes a considerable load for the server
    - To build webpages, compute queries, load the results form database
  - But a client can generate and send multiple requests without any load
  - Examples: HTTP flood attack, attack on DNS services
- Protocol attacks
  - Focus on vulnerabilites in layer 3 & 4
  - Consume resources like servers, firewalls, load balancers
  - Examples: SYN flood attack, ping of death
- Volumetric attacks
  - Consumes network bandwidth and saturates it by amplification or botnet
  - Directs a massive amount of traffic to target server
  - Examples: NTP amplification, DNS amplification, UDP flood attack, TCP flood attack

### Common Attacks
- SYN flood attack
  - Exploits TCP handshake by sending SYN messages with a spoofed IP address
  - The victim server keeps on responding but does not receive a final acknowledgement
- HTTP flood attack
  - Multiple HTTP requests are generated simultaneously against a server
  - This exhausts network resources of that server and fails to serve actual requests
- DNS amplification
  - DNS server is requested from a spoofed IP address
  - The request is structured such that the DNS server responds with a large amount of data

### Mitigation
- Preventing DDoS attack is harder than DoS attack since traffic comes from multiple sources
  - And it becomes difficult to separate malicious hosts from actual hosts
- Blackhole routing: All traffic is diverted to a black hole where it gets lost
- Rate limiting
  - Controls the rate of traffic and reduces the pace of web scrapers and brute force logins
  - Unlikely to prevent compound DDoS attacks
- Blacklisting / whitelisting IP addresses
