## Threat Modeling
- Threat can be anything that can take advantage of a vulnerability to breach security
  - And negatively alter, erase, or harm objects of interest
- Threat modeling is used to identify, communicate, understand & mitigate threats
- Documentation from this process provides system analysts and defenders
  - With a complete analysis of probable attacker profiles, attack vectors, assets of interest

## Process
- Aim
  - Establish the aim for carrying this process
  - Pay attention to the CIA triad
- Visualization & Identification
  - Understand the flow of data
  - Find processes with user interactions
- Mitigation
  - Continuous investigation of each vulnerability
  - Action plan to deal with threats
- Validation
  - Check if the threats have been mitigated or not

## Methodologies
### STRIDE
- Spoofing: An adversary posing as another user or component existing in system
- Tampering: Modification of data within the system
- Repudiation: Ability of user to deny having performed a particular action
  - Can be done using false identity, manipulation of logs, deletion or evidence
- Information Disclosure: Exposure of protected data to non-allowed user
- Denial of Service
- Elevation of Privilege: Breaching administrative controls and tampering privileges

### DREAD
- Damage Potential
- Reproducibility: How easy it is to reproduce an attack
- Exploitability: Effort required to launch an attack
- Affected Users
- Discoverability: How easy it is to discover the threat

### Others
- PASTA (Process for Attack Simulation and Threat Analysis)
  - Dynamic threat identification, enumeration, scoring process
  - Develops an asset centric mitigation strategy by analyzing attacker centric view of system
- Trike: Establishes stakeholder defined acceptable level of risk assigned to each asset class
- Vast (Visual, Agile, and Simple Threat modeling)
  - Provides an application and infrastructure visualization schemme
- Attack Tree: Conceptual diagram about how an asset might be attacked
- CVSS (Common Vulnerability Scooring System)
  - Captures principal characteristics of a vulnerability with a numerical score
- T-Map: Calculates weights of attack paths
