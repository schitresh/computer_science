## Internet Protocol version 6 (IPv6)
- Developed to deal with the problem of IPv4 exhaustion
  - Address depletion as the need for electronic devices rose quickly
    - When internet of things (IOT) came into picture
- 128-bits address having address space of 2^128 which is way bigger than IPv4
  - Uses hexadecimal format separated by colon
  - Components in address
    - 8 groups, each group represents 2 bytes
    - Each hexdigit is of 4 bits
- Better header format
  - Options are separated from the base header
    - And inserted when needed between the base header & upper layer data
  - Simplifies and speeds up the routing process
    - Because most of the options don't need to be checked by routers
- Allows new options for additional functionalities
  - And extension of protocol for new technologies
- Provides better security, priortization, real-time communication, mobile device support

## Addressing Methods
- Unicast Address
  - Identifies a single network interface
- Multicast Address
  - Used by multiple hosts which need not be geographically together
  - Broadcast address was removed due to performance reasons
    - Though it can be achieved using multicasts
- Anycast Addresss
  - Assigned to a group of interfaces
  - Any packet sent is delivered to only one member interface
    - Mostly the nearest host

## Unicast Addresses
- Provider based: Used for global communication, contains provider id & subscriber id
- Geography based: Based on location, contains details like lat & long
- Local
  - Link local: Used for addressing a single link
  - Site local: Equivalent to a private IP address in IPv4
