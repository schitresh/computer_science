# File Transfer Protocol
- Moves files between local and remote file systems
- Shields users from system differences like OS, directory structure, character sets
- Can transfer these categories of data
  - ASCII & EBCDIC
  - Image
    - File has no formal internal structure
    - Transferred one byte at a time without any processing
  - Local: File containing data in logical bytes

## Working
- Two TCP connections are used in parallel
- It sends control info in separate connection, so it's called out-of-band
  - Protocols like HTTP & SMTP that send it in same connection are called in-band

### Control connection
- Initiated by client to send info like user identification, password
  - Commands to change the remote directory
  - Commands to retrieve & store files
- Initiated on port number 21
- Persistent & stateful connection
  - Remains active throughout the session to maintain a state about user

### Data connection
- Initiated by server after control info has been sent by client
- To send the actual file
- Initiated on port number 20
- Non persistent & stateless connection
