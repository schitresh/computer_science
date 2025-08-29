## Aysnchronous Transfer Mode (ATM)
- Telecommunications standard for digital transmission of multiple types of traffic
  - Can handle both
    - Traditional high throughput data
    - And real-time low latency content
  - Can handle both constant and variable rate traffic
  - Transmits all information over connection-oriented network
    - Including data, video, voice
- Was developed to meet the needs of Broadband ISDN
  - And is a core protocol used in SONET

## Details
- Uses small fixed-size packets called cells which are transmitted asynchonously
  - In contrast, IP packets are of variable size
  - Independent of transmission medium
  - Uses virtual circuit switching (path is reserved before transmission)
- Working
  - Uses Virtual path connections (VPC)
    - That consist of virtual channel connections (VCC) bundled together
  - VCC is a basic unit carrying a single stream of cells from user to user
- Making an ATM call
  - First sends a message to set up a connection
  - Subsequently, all cells follow the same path to the destination
- Addressing
  - 20-byte global NSAP (Network Service Access Point) address for signaling
  - 32-bit locally assigned labels in cells

## Layers
- ATM Adaption Layer (AAL)
  - Isolates higher layer protocols from details of ATM processes
  - Prepares for conversion of user data into cells
- Physical Layer
  - Controls transmission and receipt of bits in physical medium
  - Converts cells to bitstream and tracks ATM cell boundaries
- ATM Layer
  - Handles transmission, switching, congestion control
    - Cell header processing, sequential delivery
  - Cell multiplexing: Simultaneous sharing of virtual circuits over physical link
  - Call relay
    - Passing cells through an ATM network
    - Making use of VPI & VCI info in cell header
