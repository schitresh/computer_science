## AAA
- AAA is a standard framework used to control
  - Who is permitted to use network resoures (authentication)
  - What they are authorized to do (authorization)
  - Capture the actions performed while accessing the network (accounting)
- An administrator can access a router or a device through a console
  - But it is incovenient if he is sitting far from the place of that device
  - So he has to take remote access to that device
- As remote access will be available by using an IP address
  - It is possible that an unauthorized user can take access using that IP address
  - So for security measures, we have to put authentication
  - Also, the packets exchanged between the device should be encrypted
    - So that any other person cannot capture sensitive info

### Authentication
- Identifying if a user that wants to access the network resources is valid or not
- Common methods are to put authentication on console port, AUX port, or VTY lines

### Authorization
- Enforces policies on network resources
  - After user has gained access to the network resources through authentication
- Determines what resources is the user allowed to access
  - And the operations that can be performed
- For example, junior engineer and senior engineer will have different permissions

### Accounting
- Monitoring and capturing events peformed by a user while accessing network resources
- Monitors how long the user has access to the network
- Administrator can create an accounting method list
  - To specify what should be accounted for
  - To whom the accounting records should be sent

## Implementation
- AAA can be implemented by using the local database of router or by using external ACS server
- Local database of the device (router)
  - First users are created for authentication
  - Then priviledge levels are provided to users for authorization
- Sending authentication requests to an external server like ACS server
  - Configuration on both router and ACS is required
    - If ACS server fails to authenticate, local database can be used as a backup
  - Configuration includes creating user
    - Separate customized method list for authentication, autorization, accounting
  - Client or Network Access Server (NAS) sends authentication requests to ACS server
    - Server takes the decision to allow the user to access the network resource or not
    - According to the credentials provided by the user

## Challenge Response Authentication Mechanism (CRAM)
- Used to authenticate actions
- One side presents a challenge
  - And the other side must present a correct answer to get authenticated
- Types of challenges
  - Static
    - User can select his challenge and authenticate himself
    - For example, security questions
      - That you select while account setup and asked in forget password
  - Dynamic
    - Challenges are selected randomly presuming that the user will know the valid answer

### Implementation
- CAPTCHA
  - Completely automated public turing test to tell computers and humans apart
  - Used to prevent spam and auto-registratoin of new accounts
  - Machine learning is used to train different types of models
  - Examples
    - User needs to enter a text or number from the distorted image
    - Images are presented and user needs to select the right pieces based on a prompt
- SSH (Secure Shell)
  - Cyptographic network protocol
  - For operating network services securely over an unsecured network
- Password
  - Password is sent to the server for validation by matching with the correct password
- Salted CRAM
  - Challenge is salted with a hash to make sure the password is used one time only
  - Hash is sent to server for matching with the hash of the correct password
  - So the password is not revealed to man in the middle attack and replay attacks
- Biometrics
