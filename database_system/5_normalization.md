## Normalization
- Process of organizing attributes to reduce data redundancy
- Data redundancy
  - Advantages
    - Data is readily accessible
    - Enhances query performance since less joins are required
  - Disadvantages
    - Increased storage size
    - Inconsistency problems or anamolies during insert, update, delete operations
- Data consistency: Keeps data consistent at all places
- Data integrity: Ensures data accuracy and protects against data loss & leaks
- Simplifies data management by breaking down complex tables

## Normal Forms
- The default requirement for a normal form is to satify all the previous normal forms

### First (1NF)
- No composite or multi-valued attributes in the relation
- Helps eliminate duplicate data and simplifies queries
- Example:
  - Student (id: 1, phone: [1234, 5678]) is not in 1NF because it has 2 values
  - Break the row into 2 rows to make it 1NF
    - Student (id: 1, phone: 1234), Student (id: 1, phone: 5678)

### Second (2NF)
- No partial dependency in the relation
  - No non-prime attribute should be dependent on any proper subset of any candidate key
- Reduces redundant data
  - If 100 students are taking the same course, no need to store its fee 100 times
- Example:
  - Student (id, course_id, course_fee) is not in 2NF
    - course_fee is a non-prime attribute
      - It cannot identify a row uniquely even if combined with other attributes
    - But course_id -> course_fee (course_free is dependent on course_id)
    - And course_id is a proper subset of a candidate key
      - It cannot identify a row uniquely on its own
  - Break the table into 2 tables to make it 2NF
    - Student (id, course_id), Course (id, course_fee)

### Third (3NF)
- No transitive dependency for non-prime attributes
  - Ensures that FD is preserved and lossless
  - If A -> B and B -> C, then A -> C is called transitive dependency
- Alternatively, we can say that for a non-trivial FD X -> Y
  - Atleast one of the following conditions should hold true
  - X is a super key
  - Y is a prime attribute
- 3NF is considered adequate for normal RDBMS
  - Because most of the 3NF tables are free of anomalies
- Example:
  - Student (id, name, state, country) is not in 3NF
    - Since id -> state and state -> country
  - Break the table into 2 tables to make it 3NF
    - Student (id, name, state), StateCountry (state, country)

### BCNF
- Advanced form for 3NF where in a FD X -> Y, X must be a super key
  - This is the last practiced forms
  - Forms beyond like 4NF & 5NF are used only for theoritical purposes
- Example:
  - Student (id, course, branch)
    - Student (id: 1, course: 'DSA', branch: 'CSE')
    - Student (id: 1, course: 'OS', branch: 'CSE')
    - Student (id: 1, course: 'Networks', branch: 'CSE')
  - For id -> branch, id is not a super key
    - Since there can be multiple values with same id
  - For course -> branch, course is not a super key
    - Since multiple courses can have same branch
  - Break the table into 3 tables to make it BCNF
  - Student (id, branch), StudentCourse (student_id, course_id), Course (id, branch)

### Fourth (4NF)
- No non-trivial multi-valued dependency except candidate key
- Multi-valued dependency (MVD)
  - If two attributes are independent of one another but both depend on a third attribute
- Example:
  - Student (id, name, course_name)
  - MVD: name & course_name are independent but id -> name, id -> course_name
  - Solution: Student (id, name), StudentCourse (student_id, course_name)

### Fifth (5NF)
- Also called projection-join normal form (PJNF)
- No join dependency except candidate keys
  - A relation decomposed into two relations must be lossless
- Lossless Decomposition
  - If relation R (A, B, C) is decomposed into R1 (A, B) & R2 (B, C)
  - It is lossless if the join of R1 & R2 over B should be equal to R
  - If is lossy if the number of joined tuples are more or less than R
  - It is dependency preserving if all the FD are preserved in R1 & R2
- Example:
  - Course (name, faculty, semester)
    - Course (name: 'DSA', faculty: 'F1', semester: 1)
    - Course (name: 'DBMS', faculty: 'F1', semester: 2)
  - R1
    - Course (name: 'DSA', faculty: 'F1')
    - Course (name: 'DBMS', faculty: 'F1')
  - R2
    - Course (faculty: 'F1', semester: 1)
    - Course (faculty: 'F1', semester: 2)
  - Join (R1, R2)
    - Course (name: 'DSA', faculty: 'F1', semester: 1)
    - Course (name: 'DSA', faculty: 'F1', semester: 2)
    - Course (name: 'DBMS', faculty: 'F1', semester: 1)
    - Course (name: 'DBMS', faculty: 'F1', semester: 2)
  - The join is introducing wrong data (loss of data)
  - A row requires all the 3 attributes to be known (name, faculty, semester)
  - Hence there is a join dependency and it is not in 5NF

## Finding Normal Forms
- Find all the candidate keys (C) using attribute closure
- Divide all attributes as prime and non-prime

### Example 1
- R (A, B, C, D, E) with FD = { A -> D, B -> A, BC -> D, AC -> BE }
- Candidate keys = { AC, BC }
  - AC is a candidate key since (AC)+ = { A, C, D, B, E }
  - BC is a candidate key since B -> A
- Prime attributes = { A, B, C }
- 1NF: Yes, no composite attributes
- 2NF: No, D is dependent on A (A -> D) which is proper subset of candidate key AC

### Example 2
- R (A, B, C, D, E) with FD = { BC -> D, AC -> BE, B -> E }
- Candidate keys = { AC }
  - AC is a candidate key since (AC)+ = { A, C, B, E, D }
- Prime attributes = { A, C }
- 1NF: Yes, no composite attributes
- 2NF: Yes, LHS (BC, AC, B) doesn't have any proper subset of candidate keys
- 3NF: No
  - BC -> D: BC is not a super key, nor D is prime attribute
  - B -> E: B is not a super key, nor E is prime attribute

### Example 3
- R (A, B, C, D, E) with FD = { B -> A, A -> C, BC -> D, AC -> BE}
- Candidate keys = { A, B }
  - B is a candidate key since (B)+ = { B, A, C, D, E }
  - A is a candidate key since (A)+ = { A, C, B, E, D }
- Prime attributes = { A, B }
- 1NF: Yes, no composite attributes
- 2NF: Yes, LHS (B, A, BC, AC) doesn't have any proper subset of candidate keys
- 3NF: Yes, All LHS have super key, so no need to check prime attribute in RHS
- BCNF: Yes, All LHS have super key

## Denormalization
- Adding redundant data to tables to optimize performance and avoid costly joins
- Does not mean reversing normalization but adding redundancy after normalization
- This can make inserts & updates more expensive, but increases accessibility
