# Recoverability and Processing
## Recoverability
- Data can be lost or transactions can fail due to
  - Transaction errors
    - Transaction irregularities or no longer acceptable
    - May be aborted due to serializability violation or deadlock
  - System error (logical programming errors)
  - Incorrect command execution, security breaches
  - System crashes, network failures, disk failures, data corruption, viruses
  - Catastrophic failures: fire, theft, overwriting by mistake
- Recovery techniques are heavily dependent upon a special file called system log
  - It contains info about start and end of each transaction
  - Keeps track of all operations that affect database values

## Logging
- Record all the activities and transactions in the database
- Fields
  - Transaction identifier
  - Data item
  - Old value
  - New value
- Log based on operations
  - T(i) start: Stores info when a transaction starts
  - T(i) commit: Stores info when a transaction commits
  - T(i) abort: Stores info when a transaction aborts

## Undo & Redo
- All modifications must precede by the creation of a log record
- The system should be able to
  - Undo the operation and set the data item to the old value
  - Redo the operation and set the data item to the new value
- Redo operations should be idempotent (give the same result when performed again)
  - Should not lead to creating duplicate entities
- After a system crash
  - Undo the transaction if T-start is present but not T-commit or T-abort
  - Redo the transaction if T-start and T-commit or T-abort is present

## Checkpoints
- Checkpoint logs keep track of the list of transactions active at the time of the checkpoint
- Any modifications by the transactions is written either prior or as part of the checkpoint
- After a crash, undo or redo needs to be applied only to the transactions in and after the checkpoint

## Modification Techniques
- Deferred Update
  - Transaction doesn't modify the database until partially committed
  - Undo is not needed since the transaction won't have changed anything
  - Redo maybe required for operations recorded in the local transaction workspace
- Immediate Update
  - Transaction can modify the database while still in execution
  - Both undo & redo are required
- Caching/Buffering
  - Disk pages that include data items that are to be updated are cached into main memory buffers
  - Then are updated in memory before being written back to disk
  - A collection of in-memory buffers called DBMS cache is kept under the control of DBMS
  - A directory is used to keep track of the database items that are in buffer
  - A dirty bit is associated with each buffer (1 if buffer is modified else 0)
- Shadow Paging
  - When a transaction begins executing, the current directory is copied into a shadow directory
  - When a page is to be modified, a shadow page is allocated in which changes are made
  - When it is ready to become durable
    - All pages that refer to the original are updated to refer new replacement page

## Backup Techniques
- Full Database Backup
- Differential Backup
  - Stores only the data changes that have occurred since the last full database backup
  - For this, first a full database backup needs to be restored
- Transaction Log Backup
  - Through this, the database can be recovered to a specific point in time

## OLAP (Online Analytical Processing)
- OLAP systems can analyze database information of multiple systems at the current time
- The primary goal is data analysis and not data processing
- Online query management system that consists of historical data
- Any type of data warehouse system is an OLAP system
- Tables are not normalized
- Relatively slow due to large amount of data
- Applications
  - Used for data mining, analytics, decision making, big data
  - Spotify analyzing songs to come up with personalized homepage and playlists
  - Movie recommendation system in netflix
- Benefits
  - Store planning, analysis, budgeting for business analytics within one platform
  - Helps in handling large volumes of data
    - Which helps in enterprise-level business applications
  - Helps in applying security restrictions for data protection
  - Provides multi-dimensional view of data
- Challenges
  - Requires professionals to handle data due to complex modeling procedure
  - Expensive to implement and maintain for large datasets
  - Requires extraction and transformation of data for analysis which delays the system
  - Updated on periodic basis and not real time

### Types of OLAP Servers
- Relational
  - Data is stored in relational database
  - Based on the premise that
    - Data need not be stored multi-dimensionally to be viewed multi-dimensionally
- Multidimensional
  - Data is stored on disks in a specialized multi-dimensional array structure
  - Has advanced indexing and hashing to locate data and handle sparse arrays
  - Fast data retrieval, optimal for slicing & dicing, perform complex calculations
- Hybrid of Relational & Multi-dimensional
- Transparent: Work with existing RDBMS without transfering data to a separate OLAP system

## OLTP (Online Transaction Processing)
- OLTP systems administer day to day transactions in any organization
- The primary goal is data processing and not data analysis
- Online data modifying system that consists of operational current data
- Handles ACID properties during data transactions
- Tables are normalized
- Fast as the queries operate on 5% of data
- Example: ATM center, sending text message, online banking & ticket booking & shopping
- Benefits
  - Allows users to read, write and delete data operations quickly
  - Helps in increasing users & transactions which helps in real-time access to data
  - Helps in applying multiple security features
  - Helps in making better decisions by providing accurate data or current data
  - Provides data integrity, consistency, and high availability to data
- Challenges
  - Limited analysis and reporting capability
  - High maintenance costs because of frequent maintenance, backups & recovery
  - Some issues like duplicate or inconsistent data can occur
