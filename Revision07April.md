## 1. Attribute domains for all tables

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

## Commands \and outputs

### 1. Create Database and Use It
```sql
mysql> CREATE DATABASE rustin_deece_db;
Query OK, 1 row affected (0.00 sec)

mysql> USE rustin_deece_db;
Database changed
```

### 2. Create Tables
```sql
mysql> CREATE TABLE rustin_qualification (
    ->     rustin_qual_id INT PRIMARY KEY,
    ->     rustin_qual_name VARCHAR(255),
    ->     rustin_qual_desc VARCHAR(255),
    ->     rustin_qual_duration INT,
    ->     rustin_qual_level VARCHAR(50)
    -> );
Query OK, 0 rows affected (0.03 sec)

mysql> CREATE TABLE rustin_subject (
    ->     rustin_subj_id INT PRIMARY KEY,
    ->     rustin_subj_name VARCHAR(255),
    ->     rustin_subj_desc VARCHAR(255),
    ->     rustin_qual_id INT,
    ->     rustin_subj_credits INT,
    ->     FOREIGN KEY (rustin_qual_id) REFERENCES rustin_qualification(rustin_qual_id)
    -> );
Query OK, 0 rows affected (0.03 sec)

mysql> CREATE TABLE rustin_student (
    ->     rustin_stud_id INT PRIMARY KEY,
    ->     rustin_stud_name VARCHAR(255),
    ->     rustin_stud_email VARCHAR(255),
    ->     rustin_stud_phone VARCHAR(15),
    ->     rustin_qual_id INT,
    ->     FOREIGN KEY (rustin_qual_id) REFERENCES rustin_qualification(rustin_qual_id)
    -> );
Query OK, 0 rows affected (0.02 sec)
```

### 3. Show Tables
```sql
mysql> SHOW TABLES;
+---------------------------+
| Tables_in_rustin_deece_db |
+---------------------------+
| rustin_qualification      |
| rustin_student            |
| rustin_subject            |
+---------------------------+
3 rows in set (0.00 sec)
```

### 4. Populate Tables
```sql
-- Populate Qualification Table
mysql> INSERT INTO rustin_qualification VALUES 
    -> (1, 'BET', 'ET Program', 4, 'Bach'),
    -> (2, 'MET', 'Adv ET Program', 2, 'Mast'),
    -> (3, 'DET', 'Doc in ET', 5, 'Doc'),
    -> (4, 'AET', 'Assoc ET Degree', 2, 'Assoc'),
    -> (5, 'DIET', 'Dip in ET', 3, 'Dip'),
    -> (6, 'CET', 'Cert ET Program', 1, 'Cert');
Query OK, 6 rows affected (0.02 sec)

-- Populate Subject Table
mysql> INSERT INTO rustin_subject VALUES 
    -> (1, 'Math 1', 'Intro to Math', 1, 10),
    -> (2, 'Math 2', 'Inter Math', 1, 10),
    -> (3, 'Math 3', 'Adv Math', 1, 10),
    -> (4, 'Phys 1', 'Intro to Phys', 1, 10),
    -> (5, 'Phys 2', 'Inter Phys', 1, 10),
    -> (6, 'Phys 3', 'Adv Phys', 1, 10);
Query OK, 6 rows affected (0.02 sec)

-- Populate Student Table
mysql> INSERT INTO rustin_student VALUES 
    -> (1, 'J Doe', 'jd1@example.com', '1234567890', 1),
    -> (2, 'J Doe 2', 'jd2@example.com', '1234567891', 1),
    -> (3, 'J Doe 3', 'jd3@example.com', '1234567892', 1),
    -> (4, 'J Doe 4', 'jd4@example.com', '1234567893', 1),
    -> (5, 'J Doe 5', 'jd5@example.com', '1234567894', 1),
    -> (6, 'J Doe 6', 'jd6@example.com', '1234567895', 1);
Query OK, 6 rows affected (0.02 sec)
```

