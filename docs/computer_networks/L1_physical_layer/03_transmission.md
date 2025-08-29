# Transmission
## Modes
### Simplex
- Unidirectional communication
- Only one of the devices on the link can transmit, the other can only receive
- Useful where feedback or response is not required, like broadcasting or surveillance
- Examples: radio, monitor, keyboard

### Half-duplex
- Each station can transmit and receive, but one at a time
- When one device is sending, the other can only receive
- Examples: walkie-talkie

### Full-duplex
- Both stations can transmit and receive simultaneously
- Signals in both the directions share the capacity of the link with each other
  - Either the link must contain two physically separated transmission path
    - One for sending & the other for receiving
  - Or the capacity must be divided between signals travelling in both the directions
- Requires a high level of bandwidth
- May not be suitable for all types of applications
- Examples: phone, video conferencing, online gaming

## Transmission Types
- Unicast
  - Message is sent from one sender to one receiver
  - Examples: email, file transfer
- Broadcast
  - Message is sent from one sender to all receivers
  - Examples: DHCP requests, ARP (Address Resolution Protocol) requests
- Multicast
  - Message is sent from one sender to a group of receivers
  - Examples: video streaming, online gaming

## Transmission Media
- The channel through which data is sent from the transmitter to the receiver
- Guided Media
  - Wired or bounded media
  - High speed & secure
- Unguided Media
  - Wireless or unbounded media
  - Less secure, transmitted through electromagnetic signal

## Guided Media
### Twisted Pair Cable
- Consists of two separately insulated conductor wires wound about each other
  - Several such pairs are bundled together in a protective sheath
- Unshielded Twisted Pair
  - Consists of two insulated copper wires twisted around one another
  - Block interferences without depending on a physical shield
  - Used for telephone connections and LAN networks
- Shielded Twisted Pair
  - Consists of a special jacket to block external interference
    - Copper braid covering or foil shield
  - Better performance at higher data rate than unshielded one
    - But more expensive & difficult to install
  - Used in fast-data-rate ethernet and in voice & data channels of telephone lines

### Coaxial Cable
- Has two parallel co-axial conductors each having a separate insulated cover
- Transmits information in two modes
  - Baseband mode: Dedicated cable bandwidth
  - Broadband mode: Cable bandwidth split into separate ranges
- Widely used by cable TVs and analog television networks

### Optical Fiber Cable
- Uses refraction of light through a core made up of glass or plastic
- Used for transmission of large volumes of data
- Supports unidirectional and bidirectional modes

### Stripline
- Transverse electromagnetic transmission line
- Uses a conducting material to transmit high frequency waves
- Conducting material is sandwiched between two layers of the ground plane
  - Which are usually shorted to provide EMI immunity
- Microstripline
  - Conducting material is separated from the ground plane by a layer of dielectric

## Unguided Media
- Radiowaves
  - Easy to generate and can penetrate through buildings
  - Sending and receiving antennas need not be aligned
  - Frequency range: 3KHz to 1GHz
  - Used by AM & FM radios, cordless phones
- Microwaves
  - Sending & receiving antennas need to be properly aligned
  - Frequency range: 1GHz to 300 GHz
  - Majorly used for mobile phone communication and television distribution
- Infrared
  - Used for very short distance communication
  - Can penetrate through obstacles and prevents interference between systems
  - Frequency range: 300GHz - 400THz
  - Used in TV remotes, wireless mouse & keyboard
