# Indexing
- Data structure technique to quickly locate and access data
- Minimizes disk accesses required for a query
- An index entry consists of the search key with value as the data reference
- Complex columns should not be indexed, it might decrease the performance instead
- Columns with large datasets but small classification should not be indexed
  - For example, boolean columns since there will be large data for a single key
  - Indexing 10K rows into true & false can deplete performance

## Indexing Mechanisms
- File organization mechanisms followed by indexing methods to store data

### Sequential File Organization (Or Ordered Index File)
- Dense index
  - For every search key in the data file, there is an index record
  - The record contains the search key and the reference to the first data record
- Sparse index
  - The index record is present for only a few items in the data file
  - The reference in each record points to a block
  - To locate a record
    - We find the record with the largest search-key value less than or equal to the target
  - After jumping to the reference pointer
    - The file is searched sequentially for the target record
  - Number of accesses required = log(n) + 1, where n is the number of blocks

### Hash File Organization
- Indices are based on the values distributed uniformly across a range of buckets
- A hash function determines the bucket to which a value is assigned
- Clustered or Primary Index
  - Similar records are grouped and indexes are created for these groups
  - In some cases, index is created on non-primary key columns which may not be unique
    - In such cases, two or more columns are grouped to get unique values
- Non-clustered or Secondary Index
  - Nested index through virtual pointers
  - Data is not physically stored in the order of the index
  - Data is present in the leaf nodes
  - Requires more time than clustered index to extract the data by following pointers
- Multilevel Index
  - As database size grows, indices also grow
  - As the index is stored in main memory, a single level index might become too large
  - It segregates the main block into various smaller blocks
    - Which ultimately point to the data blocks
  - B and B+ trees

## B-Tree
- For storing and searching large amounts of data
  - Traditional binary search trees can become impractical
  - Due to their poor performance and high memory usage
- Balanced Tree (B-Tree) is a type of self-balancing tree
  - It maintains balance by ensuring that each node has a minimum number of keys
  - This balance guarantees the time complexity of O(log(n))
    - Regardless of the initial shape of the tree
  - This is true for operations like insertion, deletion, and searching
- Can store a large number of keys in a single node
  - This allows the tree to have a larger branching factor and shallower height
  - This shallow height leads to less disk I/O and faster search & insertion
  - Node size is kept equal to disk block
- It's particularly well suited for storage systems with slow & bulky data access
  - Like hard drives, flash memory
  - When number of keys is high, data is read from disk in form of blocks
- Example:
  -                               (100)
  -          (35, 65)                              (130, 180)
  - (10, 20) (40, 50) (70, 80, 90)      (110, 120) (140, 160) (190, 240, 260)

### Properties
- All leaves are at the same level
- It's defined by the term minimum degree 't', which depends on disk block size
- All keys of a node are sorted in ascending order
- Number of keys in nodes
  - Root: (1) to (2t - 1)
  - Others: (t - 1) to (2t - 1)
  - Number of children: Number of keys + 1
- Child between two keys k1 & k2 contains all keys from k1 to k2
- Grows and shrinks from root unlike BST
  - BSTs grow downward & also shrink from downward
- Time Complexity for insert, delete, search = O(height) = O(log(n))
- Insertion only happens at leaf node

### Insertion
- Start from the root and traverse down till we reach a leaf node
- While traversing, keeping check if the next node has space
- If there's no space
  - Split the leaf node into two and separate the mid
  - Move the mid to the parent node (That's why B-tree grows up)
  - Repeat this process for every iteration if there's no space
- Add the key in the leaf node
- Example:
  - We need to insert 52 and we have: (40, 60) -> (45, 50, 55)
  - Shift 50 to parent & insert 52: (40, 50, 60) -> (45, 52, 55)

### Deletion
- Deletion is more complicated than insertion because a key can be deleted from any node
- When a key is deleted from an internal node, the node's children needs to be rearranged
- A node should not get too small during deletion
- Case 1: Key is in a leaf node -> Delete the key
- Case 2: Key is in an internal node
  - If the parent has at least t keys
    - Delete the predecessor of the key from parent node
    - Replace the key with the predecessor in the current node
  - If the parent has fewer than t keys and the child has at least t keys
    - Then delete the successor of the key from the child node
    - Replace the key with the successor in the current node
  - If both the parent and the child node has (t - 1) keys
    - Merge the current and the child node into the parent node
    - The parent node will contain (2t - 1) keys
    - Delete the key from the parent node
- Case 3: Key is not in the current node
  - Find the child that may contain the key
  - If the child has only (t - 1) keys but has an immediate sibling with at least t keys
    - Move a key from the current node to the child
    - Move a key from the child's sibling to the current node
  - If the child and its immediate siblings have (t - 1) keys
    - Merge the child with one sibling
    - Move a key from the current node to the merged node as a median

## B+ tree
- Variation of B-tree where data pointers are stored only at the leaf node
- The leaf nodes
  - Have an entry for every value of the search field
  - Have a data pointer to the record (or the block that contains the record)
  - Are linked together to provide ordered access to the search field to the records
- The internal nodes
  - Are only used to guide the search and don't store any data pointer
  - As a result, more key values can be stored in a node
  - Hence, they have a different order than leaf nodes
- Some search field values from the leaf nodes are repeated in the internal nodes
  - Hence takes more storage
- B tree stores the data pointers along with the key values in the internal nodes
  - This reduces the number of entries that can be packed into a node
  - And increases the number of levels which increases the search time
- B+ tree is very useful for range queries and bulk data retrieval

## Bitmap Indexing
- Used to improve performance of read-only queries that involve large datasets
- Used for a most frequently used column with low cardinality
- Each distinct value in a column is assigned a bit vector
- The vector contains a bit for each row and represents the presence or absence of the value

## Inverted Index
- Used in information retrieval systems to efficiently retrieve documents or web pages
  - Containing a specific term or set of terms
- Index is organized by terms (words) pointing to a list of documents
- Types
  - Record level: Contains a list of references to documents for each word
  - Word level: Also contains the positions of each word within a document
