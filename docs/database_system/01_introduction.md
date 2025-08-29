# Introduction
- Data: Collection of units of information
- Database: Organized collection of data that can be easily managed
- Database Management System
  - Software system designed to enable users to store, organize & manage a database
  - Manages security and access control
  - Scalability: Handles large amounts of data

### Drawbacks of File System
- Redundancy: If some data needs to be updated, it takes a lot of effort
- Inconsistency
  - For the same information, there can be different data at different places
- Data access
  - To access a particular info, user should already know the file
    - The file that the info is stored in and its location
- Unauthorised access: Anyone can access and update the data in unauthorized way
- No backup & recovery

### Key features
- Data modeling: Data models define the structure & relationships of the data
- Data storage & retrieval: Create, modify, query data
- Concurrency control
  - Allow multiple users to access data without conflicting with each other
- Data integrity & security
  - Constraints on the values of data and access control to restrict users
- Backup & recorvery
- Multiple data views: Same data can be represented in different ways
- Analytics & reporting

## Types
- Relational DBMS: SQL
  - The data is organized in the form of tables, and tables in rows & columns
  - The data is related to each other through primary & foreign keys
- Non-Relational DBMS: NoSQL
  - The data is organized in the form of key-value pairs, documents, graphs, or columns
  - Designed to handle large scale, high performance scenarios

## Components
### Database Object
- Any defined object in database used to store, reference, hold or manipulate data
- Table: Basic unit of storage composed of rows & columns
- View: Logically represented subset of data from one or more tables
- Index: Improves performance of fetching data
- Sequence: Generates primary key values
- Synonym: Alternative name for an object

### Database Languages
- Data Definition Language (DDL)
  - Deals with schemas and descriptions about how the data should reside in the database
  - Create, Alter, Drop, Truncate (remove all records from table), Rename
- Data Manipulation Language (DML)
  - Used to store, modify, retrieve, delete and update data
  - Select, Insert, Update, Delete
- Data Control Lanuage (DCL)
  - Access specifier to grant and revoke permissions to users
  - Grant, Revoke
- Transaction Control Language (TCL)
  - Manager for all transactional data and transaction
  - Rollback, Commit, Savepoint (Save data temporarily)

## Three Layer Architecture
- Physical or Internal Layer
  - Keeps info about the location of database objects in data store
  - Describes how the data is being stored in secondary storage
- Conceptual or Logical Layer
  - Data is represented in the form of tables and relations
  - Describes what kind of data is to be stored (schema)
- External or View Layer
  - View of data in terms of conceptual level tables
  - Users can view data in form of rows & columns
  - Different views can be generated for different users

### Data Independence
- Change of data at one level should not affect another level
- Physical data independence
  - Change in physical location of tables & indexes
    - Should not affect conceptual or external level
  - The changes can be
    - Using new storage devices
    - Modifying data structures used for storage or altering indexes
    - Using alternative file organization techniques
- Conceptual data independence
  - Adding or deleting attributes in a table should not affect the user's view of table
  - Other changes can be altering table structures or relationships
  - Difficult to achieve compared to physical data independence

## Multimedia Database
- Stores documents, graphics, images, animations, video, audio, etc
- Types of media: Static media, dynamic media, dimensional media

### Contents
- Media data: Actual data representing an object
- Format data
  - Information about the format of media data
    - Like sampling rate, resolution, encoding scheme
  - After it goes through acquisition, processing & encoding phase
- Keyword data
  - Keyword description related to the generation of data like date, time, place
- Feature data
  - Content dependent data
  - Like distribution of colors, kinds of texture, different shapes present in data

### Types based on data management
- Repository applications
  - Data & metadata stored for retrieval purpose
    - Like format, date, keyword data, feature data
  - Examples
    - Repository of satellite images, engineering drawings, radiology scanned pictures
- Presentation applications
  - Delivery of multimedia data subject to temporal constraint
    - Optimal viewing or listening requires delivering data at certain rate
    - Data is processed as it is delivered
  - Offers quality of service above certain threshold
  - Example: Annotating video & audio data, real time editing analysis
- Colloborative applications
  - Executing complex task by merging drawings, changing notifications
  - Example: Intelligent healthcare network

### Challenges
- Modelling & design
  - There can be performance & tuning issues
    - In external, conceptual & physical design layers
  - Designing can be complex due to various formats like jpeg, gif, png, mpeg
  - These formats are not easy to convert from one form to another
- Storage
  - Challenge of representation, compression, archiving, buffering
    - And mapping device hierarchies
  - BLOB (Binary Large Object) facility allows untyped bitmaps to be stored and retrieved
- Performance
  - Physical limitations in video playback or audio-video synchronization
  - Parallel processing may alleviate some problems
    - But such techniques are not fully developed
  - Multimedia database consumes a lot of processing time and bandwidth
- Queries & retrieval
  - Accessing data for multimedia through query have many issues
  - Query formulation, query execution and optimization needs to be worked upon
