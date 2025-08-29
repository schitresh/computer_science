# Normalization
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
- Example: Student (id: 1, phone: [1234, 5678])
  - Student is not in 1NF because phone has 2 values
  - Break the row into 2 rows to make it 1NF
    - Student (id: 1, phone: 1234)
    - Student (id: 1, phone: 5678)

### Second (2NF)
- Relation is in 2NF if any one of the following holds true
  - Candidate key is single valued
  - Candidate key is multi valued, but there is no partial dependency in the relation
    - Any non-prime attribute should not be dependent on any proper subset of any candidate key
- Reduces redundant data
  - Student (id, course_id, course_fee)
  - If 100 students are taking the same course, no need to store its fee 100 times
- Consider X -> Y & A -> Y
  - Let's say X is a composite candidate key {A, B}
  - It is a partial dependency because Y is non-prime and depends only on A
    - And A is a proper subset of the candidate key {A, B}
    - If A -> Y was not present, it will be in 2NF
  - If the candidate key X was single valued (say B -> Y)
    - Then also it will be in 2NF
- Proper subset
  - A proper subset is a set that contains some but not all elements of another set
  - E.g. {1} is proper subset of {1, 2}, but {1, 2} is subset (not proper) of {1, 2}
- Example: StudentCourse (id, course_id, course_fee)
  - It is not in 2NF because
    - Candidate key here is {id, course_id}
    - But course_id -> course_fee
      - course_id is a proper subset of a candidate key
      - course_fee is a non-prime attribute
        - It cannot identify a row uniquely even if combined with other attributes
    - It is a partial dependency and so this relation is not in 2NF
  - Break the table into 2 tables to make it 2NF
    - StudentCourse (id, course_id)
    - Course (id, course_fee)

### Third (3NF)
- No transitive dependency for non-prime attributes on any candidate key
  - If A -> B and B -> C, then A -> C is called transitive dependency
  - Ensures that FD is preserved and lossless
- Alternatively, we can say that for a non-trivial FD X -> Y
  - Atleast one of the following conditions should hold true
  - X is a super key
  - Y is a prime attribute
- 3NF is considered adequate for normal RDBMS
  - Because most of the 3NF tables are free of anomalies
- Example: Student (id, name, state, country)
  - It is not in 3NF because
    - id -> state and state -> country
      - Country is a non-prime attribute since the candidate key is {id}
      - But it depends transitively on id (which is candidate key)
    - Alternatively, country is non-prime and state is not super key
      - But state -> country
  - Break the table into 2 tables to make it 3NF
    - Student (id, name, state)
    - StateCountry (state, country)
- Example 2:
  - StudentCourse (id, course, instructor, instructor_email)
    - {id, course} -> instructor (a course can have multiple instructors)
    - instructor -> course (an instructor teaches only one course)
    - instructor -> instructor_email
    - {id, instructor} -> course (course can be determined through id & instructor)
  - Candidate keys
    - {id, course}, since a student can have multiple courses
    - {id, instructor}, since an instructor teaches only one course
  - Hence, {id, course} -> instructor -> instructor_email
    - Which is transitive dependency and hence not in 3NF
    - Alternatively, instructor_email is non-prime and instructor is not super key
  - Solution
    - Student (id, course, instructor)
    - Instructor (instructor, instructor_email)

### BCNF
- In a FD X -> Y, X must be a super key
- Advanced form for 3NF
  - This is the last practiced form
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
    - Student (id, branch)
    - StudentCourse (student_id, course_id)
    - Course (id, branch)
- Example 2:
  - StudentCourse (id, course, instructor)
    - {id, course} -> instructor (a course can have multiple instructors)
    - instructor -> course (an instructor teaches only one course)
    - {id, instructor} -> course (course can be determined through id & instructor)
  - Candidate keys
    - {id, course}, since a student can have multiple courses
    - {id, instructor}, since an instructor teaches only one course
  - Here, in instructor -> course, instructor is not a super key
    - Hence it is not in BCNF
  - Solution
    - StudentInstructor (id, instructor)
    - InstructorCourse (instructor, course)

### Fourth (4NF)
- No non-trivial multi-valued dependency except candidate key
- Multi-valued dependency (MVD)
  - If two attributes are independent of one another but both depend on a third attribute
- Example:
  - Student (id, name, course_name)
  - MVD: name & course_name are independent but id -> name, id -> course_name
  - Solution
    - Student (id, name)
    - StudentCourse (student_id, course_name)

### Fifth (5NF)
- Also called projection-join normal form (PJNF)
- No join dependency except candidate keys
  - A relation decomposed into two relations must be lossless
- Lossless Decompositionwhich
  - If relation R (A, B, C) is decomposed into R1 (A, B) & R2 (B, C)
  - It is lossless if the join of R1 & R2 over B should be equal to R
  - It is lossy if the number of joined tuples are more or less than R
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
  - Solution
    - R1 (name, faculty)
    - R2 (name, semester)
    - R3 (faculty, semester)

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
- 2NF: No, D is dependent on A (A -> D)
  - Where A is proper subset of candidate key AC

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
