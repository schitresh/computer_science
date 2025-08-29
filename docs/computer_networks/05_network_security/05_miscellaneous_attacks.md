# Miscellaneous Attacks
## Spoofing & Phishing
- IP Spoofing
  - Injects packet into the interrnet with a false source address
  - Can be solved using end-point authentication
- DNS spoofing or DNS cache poisoning
  - Corrupt DNS data is introduced into a DNS resolver's cache
    - Causing the name server to return an incorrect IP address
- Phishing
  - Sending emails purporting to be from reputable companies
  - In order to induce individuals to reveal personal information & sensitive data
  - When done through phone calls, it's called vishing (voice phishing)
- Packet Sniffer
  - A passive receiver that records a copy of every packet that flies by
  - Placed in the vicinity of a wireless transmitter
  - Some of the best defenses involve cryptography

## Hacking Attacks
- Man in the Middle attack
  - Someone between the source & destination
    - Actively monitors, captures and controls the communication transparently
  - For example, re-route a data exchange
  - When communicating at low levels of network layer
    - Computers might not be able to determine with whom they are exchanging data
- Compromized Key attacks
  - A key is a secret code or number necessary to interpret secured information
  - Obtaining a key is difficult and resource intensive process for an attacker
  - But it is possible and referred as compromised key when obtained

## Vulnerability Attacks
- Trap Door
  - The designer of a program or system might leave a hole that only he is capable of using
  - Quite difficult to detect as one needs to go through the source code of all the components
- Port Scanning
  - Automated process that creates a TCP/IP connection to a specific port
  - To protect the identity of attacker, they are launched from zombie systems

## Brute Force Attacks
- Birthday Attack
  - Type of cryptographic attack that belongs to a class of brute force attacks
  - Exploits the mathematics behind the birthday problem in probability theory
  - Success of this attack largely depends upon likelihood of collisions
    - Found between random attack attempts and a fixed degree of permutations
  - Birthday paradox problem
    - Let's say there is a classroom of 30 students and a teacher
    - The teacher wants to find pairs of students that have the same birthday
    - For a particular date, probability of at least one student born is
      - 1 - (364 / 365)^n = 7.9% for n = 30
    - Probability that at least one student has the same birthday as any other is
      - 1 - (365! / ((365 - n!) * 365^n)) = 70% for n = 30
