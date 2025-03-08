## Relational Model
- Representing data in form of tables (or relations) connected by key fields
- After designing the conceptual model of the database using ER diagram
  - It needs to be converted into a relational model
  - So that it can be implemented using the language of RDBMS
- Relational Schema
  - Structure of a relation
  - The number of attributes in a relation is called its degree
  - Example: Student (id, name, email)
- Relational Instance
  - Set of values present in a relationship
  - The number of these instances is called cardinality
  - Example: Student (id: 1, name: 'Test', email: 'test@email.com')
- Relational Algebra
  - Set of operations that can be performed on relations

## Codd's Rules
- Checks whether DBMS has the quality to become RDBMS
- It's rare to fulfill all the rules, generally 8-9 rules are followed
- These 13 rules are popularly known as Codd's 12 rules (index 0 - 12)
- Rule 0: Foundation
  - Must be able to manage databases entirely through its relational capabilities
- Rule 1: Information
  - Data stored must be a value of some cell of a table
- Rule 2: Guaranteed Access
  - Every data element must be accessible
    - By the table name, primary key, and attribute name
- Rule 3: Systematic Treatment of NULL values
  - NULL value must only correspond to missing, unknown, or not applicable values
- Rule 4: Active Online Catalog
  - Structure of the database must be stored in an online catalog
    - That can be queried by authorized users
- Rule 5: Comprehensive Data Sub-language
  - Database should be accessible by a language
    - Supported for definition, manipulation, & transaction management
- Rule 6: View Updating Rule
  - Different views should be updatable by the system
- Rule 7: High level insert, update & delete
  - Should support operations like insert, delete, update, etc at each level of relations
- Rule 8: Physical Data Independence
  - Any modification in physical location of table should not affect application level
- Rule 9: Logical Data Independence
  - Any modification in conceptual schema of table should not affect application level
  - Example: Merging two tables into one
    - Should not affect the application accessing it (difficult to achieve)
- Rule 10: Integrity Independence
  - Integrity constraints modified at database level should not affect application level
- Rule 11: Distribution Independence
  - Distribution of data over various locations should not be visible to end-users
- Rule 12: Non-subversion
  - Low level access to data should not be able to bypass the integrity rule to change data

## Relation Keys
- Keys are used to identify a row in a table uniquely
- It also helps in setting relationship between various columns & tables
- Super: A set of any number of attributes that can identify a row uniquely
- Candidate: Minimal set of attributes that can identify a row uniquely
- Primary: One key chosen out of candidate keys to identify a row uniquely
- Composite: If a combination of attributes are used as the primary key
- Alternate: Candidate keys except the primary key
- Foreign
  - A reference key that can identify a row uniquely in the related table
  - It should be a primary key in the referenced table

## Constraints
- While designing a relational model
  - The conditions defined that must hold true for the data
  - These constraints are checked before performing any operation in database
- Domain Constraints
  - Attribute level constraints, e.g. age should be > 0 for Student relation
- Key Integrity
  - Every relation should have at least one key to uniquely identify a row
  - It cannot have NULL values
- Referential Integrity
  - When one attribute of a relation can only take values
    - From another attribute of the same or another relation
  - Example: branch_code in Branch relation referenced in Student relation
    - Referencing relation: Student (id, name, branch_code)
    - Referenced relation: Branch (branch_code, branch_name)

## Anomalies
- Insertion
  - Referencing attribute cannot have a value that is not present in the referenced attribute
- Deletion
  - Referenced attribute cannot be deleted if its present in a referencing attribute
- Updation
  - Referenced attribute cannot be updated if its present in a referencing attribute
- Solutions for Deletion/Updation
  - Cascade: Deletes/Updates the referencing rows if the referenced row is deleted/updated
  - Set NULL in referencing rows
- Normalization can be used to minimize these anamolies

## Data Warehouse Modeling
### Star Schema
- Data is organized into a central fact table
  - That contains metrics or measures that are of interest
  - In a sales data warehouse
    - Fact table might contain sales revenue, units sold, profit margins
  - Each record in the fact table represents a specific event or transaction
    - Like a sale or order
- Fact table is surrounded by dimension tables
  - That describe the attributes of the measures
  - These attributes are used to slice and dice the data in fact table
  - This allows users to analyze the data from different perspectives
  - In a sales data warehouse
    - Dimension tables might include product, customer, time & location
- Each dimension table is joined to fact table through a foreign key relationship
  - A user might want sales revenue by product category or region or time period
- It improves the data retrieval and is used by many OLAP systems

### Snowflake Schema
- Variant of star schema
  - Where dimensions are present in a normalized form im multiple related tables
  - The dimensions are detailed and highly structured having several levels of relationship
  - The child tables might have multiple parent tables
- These tables are maintained in normalized form to reduce redundancy
  - It makes them easy to maintain
  - Though more joins are required that impact the performance

## Relational Algebra
- Union: `A U B`
- Intersection: `A ∩ B`
- Difference: `A - B`
- Cartesian Product: `A X B`
- Selection: `σ condition (relation_name)`
  - Displays all attributes
- Projection: `π (col1, col2) relation_name`
- Divide: `A ÷ B`
- Rename: `ρ (old_relation, new_relation)`

### Joins
- Outer Joins
  - Left: `A ⟕ B`
  - Right: `A ⟖ B`
  - Full: `A ⟗ B`
- Inner Joins
  - Conditional or Theta: `A ⋈ θ B`, theta denotes conditions
  - Equi: `A ⋈ A.column1 =  B.column2 (B)`
  - Natural: `A ⋈ B`
    - If there is a common attribute with the same name & type

### Nested vs Join Queries
- Nested queries
  - Only relevant info from each table can be extracted
  - Can lead to bugs or poor performance, optimization depends on the developer
  - Every constant subquery is evaluated as many times encountered
    - Large subqueries may take time to execute
- Join queries
  - Whole tables are fetched and a large table is created from which filtering happens
  - Joins are universally understood, so no optimization issues can arise
  - Foreign & primary keys are usually indexed
    - So performs better than large subqueries
