# Introduction
## System Security
- Security can be compromised via any of these breaches
  - Breach of confidentiality: Unauthorized reading of data
  - Breach of integrity: Uauthorized modification of data
  - Break of availability: Unauthorized destruction of data
  - Theft of service: Unauthorized use of resources
  - Denial of service: Preventing legitimate use of system
- The security of a system can be threatened via two violations
  - Threat: A program that has the potential to cause serious damage to the system
    - Program Threats
      - A program is written to hijack the security or change the behavior
      - A user program is altered and make to perform malicious unwanted tasks
      - Examples: Virus, worm, trojan horse, trap door, logic bomb
    - Security Threats
      - System services, resources or user files are misused
      - Also used as medium to launch program threats
      - Examples: Worm, port scanning, denial of service
  - Attack: An attempt to break security and make unauthorized use of an asset

## CIA Triad
### Confidentiality
- Only authorized individuals or systems
  - Should be permitted to view sensitive or classified information
- A primary way to safegaurd data is to use encryption techniques
  - AES (Advanced Encryption Standard)
  - DES (Data Encryption Standard)
- Another way to protect data is through VPN (Virtual Private Network) tunnel

### Integrity
- The system should make sure that data has not been modified
  - Corruption of data is a failure to maintain data integrity
- To check this, a hash value is generated using hash functions like
  - SHA (Secure Hash Algorithm): 160-bit hash in SHA-1
  - MD5 (Message Direct 5): 128-bit hash
- This hash value is attached to the data
  - When the target host receives the packet, it runs the same function
    - And checks if the generated hash matches the received hash

### Availability
- Network (systems, data) should be readily available to its users
  - Or else it may impact the business
- Network administrator should maintain hardware and make regular upgrades
  - Should have a plan for fail-over and prevent bottlenecks
- Attacks like DoS or DDoS may render a network unavailable
  - As the network resources get exhausted
