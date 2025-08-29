## HTTP (HyperText Transfer Protocol)
- Communication protocol used to deliver data between a client and a server
  - Data such as text, images, and other multimedia files are shared on WWW
  - Uses hypertext pages that can be interlinked with each other to form web pages
    - HTML is used to generate these pages
    - HTTP protocol transfers the hypertext pages from web server to web browser
- Methods HTTP/1.1: GET, POST, HEAD, PUT, DELETE
- Status Code:
  - 200: OK
  - 301: Moved Permanently
  - 400: Bad Request
  - 404: Not Found
  - 505: HTTP version not supported

### Details
- Connectionless protocol
  - After the connection is closed
    - The client and the server don't remember anything about each other
- Stateless protocol
  - Server maintains no information about past client requests
  - Each transaction on the protocol is carried out independently of the others
    - Without reference to the history
  - After the transaction is finished
    - The connection between the browser and the server ends
- Client-server model that uses TCP
  - Client initiates TCP connection (creates socket) to server, port 80
  - Server accepts connection, notifying client
  - HTTP messages are exchanged between browser (client) and web server

## HTTPS (HTTP Secure)
- Combination of HTTP with SSL/TLS convention to supply encrypted communication
  - And secure distinguishing proof of an arranged web server
- Encrypts all message substance including HTTP headers and the request/reponse data
- Requires a trusted third party to sign server side digital certificate

## Types
### Non-persistent
- Each object requires a new TCP connection for transmission
- With parallel connection for multiple objects
  - Requires extra overhead to transfer data
- Without parallel connection
  - Requires 2 RTTs (Round Trip Time) per object
  - Response time per object = 1 RTT for connection + 1 RTT for file transmission
- Connection is opened & closed each time
  - Which is more secure & does not waste resources
  - But results in an extra overhead and slow speed

### Persistent
- Multiple objects over one TCP connection
- After a connection is established that takes 1 RTT
  - Multiple objects can be sent over the same network that takes 1 RTT
  - Response time per object = 1 RTT (File transmission time)
- Types
  - Non-pipelined: Another request can be sent only if previous request is acked
  - Pipelined: Another request can be sent even if previous request is not acked
- Connection remains open
  - Which is less secure & wastes network resources
  - But removes the extra overhead of connection establishment and is fast

## Cookies
- Since HTTP is stateless protocol
  - Cookies help to keep state & give customized experience to user
- Uses: authorization, shopping carts, recommendations, user session state
- Servers can take swift action using cookies even one week later

## Conditional Requests
- Similar to the standard HTTP requests
  - But are only fulfilled by the server if the specified validators pass
- Useful to validate content of a cache, verify integrity of a document
