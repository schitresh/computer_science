## WiFi (Wireless Fidelity)
- Wireless networking technique that functions similar to a local area network
  - Routers and radio frequency waves are used to transmit data
- Can be less expensive and easier to install than wires & cables
  - It might be challenging to provide reliable coverage
    - In some areas where signal can become weak
- Enables a large number of users to connect to internet
  - At public places or organizations
  - Allows mobile devices to connect to internet

## Security Protocols
### WEP (Wired Equivalent Privacy)
- 64-bit or 128-bit encryption key
  - That must be manually entered on wireless access points & devices
  - Once configured can never be changed
- Uses cyclic redundancy check (CRC)
- Security flaws
  - Does not provide a sufficiently strong data integrity guarantee for the packets
  - Message authentication codes are used to solve this issue
    - But requires too much computation to be used on old network cards

### WPA (Wifi Protected Access)
- Intermediate measure in anticipation of the availability of the more secure & complex WPA2
- Employs per-packet key dynamically generating a new 128-bit key for each packet
  - Prevents the types of attacks that compromise WEP
- Includes a message integrity check called TKIP (Temporal Key Integrity Protocol)
  - To prevent attackers from altering or resending data packets
  - Much stronger than CRC used in WEP
- Security flaws
  - Limitations of the message integrity code hash function
    - That is used to retrieve the keystream from short packets
  - Can be used for re-injection and spoofing

### WPA2 (Wifi Protected Access 2)
- Includes mandatory support for
  - CCMP (Counter Mode CBC-MAC Protocol)
    - Block chaining message authentication code protocol
    - More robust and dependable than TKIP
  - AES (Advanced Encryption Standard) based encryption mode
- Mandatory for all new devices to bear the Wifi trademark
- Security flaws
  - Risk of unwanted access to the company wireless network
  - Occurs when an attack vector on specific WPS access points is compromised

### WPA3 (Wifi Protected Access 3)
- 192-bit cryptographic strength
- 384-bit Hash Message Authentication Mode (HMAC)
- 256-bit Broadcat/Multicast Integrity Protocol (BIP-GMAC-256)
- 256-bit Galois/Counter Model Protocol encryption (GCMP-256)
- SAE exchange
- Wifi Device Provisioning Protocol (DPP)

## WPS (Wifi Protected Setup)
- A wireless network security standard that tries to make connections
  - Between a router and wireless devices in a faster & easier way
  - Works only for wireless networks that use password protection using WPA or WPA2
- In a standard setup, you can't connect a wireless device to a wireless network
  - Until you know the network name called Service Set Identifier (SSID)
  - And its password called WPA-PSK (Pre-Shared Key)
- WPS can simplify this connection process
  - Push button
    - Press the WPS button located on the router and client devices
    - The device connects automatically without password once the buttons are enabled
  - PIN: Client device must enter the PIN found on the sticker for the access point
  - Network Field Communication: Client device must be brought close to the access point
- Relatively new technology, so not all devices support it
