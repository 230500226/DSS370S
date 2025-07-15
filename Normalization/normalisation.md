# Database Normalisation Example

This document demonstrates the process of normalisation using a student-module-qualification scenario. Each stage is represented with sample tables and explanations:

---

## a) **Unnormalised Table (UNF)**

This table contains repeating groups, duplicates, and is not atomic.

| StudentID | StudentName | Qualification | Modules                            |
|-----------|-------------|---------------|-------------------------------------|
| 1001      | Alex Smith  | BEng Elec     | Circuits, Signals                   |
| 1002      | Jamie Lee   | BSc Comp      | Programming, Databases, Networks    |
| 1003      | Alex Smith  | BEng Elec     | Circuits, Signals                   |
| 1004      | Chris Kim   | BEng Elec     | Circuits, Control                   |

**Notes:**
- "Modules" contains multiple values (not atomic).
- Duplicate students (Alex Smith, IDs 1001 and 1003).
- Functional dependencies are unclear.

---

## b) **First Normal Form (1NF)**

Remove repeating groups and ensure atomic values.

| StudentID | StudentName | Qualification | Module      |
|-----------|-------------|---------------|-------------|
| 1001      | Alex Smith  | BEng Elec     | Circuits    |
| 1001      | Alex Smith  | BEng Elec     | Signals     |
| 1002      | Jamie Lee   | BSc Comp      | Programming |
| 1002      | Jamie Lee   | BSc Comp      | Databases   |
| 1002      | Jamie Lee   | BSc Comp      | Networks    |
| 1003      | Alex Smith  | BEng Elec     | Circuits    |
| 1003      | Alex Smith  | BEng Elec     | Signals     |
| 1004      | Chris Kim   | BEng Elec     | Circuits    |
| 1004      | Chris Kim   | BEng Elec     | Control     |

**Notes:**
- Each cell contains a single value.
- Duplicates still exist.
- Some redundancy and functional dependency issues remain.

---

## c) **Second Normal Form (2NF)**

Remove partial dependencies; each non-key attribute is fully dependent on the whole primary key.

**Student Table**

| StudentID | StudentName | Qualification |
|-----------|-------------|---------------|
| 1001      | Alex Smith  | BEng Elec     |
| 1002      | Jamie Lee   | BSc Comp      |
| 1003      | Alex Smith  | BEng Elec     |
| 1004      | Chris Kim   | BEng Elec     |

**Enrollment Table**

| StudentID | Module      |
|-----------|-------------|
| 1001      | Circuits    |
| 1001      | Signals     |
| 1002      | Programming |
| 1002      | Databases   |
| 1002      | Networks    |
| 1003      | Circuits    |
| 1003      | Signals     |
| 1004      | Circuits    |
| 1004      | Control     |

**Notes:**
- Non-key attributes depend on the whole primary key.
- Student and module assignments are separated.

---

## d) **Third Normal Form (3NF)**

Remove transitive dependencies; non-key attributes should not depend on other non-key attributes.

**Student Table**

| StudentID | StudentName | QualificationID |
|-----------|-------------|-----------------|
| 1001      | Alex Smith  | Q01             |
| 1002      | Jamie Lee   | Q02             |
| 1003      | Alex Smith  | Q01             |
| 1004      | Chris Kim   | Q01             |

**Qualification Table**

| QualificationID | QualificationName |
|-----------------|------------------|
| Q01             | BEng Elec        |
| Q02             | BSc Comp         |

**Enrollment Table**

| StudentID | ModuleID |
|-----------|----------|
| 1001      | M01      |
| 1001      | M02      |
| 1002      | M03      |
| 1002      | M04      |
| 1002      | M05      |
| 1003      | M01      |
| 1003      | M02      |
| 1004      | M01      |
| 1004      | M06      |

**Module Table**

| ModuleID | ModuleName  |
|----------|-------------|
| M01      | Circuits    |
| M02      | Signals     |
| M03      | Programming |
| M04      | Databases   |
| M05      | Networks    |
| M06      | Control     |

**Notes:**
- All tables only contain keys and directly related attributes.
- No transitive dependencies.
- StudentID uniquely identifies students, even if names repeat.

---

## **Summary**

Normalisation improves data integrity, removes redundancy, and ensures each fact is stored only once.  
- **UNF:** Data is messy, with repeats and groups.
- **1NF:** Atomic values, but redundancy remains.
- **2NF:** Removes partial dependencies.
- **3NF:** Removes transitive dependencies and achieves a fully normalised structure.
