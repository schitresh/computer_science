## Packet Types
- There are two types of packets used in the network layer
- Data packets
  - Used to transfer user data
  - Supported by routed protocols like IP
- Route update packets
  - Used to update info about networks connected to all the routers
    - To neighbouring routers
  - Supported by routing protocols
    - Like RIP (Routing Information Protocol), OSPF (Open Shortest Path First)

## Routing Protocols
- Help routers determine the best path for data to reach its destination
  - Based on factors like network congestion, network latency, network distance
  - Can detect failures and redirect traffic to alternative paths
- Allow networks to grow & change dyanmically
  - Without any manual reconfiguration of individual routers
- A routing table is created which contains information about the routes

## Types
- Static or Non-adaptive
  - Routes are manuallly configured
  - And they are not dynamically updated based on network changes
  - Best suited for small networks where topology does not change
- Dynamic or Adaptive
  - Routes are automatically updated based on network changes
    - Topology, load, delay, distance, number of hops, estimated transit time
  - When a router finds a change in topology, it advertises to all other routers
  - Best suited for large & complex networks where topology changes frequently
- Default
  - Router is configured to send all packets toward a single router (next hop)
  - It is forwared to the default router
    - Irrespective of which network the packet belongs
- Heirarchical
  - Network is divided into multiple levels or domains
    - With each level having its own routing protocol
  - Best suited for large & complex networks
    - That needs to be divided into manageable sections

## Dynamic Routing Protocols
### Distance Vector Routing Protocol
- Selects the best path on the basis of hop counts to reach the destination network
  - Each router computes distance of its immediate neighbours
  - Router shares knowledge about whole network to its neighbours
- Updates (routing info) is not broadcasted
  - But shared to neighbouring nodes periodically
  - A router shares its knowledge about the whole network (full routing tables)
  - This is called routing on rumours
- Works on bellman ford algorithm
  - Each router maintains a distance vector table
    - Containing its distance from all possible destination nodes
- Characteristics
  - Based on: Local knowledge
  - Bandwidth required: Less (local sharing, small packets, no flooding)
  - Information sharing: Regular intervals
  - Algorithm to make routing table: Bellman-ford
  - Traffic: Less
  - Convergence: Slow
  - Problems: Count to infinity, Slow convergence, Persistent loops

#### Routing Loops
- Routing loops is the main issue since bellman ford algorithm cannot prevent loops
- Usually occur when an interface goes down or two routers send updates at the same time
- Routing loops cause count to infinity problem
  - Wrong information keeps propogating within each other toward infinity
  - Let's say AB = 1 & BC = 1, so AC = 2
    - If B & C are disconnected, B will remove C from its table
    - Meanwhile, if A advertises that AC = 2, then B updates BC = 3 since AB = 1
    - A then receive update from B that BC = 3 and it updates AC = 4 since AB = 1
  - Spreading the bad information is called route poisoning
- Solutions: Poison reverse, Split horizon
- Examples: RIP (Routing Information Protocol)

### Link State Routing Protocol
- Knows more about internetwork than distance vectors
  - Each router has node map and calculates best path
  - Router shares knowledge of its neighbours with all the routers
  - Maintains neighbor table, topology table, routing table
- Knowledge about the neighborhood
  - Instead of sending routing table, a router sends info about its neighborhood only
  - A router broadcasts its identities and cost of directly attached links
  - Hello messages or keep alive messages are used for neighbor discovery & recovery
- Flooding
  - In flooding, each router sends info
    - To every other router on the internetwork except its neighbors
  - Every router that receives tht packet sends the copies to all the neighbors
- Information Sharing
  - Router sends information only when a change occurs in the information
  - Only the updates requested by the neighbor router are exchanged
- Initially each node knows the cost of its neighbors
  - And finally each node knows the entire graph
  - Dijkstra's algorithm is used to calculate optimal routes
- Characteristics
  - Based on: Global knowledge
  - Bandwidth required: More (large packets, flooding)
  - Information sharing: Whenever there is a change
  - Algorithm to make routing table: Dijkstra
  - Traffic: More
  - Convergence: Fast
  - Problems: Heavy traffic due to packet flooding
- Examples: OSPF (Open Shortest Path First)

### Advanced Distance Vector Routing Protocol
- Hybrid of distance vector & link state routing protocols
- Examples: EIGRP (Enhanced Interior Gateway Routing Protocol)

## Redistribution
- Using a single routing protocol in an organization is preferred
- But under some conditions, we have to use multiple protocols
  - Like company mergers, multi-vendor devices
- Advertising a route learned through a routing protocol
  - Into another routing protocol is called redistribution
- We have to define metric of the routing protocol in the advertising routing protocol
  - For example, to advertise EIGRP into RIP, we have to define hop count (metric of RIP)
