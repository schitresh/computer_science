## Firewall
- Network security device
  - That prevents unauthorized access to a network
  - Monitors both incoming & outgoing traffic to detect and prevent threats
  - Can be either hardware or software based
- Actions
  - Accept: Allow th traffic
  - Reject: Block the traffic and reply with an unreachable error
  - Drop: Block the traffic with no reply
- History
  - Before firewalls, network security was performed by ACLs residing on routers
  - ACL: Access Control List
  - ACL rules can determine whether network access should be granted or denied
  - But they cannot determine the nature of the packet it is blocking
  - And they do not have capacity to keep threats out of the network
  - Hence, firewall was introduced

## Working
- Firewall matches the network traffic against the set rules defined in its table
- Maintains distinct set of rules for outgoing and incoming traffic
- Most traffic that reaches on the firewall
  - Is one of the three major transport layer protocols
  - TCP, UDP, ICMP which all have a source & a destination address
  - TCP & UDP have port numbers while ICMP uses type code instead of port number
- It is difficult to explicitly cover every possible rule
  - Hence a firewall must always have a default policy

## Types
- Static Packet Filtering
  - Monitors outgoing & incoming packets to control network access
    - Works on the network & transport layer
  - Based on source & destination IP address, protocols, ports present in IP headers
    - Maintains a filtering table with these attributes
    - To decide if a packet will be forwarded or discarded
- Stateful Packet Filtering
  - Based on the same attributes as static packet filtering
  - Determines the connection state of packet travelling across it like TCP streams
  - Which makes it more efficient than packet filtering
  - So the filtering decisions are based on defined rules
    - As well as packet's history in the state table
- Application Gateways or Proxy Firewalls
  - Multiple application gateways can run with separate servers on the same host
  - Examines & filters packets on any OSI layer upto application layer
  - Recognizes when certain application and protocols are being misused
- Next Generation Firewalls (NGFW)
  - Deep packet inspection, application inspection, SSL/SSH inspection
  - Many functionalities to protect the network from modern threats

## Zone-based Firewall
- If an organization cannot afford a hardware firewall, it can use an alternative
  - Implement the firewall features on router By using
    - CBAC (by maintaining access list)
    - Zone-based firewall (new approach than CBAC)
- Zone
  - Logical area in which the devices have the same trust levels
  - By default, traffic is not allowed from one zone to another
  - There are two zones: inside (private network) and outside (WAN connection)
- Zone pair
  - We can define zone pairs to allow traffic based on direction
    - Inside to outside
    - Outside to inside
    - Self zone (traffic within the zone)
