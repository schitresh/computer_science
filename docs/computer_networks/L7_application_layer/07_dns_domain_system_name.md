# Domain Name System (DNS)
- Distributed database implemented in a heirarchy of name servers
- Every host is identified by its IP address
  - But managing numbers is very difficult since there are millions of websites
  - Also IP addreesses are not static, they can change
  - So domain names are used instead and are converted to their IP address by DNS
- Uses UDP because
  - UDP is much faster than TCP which uses 3 way handshake end-to-end connection
  - DNS servers don't have to keep connections
  - DNS requests are generally very small and fit well within UDP segments
  - Reliability can be increased at application layer by using timeout & resend

## DNS Lookup
- Client sends a request to a DNS resolver to resolve a domain name
- If not found, it can
  - Send request to other or high level servers (recursive lookup)
  - Or it can refer the resolver to other servers (iterative lookup)
- This process keeps repeating at each level till the DNS is resolved
  - Once found, the results are cached based on the frequency or other factors
- Servers in order of lookup
  - Local name server
  - Root name server
  - Top level domain (TLD)
    - Manages entries for domains like com, org, edu, uk, fr, ca, in
  - Authoritative name server: Maintained by organization or service provider