### 5. Select All Records from Each Table
```sql
mysql> SELECT * FROM rustin_qualification;
+----------------+------------------+------------------+----------------------+-------------------+
| rustin_qual_id | rustin_qual_name | rustin_qual_desc | rustin_qual_duration | rustin_qual_level |
+----------------+------------------+------------------+----------------------+-------------------+
|              1 | BET              | ET Program       |                    4 | Bach              |
|              2 | MET              | Adv ET Program   |                    2 | Mast              |
|              3 | DET              | Doc in ET        |                    5 | Doc               |
|              4 | AET              | Assoc ET Degree  |                    2 | Assoc             |
|              5 | DIET             | Dip in ET        |                    3 | Dip               |
|              6 | CET              | Cert ET Program  |                    1 | Cert              |
+----------------+------------------+------------------+----------------------+-------------------+
6 rows in set (0.00 sec)

mysql> SELECT * FROM rustin_subject;
+----------------+------------------+------------------+----------------+---------------------+
| rustin_subj_id | rustin_subj_name | rustin_subj_desc | rustin_qual_id | rustin_subj_credits |
+----------------+------------------+------------------+----------------+---------------------+
|              1 | Math 1           | Intro to Math    |              1 |                  10 |
|              2 | Math 2           | Inter Math       |              1 |                  10 |
|              3 | Math 3           | Adv Math         |              1 |                  10 |
|              4 | Phys 1           | Intro to Phys    |              1 |                  10 |
|              5 | Phys 2           | Inter Phys       |              1 |                  10 |
|              6 | Phys 3           | Adv Phys         |              1 |                  10 |
+----------------+------------------+------------------+----------------+---------------------+
6 rows in set (0.00 sec)

mysql> SELECT * FROM rustin_student;
+----------------+------------------+-------------------+-------------------+----------------+
| rustin_stud_id | rustin_stud_name | rustin_stud_email | rustin_stud_phone | rustin_qual_id |
+----------------+------------------+-------------------+-------------------+----------------+
|              1 | J Doe            | jd1@example.com   | 1234567890        |              1 |
|              2 | J Doe 2          | jd2@example.com   | 1234567891        |              1 |
|              3 | J Doe 3          | jd3@example.com   | 1234567892        |              1 |
|              4 | J Doe 4          | jd4@example.com   | 1234567893        |              1 |
|              5 | J Doe 5          | jd5@example.com   | 1234567894        |              1 |
|              6 | J Doe 6          | jd6@example.com   | 1234567895        |              1 |
+----------------+------------------+-------------------+-------------------+----------------+
6 rows in set (0.00 sec)
```

### 6. Select Distinct Values from Each Table
```sql
mysql> SELECT DISTINCT rustin_qual_name FROM rustin_qualification;
+------------------+
| rustin_qual_name |
+------------------+
| BET              |
| MET              |
| DET              |
| AET              |
| DIET             |
| CET              |
+------------------+
6 rows in set (0.02 sec)

mysql> SELECT DISTINCT rustin_subj_name FROM rustin_subject;
+------------------+
| rustin_subj_name |
+------------------+
| Math 1           |
| Math 2           |
| Math 3           |
| Phys 1           |
| Phys 2           |
| Phys 3           |
+------------------+
6 rows in set (0.00 sec)

mysql> SELECT DISTINCT rustin_stud_name FROM rustin_student;
+------------------+
| rustin_stud_name |
+------------------+
| J Doe            |
| J Doe 2          |
| J Doe 3          |
| J Doe 4          |
| J Doe 5          |
| J Doe 6          |
+------------------+
6 rows in set (0.00 sec)
```

### 7. Use Order By
```sql
mysql> SELECT * FROM rustin_student ORDER BY rustin_stud_name;
+----------------+------------------+-------------------+-------------------+----------------+
| rustin_stud_id | rustin_stud_name | rustin_stud_email | rustin_stud_phone | rustin_qual_id |
+----------------+------------------+-------------------+-------------------+----------------+
|              1 | J Doe            | jd1@example.com   | 1234567890        |              1 |
|              2 | J Doe 2          | jd2@example.com   | 1234567891        |              1 |
|              3 | J Doe 3          | jd3@example.com   | 1234567892        |              1 |
|              4 | J Doe 4          | jd4@example.com   | 1234567893        |              1 |
|              5 | J Doe 5          | jd5@example.com   | 1234567894        |              1 |
|              6 | J Doe 6          | jd6@example.com   | 1234567895        |              1 |
+----------------+------------------+-------------------+-------------------+----------------+
6 rows in set (0.00 sec)
```

### 8. Use Aggregation
```sql
mysql> SELECT AVG(rustin_subj_credits) AS avg_credits FROM rustin_subject;
+-------------+
| avg_credits |
+-------------+
|     10.0000 |
+-------------+
1 row in set (0.01 sec)
```
