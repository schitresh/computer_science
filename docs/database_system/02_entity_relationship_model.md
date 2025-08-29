# Entity Relationship Model
- Representation of entities and their relationships

### Representations
- Entity
  - Strong: Rectange
  - Weak: Double Rectangle
- Entity Set: Vertical Oval
- Attribute
  - Single-valued: Oval
  - Key: Oval with Underline
  - Multi-valued: Double Oval
  - Derived: Dashed Oval
- Relationship: Diamond
  - Identifying Relationship: Double Diamond
  - Participation
    - Total: Double Line
    - Partial: Line

## Entity
- Also known as Entity Type
- Strong Entity
  - Entity that has a key attribute and does not depend on other entities
  - Records are identified uniquely using primary key
- Weak Entity
  - Dependent entity with no key attribute
  - Example: Salary entity won't exist without employee entity
  - Participation: Total
- Entity Set: Set of individual entities (instances of entity type)

## Attributes
- Properties that define the entity type
- Key Attribute: Uniquely identifies each entity in the entity set
- Composite Attribute
  - Attribute composed of many other attributes
  - Example: Address consists of street, city, state, country
- Multi-valued Attribute
  - Example: There can be multiple Email for a user
- Derived Attribute
  - Example: Age attribute can be derived from date of birth

## Relationship
- Association between entity types
- Identifying Relationship
  - Relationship between weak entity & its identifying strong entity
- Relationship Set: Set of relationships of the same type

### Degree
- Number of different entity sets participating in a relationship set
- Unary
  - One entity is related to another entity of the same type
  - Example: A person is married to another person
- Binary
  - One entity is related to another entity of a different type
  - Example: A student is enrolled in a course
- N-ary
  - More than 2 entities are related
  - Example: A doctor prescribes a medicine to a patient

### Cardinality
- Number of times an entity participates in a relationship
- One to One
  - An employee can have only one salary
  - Minimum tables required
    - Total Participation: 1
      - Employee (emp_id, salary)
    - Partial Participation: 2
      - There can be disconnected entities in second table
      - If so, it can lead to empty cells for salary column in above approach
      - Employee (emp_id, salary_id), Salary (emp_id)
- One to Many
  - A company can have many employees
  - Minimum tables required: 2
  - Company (com_id), Employee (emp_id, com_id)
- Many to Many
  - A student can enroll in many courses & a course can be enrolled by many students
  - Minimum tables required: 3
  - Student (stu_id), Course (course_id), StudentCourses (stu_id, course_id)

### Participation
- Total
  - Each entity in entity set participates in the relationship
  - Each student must enroll in a course
- Partial
  - Entity in entity set may or may not participate in the relationship
  - A person may or may not have a car

## Enhanced ER Model
- Specialization (Subclass)
  - Divide an entity into sub-entities based on characteristics (Top-down approach)
  - 'is a' relationship
  - Example: Laptop is a computer (laptop is a special/sub class of computer)
  - Contraints:
    - Total or Partial
      - Total subclass if every super-class entity is to be associated
      - with some sub-class entity
    - Overlapped or Disjoint
      - Overlapping subclass if an entity from a super-set can be related (can occur)
      - in multiple sub-class sets
- Generalization (Superclass)
  - Extracting common properties and creating a generalized entity (Bottom-up approach)
  - Example: Laptop is a computer (computer is a general/super class of laptop)
- Inheritance
  - Feature that allows subclasses to inherit attributes & relationships from superclasses
- Multiple Inheritance
  - An entity can be a subclass of multiple entity types
  - Teaching Assistant can be a subclass of Employee & Student both
  - Attributes of the subclass are union of attributes of all superclasses
- Aggregation
  - Abstraction that represents a group of entities as a single entity
  - Example: An employee working on a project may require machinery
    - Aggregate entities Employee & Project
      - Are connected with the relationship 'working on'
    - Entities Employee-Project-Aggregate and Machinery
      - Are connected with the relationship 'requires'

## Recursive Relationship
- Employee & Boss (Boss is also employee)
- User & Friend (Friend is also user)
- Boss and Friend are called role names

### Employee - Boss
- Employee
  - Min cardinality = 0 (CEO can't have boss)
  - Max cardinality = 1 (employee can have only one boss)
- Boss
  - Min cardinality = 0 (individual contributors don't manage any employee)
  - Max cardinality = n (can manage many employees)
- Participation: Partial
- Relationship: Many to one
  - Employee (emp_id, boss_id)
- Foreign keys: boss_id in Employee

### User - Friend
- User
  - Min cardinality = 0
  - Max cardinality = n
- Friend
  - Min cardinality = 0
  - Max cardinality = n
- Participation: Partial
- Relationship: Many to many
  - User (user_id), Friendship (user_id, friend_user_id)
  - Store both (user_id, friend_user_id) & (friend_user_id, user_id)
    - To make it simple & scalable

## Impedance Mismatch
- When two systems or components that are supposed to work together
  - Have different data models, structures or interfaces
  - It can make communciation difficult or inefficient
- In databases, it refers to discrepancy between
  - OOP model in application code & relational model in database
  - OOP models represent data as objects with properties & methods
  - Relational model represents data as tables with columns & rows
- Challenges in mapping objects to tables & vice versa
  - Object heirarchy may need to be flattened into single table
  - Multiple related tables may need to be joined together to represent a single object
  - Data type mismatch between the programming language and the data models
- The query results can be sets or multisets of tuples
  - Where each tuple is formed of attribute values
  - The result's data structures needs to be binded
    - To the programming language's data structures
  - The tuples are required to be looped over to extract individual values
  - These can lead to performance issues, data inconsistency, development time & cost
- To overcome the impedance mismatch problem, Object Relational Mapping (ORM) is used
  - It automates the mapping process between objects & tables
