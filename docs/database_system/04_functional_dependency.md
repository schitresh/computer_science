# Functional Dependency
- A functional dependency A -> B in a relation holds if
  - Two tuples having the same value of attribute A also have the same value for attribute B
- Examples
  - `student_id -> student_name`, `state -> country` hold
  - `student_name -> state` doesn't hold
- Advantages
  - Reduces data redundancy
  - Enhances data integrity and guarantees that data is consistent
  - Simplifies adding, editing, & removing data
- Disadvantages
  - Overly restrictive functional dependencies can slow query performance
  - They don't take the semantic meaning of data into account
    - May not reflect the true relationships between data elements
- Functional dependency set of a relation is the set of all FDs in that relation

### Trivial FD
- A FD X -> Y is trivial if Y is a subset or X
- That is, if the set of dependent attributes are included in the source attributes
- Example: {student_id, student_name} -> {student_id}
- Else it is called non-trivial FD

### Armstrong Axioms
- Axioms
  - Reflexivity: If Y is a subset of X, then X -> Y
  - Augmentation: If X -> Y, then XZ -> YZ
  - Transitivity: If X -> Y and Y -> Z, then X -> Z
- Secondary Rules: Derived from the above axioms
  - Union: If X -> Y and X -> Z, then X -> YZ
  - Composition: If X -> Y and A -> B, then XA -> YB
  - Decomposition: If X -> YZ, then X -> Y and X -> Z
  - Pseudo Transitivity: If X -> Y and YA -> Z, then XA -> Z
  - Self Determination: X -> X
  - Extensivity
    - If XA -> X and X -> Y, then XA -> Y
    - If XY -> XYZ and XYZ -> YZ, then XY -> YZ

### Equivalence of FD
- Let F and G be two FD sets for a relation
- If F can be derived from G, then F is a subset of G
- If G can be derived from F, then G is a subset of F
- If both of the above are true, then F = G

## Attribute Closure
- Attribute closure of an attribute set
  - Is the set of attributes that can be functionally determined from it
  - If the set of attributes is A, then its attribute closure is represented as A+
- Example: For a Student table
  - (student_id)+ = {student_id, name, phone, state, country}
    - If student_id is known, then the mentioned attributes can be determined from it
  - (student_state)+ = {student_state, student_country}
- Advantages
  - Identifies all attributes that can be derived from a given set of attributes
    - And ensures data consistency
  - Identifies relationships between attributes and tables
    - Helpful to optimize query performance
- Disadvantages
  - As the number of attributes & tables increase, it can become complex to manage
  - They don't take the semantic meaning of data into account

### Finding Keys
- An attribute set will be a super key if
  - The attribute closure of the set contains all attributes of relation
- This attribute set will also be a candidate key if
  - No subset of the set can functionally determine all attributes of the relation
- Prime Attributes: Attributes that are parts of any candidate key of a relation
  - Other attributes are called non-prime attributes

## Canonical Cover
- Managing a large set of functional dependencies can result in
  - Unnecessary computational overhead
  - This is where the canonical cover becomes useful
- A canonical cover of a set of FDs
  - Is a simplified version of FDs that retains the same closure as the original set
  - Ensuring no redundancy
- Extranious Attribute of FD
  - If it can be removed from LHS without changing the closure of the set of FDs
- Advantages
  - Essential for optimizing database management systems
  - Simplifies and minimizes the dependencies while preserving their properties
    - Reducing computational overhead, and improving efficiency
  - By reducing, eliminating, and minimizing dependencies, canonical cover creates
    - A minimal, unique, and accurate representation of the original set
  - It helps to reduce data redundancy, improves query performance
    - And makes database maintenance easier.
- Application
  - Whenever a user updates the database
    - The system must check if any of the FDs are getting violated
  - If there are violations in the new database state, then the system must roll back
  - Working with a huge set of FD can cause unnecessarily added computational time
  - Useful to provide simplified set of FD to determine keys

### Finding Canonical Cover
- Reduction
  - Remove redundant dependencies
  - Combine dependencies that have common attributes on LHS
- Elimination: Eliminate extraneous attributes from LHS
- Minimization: Remove dependencies that are implied by other dependencies
- Example: A -> BC, B -> C, AB -> C
  - Reduction: A -> B (A -> BC && B -> C), A -> C (AB -> C && B -> C)
  - Elimination: A -> C (A -> B && B -> C)
  - Minimization: Remove AB -> C since A -> C

### F Canonically Covers G
- Consider two sets of FD
  - F = { A -> B, AB -> C, D -> AC, D -> E }
  - G = { A -> BC, D -> AB }
- Create singleton RHS
  - F = { A -> B, AB -> C, D -> A, D -> C, D -> E }
  - G = { A -> B, A -> C, D -> A, D -> B}
- Remove extraneous attributes
  - F = { A -> B, A -> C, D -> A, D -> C, D -> E }
    - Remove B from AB -> C since A -> B && AB -> C
  - G = { A -> B, A -> C, D -> A, D -> B}
    - No changes since all LHS have single attributes
- Remove redundant FDs
  - F = { A -> B, A -> C, D -> A, D -> E }
    - D -> C can be derived from D -> A && A -> C
  - G = { A -> B, A -> C, D -> A }
    - D -> B can be derived from D -> A && A -> B
- All FDs of G are covered in F, so F covers G
