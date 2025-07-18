# DSS370S Normalisation 230500226 Rustin

---

## a) **Unnormalised Table (UNF)**

This table contains repeating groups, duplicates, and is not atomic.

| StudentID   | StudentName | Qualification | Modules                            |
|-------------|-------------|---------------|-------------------------------------|
| 230500110   | Alex Smith  | BEng Elec     | Circuits, Signals                   |
| 230500111   | Jamie Lee   | BEng Comp     | Programming, Databases, Networks    |
| 230500112   | Alex Smith  | BEng Elec     | Circuits, Signals                   |
| 230500113   | Chris Kim   | BEng Elec     | Circuits, Control                   |

**Notes:**
- "Modules" contains multiple values (not atomic).
- Duplicate students (Alex Smith, IDs 230500110 and 230500112).
- Functional dependencies are unclear.

---

## b) **First Normal Form (1NF)**

Remove repeating groups and ensure atomic values.

| StudentID   | StudentName | Qualification | Module      |
|-------------|-------------|---------------|-------------|
| 230500110   | Alex Smith  | BEng Elec     | Circuits    |
| 230500110   | Alex Smith  | BEng Elec     | Signals     |
| 230500111   | Jamie Lee   | BEng Comp     | Programming |
| 230500111   | Jamie Lee   | BEng Comp     | Databases   |
| 230500111   | Jamie Lee   | BEng Comp     | Networks    |
| 230500112   | Alex Smith  | BEng Elec     | Circuits    |
| 230500112   | Alex Smith  | BEng Elec     | Signals     |
| 230500113   | Chris Kim   | BEng Elec     | Circuits    |
| 230500113   | Chris Kim   | BEng Elec     | Control     |

**Notes:**
- Each cell contains a single value.
- Duplicates still exist.
- Some redundancy and functional dependency issues remain.

---

## c) **Second Normal Form (2NF)**

Remove partial dependencies; each non-key attribute is fully dependent on the whole primary key.

**Student Table**

| StudentID   | StudentName | Qualification |
|-------------|-------------|---------------|
| 230500110   | Alex Smith  | BEng Elec     |
| 230500111   | Jamie Lee   | BEng Comp     |
| 230500112   | Alex Smith  | BEng Elec     |
| 230500113   | Chris Kim   | BEng Elec     |

**Enrollment Table**

| StudentID   | Module      |
|-------------|-------------|
| 230500110   | Circuits    |
| 230500110   | Signals     |
| 230500111   | Programming |
| 230500111   | Databases   |
| 230500111   | Networks    |
| 230500112   | Circuits    |
| 230500112   | Signals     |
| 230500113   | Circuits    |
| 230500113   | Control     |

**Notes:**
- Non-key attributes depend on the whole primary key.
- Student and module assignments are separated.

---

## d) **Third Normal Form (3NF)**

Remove transitive dependencies; non-key attributes should not depend on other non-key attributes.

**Student Table**

| StudentID   | StudentName | QualificationID |
|-------------|-------------|-----------------|
| 230500110   | Alex Smith  | Q01             |
| 230500111   | Jamie Lee   | Q02             |
| 230500112   | Alex Smith  | Q01             |
| 230500113   | Chris Kim   | Q01             |

**Qualification Table**

| QualificationID | QualificationName |
|-----------------|------------------|
| Q01             | BEng Elec        |
| Q02             | BEng Comp        |

**Enrollment Table**

| StudentID   | ModuleID  |
|-------------|-----------|
| 230500110   | CIR250S   |
| 230500110   | SIG250S   |
| 230500111   | PROG250S  |
| 230500111   | DAT250S   |
| 230500111   | NET250S   |
| 230500112   | CIR250S   |
| 230500112   | SIG250S   |
| 230500113   | CIR250S   |
| 230500113   | CON250S   |

**Module Table**

| ModuleID   | ModuleName  |
|------------|-------------|
| CIR250S    | Circuits    |
| SIG250S    | Signals     |
| PROG250S   | Programming |
| DAT250S    | Databases   |
| NET250S    | Networks    |
| CON250S    | Control     |

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
