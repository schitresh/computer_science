## SSH (Secure Shell)
- Cryptographic network protocol used to transfer encrypted data over a network
  - Allows you to connect to a server without having to enter password for each system
  - The port number of SSH is 22
- Features: Encryption, authentication, tunneling
- Comes in key pairs
  - Public key: For encryption function, everyone can see it, no need to protect
  - Private key: For decryption function, stays in computer, must be protected
- Types of key pairs
  - User key: If public & private key remain with the user
  - Host key: If public & private key are on a remote system
  - Sesson key: Used when a large amount of data is to be transmitted

## Working
- Public keys from the local system are passed to the server
- The server identifies if the public key is registered
  - If so, the server creates a new secret key
  - And encrypts it with the public key
  - The encrypted code is sent to the local system
- The data is unlocked by the private key of the system
  - And is sent to the server
  - The server after receiving this data verifies the local system
- SSH creates a route
  - And all the encrypted data are transferred through it with no security issue
