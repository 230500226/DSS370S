Relationships in ER modeling define how **entities** (like `Employee` or `Department`) interact in a database. They have **participants**, a **degree** (how many entities are involved), and **cardinality** (how many instances can relate).

---

### Relationship Degrees

- **Binary (2 entities):** Most common (80% of needs). Connects two entities, e.g., `Employee` works `in` `Department`.
- **Ternary (3 entities):** Connects three entities when their interaction makes sense only together, e.g., `Student`, `Course`, and `Professor` in a `registers` relationship.
- **Complex (4+ entities):** Rare, used for highly specialized cases.

---

### Representing Relationships in ER Diagrams

- **Binary:** A simple line between entities, with the relationship name above it (e.g., `EMPLOYEE ||--o{ DEPARTMENT : "works_in"`).
- **Complex (Ternary, Quaternary, etc.):** Represented by a **diamond symbol** with the relationship name inside. All participating entities connect to this diamond. This visually distinguishes them and clarifies complex interactions (e.g., `STAFF ||--o{ REGISTRATION : registers`, `CLIENT ||--o{ REGISTRATION : is_for`, `BRANCH ||--o{ REGISTRATION : at`).

---

### Why It Matters

Using these notations ensures **clarity** and **consistency** in database design, helping to avoid issues like redundancy or ambiguous paths. Complex relationships should only be used when all participating entities are essential to the relationship's meaning.
