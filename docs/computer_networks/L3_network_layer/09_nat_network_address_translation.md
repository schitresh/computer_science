## Network Address Translation (NAT)
- Allows multiple devices to access the internet through a single public address
  - Also masks the port number of the host with another port
  - Provides privacy to the local users
    - And rejects malicious packet not requested by anyone
- A network device (router or firewall) assigns a public address
  - To a computer (or group of computers) inside a private network
- The main use of NAT is to limit the number of public IP addresses
  - That an organization or company must use
  - For both economy and security purposes

## Working
- Generally, the border router is configured for NAT
  - Border router is the one that has one interface in the local (inside) network
  - And one interface in the global (outside) network
- When a packet traverse outside the local network
  - NAT converts the local (private) IP address to global (public) IP address
- When a packet enters the local network
  - Global IP address is converted to local IP address
- If NAT runs out of addresses in the configured pool, the packets are dropped
  - And ICMP sents unreachable packet to the destination

## Masking Port Numbers
- Let's say two hosts A and B are connected
- Both of them request for the same destination
  - On the same port number (say 1000) on the host side at the same time
  - On receiving a reply from the destination
    - It will be unclear to NAT which reply belongs to which host
- To avoid such a problem
  - NAT masks the source port number and makes an entry in the NAT table

## Types
- Static NAT
  - A single unregistered (private) IP address
    - Is mapped with a registered (public) IP address
  - Generally used for web hosting
  - Not used in organization as there are many devices that need internet access
- Dynamic NAT
  - An unregistered IP address is translated to a registered IP address
    - From a pool of public addresses
  - If no IP address of the pool is free, then the packet is dropped
  - Used when the number of users who want internet access is fixed
  - Not used in organization
    - As each user that wants to access internet needs to be assigned a global address
- Port Address Translation (PAT)
  - Also known as NAT overload
  - Many local IP addresses can be translated to a single registered IP address
  - Port numbers are used to distinguish the traffic
  - Most frequently used, cost effective
