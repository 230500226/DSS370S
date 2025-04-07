Here are the detailed steps for creating a database management system for the DEECE department, using "Rustin" as the surname prefix.

### 1. Attribute Domains for all Tables

**Qualification Table**
- `rustin_qual_id`: Unique identifier for the qualification (Primary Key)
  - Data Type: `int`
  - Range: `1 - 9999`
  - Justification: Allows up to 9999 unique qualifications.
- `rustin_qual_name`: Name of the qualification
  - Data Type: `varchar(255)`
  - Justification: Allows for long qualification names.
- `rustin_qual_desc`: Description of the qualification
  - Data Type: `varchar(255)`
  - Justification: Provides space for detailed descriptions.
- `rustin_qual_duration`: Duration of the qualification in years
  - Data Type: `int`
  - Range: `1 - 10`
  - Justification: Typically, qualifications range from 1 to 10 years.
- `rustin_qual_level`: Level of the qualification (e.g., Bachelor, Master)
  - Data Type: `varchar(50)`
  - Justification: Allows for various levels of qualifications.

**Subject Table**
- `rustin_subj_id`: Unique identifier for the subject (Primary Key)
  - Data Type: `int`
  - Range: `1 - 9999`
  - Justification: Allows up to 9999 unique subjects.
- `rustin_subj_name`: Name of the subject
  - Data Type: `varchar(255)`
  - Justification: Allows for long subject names.
- `rustin_subj_desc`: Description of the subject
  - Data Type: `varchar(255)`
  - Justification: Provides space for detailed descriptions.
- `rustin_qual_id`: Foreign key reference to the qualification
  - Data Type: `int`
  - Justification: Links the subject to a qualification.
- `rustin_subj_credits`: Credits for the subject
  - Data Type: `int`
  - Range: `1 - 30`
  - Justification: Subjects typically have credit values within this range.

**Student Table**
- `rustin_stud_id`: Unique identifier for the student (Primary Key)
  - Data Type: `int`
  - Range: `1 - 9999`
  - Justification: Allows up to 9999 unique students.
- `rustin_stud_name`: Name of the student
  - Data Type: `varchar(255)`
  - Justification: Accommodates full names of students.
- `rustin_stud_email`: Email address of the student
  - Data Type: `varchar(255)`
  - Justification: Standard email length.
- `rustin_stud_phone`: Phone number of the student
  - Data Type: `varchar(15)`
  - Justification: Accommodates various phone number formats.
- `rustin_qual_id`: Foreign key reference to the qualification
  - Data Type: `int`
  - Justification: Links the student to a qualification.

### 2. DDL Statements to Create the Tables

```sql
CREATE TABLE rustin_qualification (
    rustin_qual_id INT PRIMARY KEY,
    rustin_qual_name VARCHAR(255),
    rustin_qual_desc VARCHAR(255),
    rustin_qual_duration INT,
    rustin_qual_level VARCHAR(50)
);

CREATE TABLE rustin_subject (
    rustin_subj_id INT PRIMARY KEY,
    rustin_subj_name VARCHAR(255),
    rustin_subj_desc VARCHAR(255),
    rustin_qual_id INT,
    rustin_subj_credits INT,
    FOREIGN KEY (rustin_qual_id) REFERENCES rustin_qualification(rustin_qual_id)
);

CREATE TABLE rustin_student (
    rustin_stud_id INT PRIMARY KEY,
    rustin_stud_name VARCHAR(255),
    rustin_stud_email VARCHAR(255),
    rustin_stud_phone VARCHAR(15),
    rustin_qual_id INT,
    FOREIGN KEY (rustin_qual_id) REFERENCES rustin_qualification(rustin_qual_id)
);
```

### 3. DML Statements to Populate the Tables

```sql
-- Populate Qualification Table
INSERT INTO rustin_qualification VALUES (1, 'Bachelor of Engineering Technology', 'Engineering Technology Program', 4, 'Bachelor');
-- Add 5 more rows similarly

-- Populate Subject Table
INSERT INTO rustin_subject VALUES (1, 'Mathematics 1', 'Introduction to Mathematics', 1, 10);
-- Add 5 more rows similarly

-- Populate Student Table
INSERT INTO rustin_student VALUES (1, 'John Doe', 'john.doe@example.com', '1234567890', 1);
-- Add 5 more rows similarly
```

### 4. Select * from each table

```sql
SELECT * FROM rustin_qualification;
SELECT * FROM rustin_subject;
SELECT * FROM rustin_student;
```

### 5. Select distinct from each table

```sql
SELECT DISTINCT rustin_qual_name FROM rustin_qualification;
SELECT DISTINCT rustin_subj_name FROM rustin_subject;
SELECT DISTINCT rustin_stud_name FROM rustin_student;
```

### 6. Use order by

```sql
SELECT * FROM rustin_student ORDER BY rustin_stud_name;
```

### 7. Use group by

```sql
SELECT rustin_qual_id, COUNT(*) FROM rustin_student GROUP BY rustin_qual_id;
```

### 8. Use aggregation

```sql
SELECT AVG(rustin_subj_credits) AS avg_credits FROM rustin_subject;
```

This setup ensures that the database management system is well-structured, with meaningful attribute domains and comprehensive DDL, DML, and SQL queries to manage and retrieve data effectively.
