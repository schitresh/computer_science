# Message Authentication Codes (MAC)
- Also known as error detection code or cyptographic checksum
- Let's say user A wants to send a message to user B
  - A encrypts and sends the message using shared-cryptosystem
  - A sends the key to B using public-key cryptosystem
  - B uses the key to decrypt to ciphertext and obtains the message
- What if a malicious user falsifies the ciphertext during the transmission
  - Or the message alters due to external problems like noise
  - When B decrypts the message, it will get the wrong message
  - B has to check whether the ciphertext is falsified or not
    - By using message authentication code
    - Ciphertext + Key = Message Authentication Code

## HMAC (Hashed MAC)
- Involves a cryptographic hash function and a secret cryptographic key
  - For example, SHA-256 or MD-5
- Uses two passes of hash computation
  - First pass produces an internal hash from the message and the inner key
  - Second pass produces the final HMAC code from the internal hash and the outer key
- Message (encrypted or not) is sent along with the HMAC hash
  - Parties with the secret key will hash the message again
  - If it is authentic, the received and computed hashes will match

## RSA Algorithm
- RSA is the acronym for the names of the developers
- Asymmetric cryptography algorithm
  - Means that it works on two different keys: public key & private key
  - Considered very secure and widely used
- Working
  - A client sends its public key to the server and requests some data
  - The server encrypts the data using the client's public key and sends to client
  - The client receives this data and decrypts it using private key
- Concept
  - It is difficult to factorize a large integer
  - Public key consists of multiplication of two large prime numbers
  - Private key is also derived from the same two prime numbers
    - If somebody can factorize the large number, private key is compromised
  - Hence, encryption strength lies on the key size
    - Key size is typically 1024 or 2048 bits
    - Due to this, it is slower than other encryption algorithms
