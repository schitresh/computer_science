## Multiple Access Control
- If there is no dedicated link between the sender and the receiver
  - Then multiple stations can access the channel simultaneously
  - Multiple access protocols are required to decrease collision and avoid crosstalk
- Types
  - Random access protocols
  - Controlled access protocols
  - Channelization protocols

## Random Access Protocols
- All stations have the same priority
- Any station can send data depending on the medium's state (idle or busy)
- There is no fixed time for sending data
- There is no fixed sequence of stations sending data

### Aloha
- Used in low traffic networks
- Pure Aloha
  - Station waits for an acknowledgement after sending data
  - If acknowledgement is not received within the alotted time
    - Then the station waits for a random amount of time (backoff time)
    - And then re-sends the data
  - The probability of collision decreases
    - Since different stations wait for different amount of time
- Slotted Aloha
  - Time is divided into slots
  - Sending data is allowed only at the beginning of these slots
  - If a station misses the allowed time
    - It must wait for the next slot
    - This reduces the probability of collision

### CSMA (Carrier Sense Multiple Access)
- The station senses the medium (for idle or busy) before transmitting data
- If it is busy, then it waits till the channel becomes idle
- Better efficiency than aloha, used in high traffic networks
- There is a chance of collision due to propogation delay

### CSMA/CD (Collision Detection)
- Once the station sends an entire frame, it does not keep a copy of the frame
  - And does not monitor the channel for collision detection
  - So before sending the last bit of the frame, the collision must be detected
- If a collision signal is received by the node, transmission is stopped
  - Resending the frame immediately after may lead to consequent collisions
  - So back-off algorithm is used
    - Where it waits for random time intervals before resending the frame
- The size of a frame must be large enough to detect the collision by the sender
  - Frame transmission delay must be at least two times the maximum propogation delay
  - T(t) >= 2 * T(p)
  - T(t) = S / B (S = Frame Size, B = Bandwidth or Transmission Speed)
  - T(p) = L / P (L = Distance between farthest nodes, P =  Propogation Speed)
  - From above equations, we can get the mimimum frame size (S) and the maximum cable length (L)

### CSMA/CA (Collision Avoidance)
- Interframe space
  - If the medium is idle, the station waits for a period of time (interframe space)
  - After that it checks for the medium status again
  - This avoids collision due to propogation delay
  - The interframe space depends on the priority of the station
- Contention window
  - Divides time into slots and chooses a random number of slots as wait time
  - The number of slots double every time medium is found busy
- Acknowledgement
  - The sender re-transmits the data if acknowledgement is not received before time-out

## Controlled Access Protocols
- The stations seek information from one another to find which station has the right to send
- Allows only one node to send at a time to avoid collision of messages on a shared medium

### Reservation
- Station needs to make a reservation before sending data
- The timeline has two kind of periods
  - Reservation interval of fixed time length
  - Data transmission period of variable frames
- If there are N stations, reservation interval is divided into N slots
  - Each station has one slot, no other station can transmit during this slot
  - i'th station announces that it has a frame to send by inserting 1 bit into the i'th slot
  - After all N slots have been checked, each station knows which stations wish to transmit
  - The stations which have reserved their slots transfer their frames in that order
- After data transmission period, next reservation interval begins

### Polling
- A controller sends a message to each node in turn
- One station acts as a primary station (or controller) and others as secondary stations
  - All data exchanges happen through the controller
  - The message sent by the controller
    - Contains the address of the node being selected for granting access
- All nodes receive the message
  - But only the addressed one responds and sends data if any
  - If there is no data, usually a 'poll reject' (NAK) message is sent back
- Problems
  - High overhead of the polling messages
  - High dependence on the controller
- Since every station has an equal chance in every round, link sharing is biased

### Token Passing
- The stations are connected logically to each other in form of ring or bus
- Access to stations is governed by tokens
  - A token is a special bit pattern or a small message
  - The token circulates from one station to the next in a predefined order
  - When a station gets the token
    - It sends the frame queued for transmission and passes the token
- Problems to tackle
  - Duplication or loss of token
  - Insertion or removal of a station

## Channelization Protocols
- The available bandwidth of the link is shared in time, frequency and code
  - To multiple stations to access a channel simultaneously
- This is done using circuit switching
  - This means dividing bandwidth into pieces by frequency or time

### Ways to share bandwidth
- Frequency Division Multiple Access
  - Bandwidth is divided into equal bands and each station is alloted its own band
  - Guard bands are added to avoid overlap, to avoid crosstalk and noise
- Time Division Multiple Access
  - To avoid collision, time is divided into slots and alloted to stations
  - There is an overhead of synchronization
    - Which is solved by adding synchronization bits to each slot
  - Propogation delay is resolved by adding guard bands
- Code Division Multiple Access
  - One channel carries all transmissions simultaneously, no division of bandwidth or time
  - Data from different stations are transmitted in different code languages
  - By recognizing the code language, the identity of the station is mapped
- Orthogonal Frequency Division Multiple Access
  - Bandwidth is divided into small subcarriers to increase the overall performance
  - Widely used in 5G technology
- Spatial Division Multiple Access
  - Uses multiple antennas at the transmitter and receiver
  - To separate the signals of multiple users located in different spatial directions
