# SMTP (Simple Mail Transfer Protocol)
- SMTP is a push protocol used to send emails
- POP/IMAP are used to retrieve emails
  - POP (Post Office Protocol)
  - IMAP (Internet Message Access Protocol)
- Types
  - End-to-end: Used to communicate between different organizations
  - Store-and-forward: Used within an organization

## Working
- Sender opens a TCP connection to the SMTP server
- SMTP server is always on listening mode, it listens & establishes the TCP connection
- Sender sends the mail over the connection
- SMTP server keeps the mail to itself until it is successfully delivered

## Components
- Sender's user agent prepares a message and sends it to the Mail Transfer Agent (MTA)
- MTA maintains a small queue
  - To schedule repeat delivery of mail in case receiver is not available
- MTA transfers the mail across the network to the receiver's MTA
- The user agent on the server side checks the mailboxes at regular intervals
- If any information is received, it informs the user about the mail

## MIME (Multipurpose Internet Mail Extension)
- Supplementary protocol that allows non-ASCII data to be sent through SMTP
  - Allows users to exchange data like audio, video, images, application programs
  - Enables to use HTML and CSS in emails to customize and beautify them
  - Allows using different languages like Hindi, French, Japanese, etc
- Working
  - SMTP has a simple structure and sends message only in NVT 7-bit ASCII format
  - MIME transforms non-ASCII data to NVT 7-bit ASCII data at the sender side
  - And delivers to the client SMTP where the inversion happens
  - MIME header is added to the email to define transformation and content info
