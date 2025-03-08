## Mobile Communication
- SIM (Subscriber Identity Module) card
  - Stores subscriber's identification and account information
  - Stores security credentials that allow a device to connect to the network
- A SIM card plugged into a mobile device forms GSM system
  - GSM (Global System for Mobile Communication)
  - GSM system can be dissected into radio, network & operation subsystems

## Radio Subsystem
- Mobile communication occurs in the form of radio waves that travel through air
- Mobile station (MS)
  - Stores user specific data in SIM card
    - Serial number, card type, PIN, PIN unblocking key, authentication key
    - List of subscribed services
  - Stores dynamic data required for wireless communication
    - Location information, cipher key for encryption & decryption
- Base station system (BSS)
  - Maintains radio connection to the mobile station
  - Performs coding & decoding of the voice communication
  - This happens through radio equipment present on cell tower
    - Like antennas, amplifiers, signal processors
  - Designates radio frequencies for communication
    - And performs handover from one cell tower to another

### Network Subsystem
- Handles the handover from one BSS to another
  - Which enables national & internation roaming
- It is aware of the subscriber location via its databases
  - Home location register & visitor location register
- The movement of a mobile station is traced
  - And updated in the registers if it leaves the current location area

### Operation Subsystem
- Responsible for smooth operations of a network
- Traffic monitoring, subscriber management, security, accounting, billing
- This informatino is held in a consolidate database of existing mobile devices
  - This database is called equiment identity register
  - This database is updated to blacklist any stolen device
    - And block communication on the associated SIM
