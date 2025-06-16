---

# Assignment: Advanced SQL Database Management  
**Database Name:** `Rusitn230500226`  

## Introduction  
This guide demonstrates the use of advanced SQL queries and features in MySQL. The following solutions use a database named after my surname and student number as required.

---

## Database and Table Creation

```sql
-- Create the database
CREATE DATABASE Rusitn230500226;
USE Rusitn230500226;

-- Table 1: Rusitn_Students
CREATE TABLE Rusitn_Students (
    StudentID INT PRIMARY KEY AUTO_INCREMENT,
    FirstName VARCHAR(50),
    LastName VARCHAR(50),
    Email VARCHAR(100) UNIQUE,
    EnrollmentDate DATE
);

-- Table 2: Rusitn_Courses
CREATE TABLE Rusitn_Courses (
    CourseID INT PRIMARY KEY AUTO_INCREMENT,
    CourseName VARCHAR(100),
    Department VARCHAR(50),
    Credits INT,
    Instructor VARCHAR(50)
);

-- Table 3: Rusitn_Enrollments
CREATE TABLE Rusitn_Enrollments (
    EnrollmentID INT PRIMARY KEY AUTO_INCREMENT,
    StudentID INT,
    CourseID INT,
    Grade CHAR(2),
    EnrollDate DATE,
    FOREIGN KEY (StudentID) REFERENCES Rusitn_Students(StudentID),
    FOREIGN KEY (CourseID) REFERENCES Rusitn_Courses(CourseID)
);

-- Table 4: Rusitn_Instructors
CREATE TABLE Rusitn_Instructors (
    InstructorID INT PRIMARY KEY AUTO_INCREMENT,
    Name VARCHAR(50),
    Department VARCHAR(50),
    Email VARCHAR(100) UNIQUE,
    HireDate DATE
);

-- Table 5: Rusitn_Departments
CREATE TABLE Rusitn_Departments (
    DepartmentID INT PRIMARY KEY AUTO_INCREMENT,
    DepartmentName VARCHAR(50),
    OfficeLocation VARCHAR(50),
    Head VARCHAR(50),
    Budget DECIMAL(10,2),
    EstablishedYear INT
);
```

**Note:** Each table has at least 5 columns (degree) and will hold at least 4 records (cardinality) as required.

---

## 1. Demonstrating an Advanced Query: Common Table Expressions (CTE)

**CTEs** are advanced SQL features that allow for temporary result sets which can be referenced within a SELECT, INSERT, UPDATE, or DELETE statement.

```sql
-- Example: Find students with above-average grades using a CTE

WITH GradeAverages AS (
    SELECT StudentID, AVG(
        CASE 
            WHEN Grade = 'A' THEN 4
            WHEN Grade = 'B' THEN 3
            WHEN Grade = 'C' THEN 2
            WHEN Grade = 'D' THEN 1
            ELSE 0
        END
    ) AS GPA
    FROM Rusitn_Enrollments
    GROUP BY StudentID
)
SELECT s.FirstName, s.LastName, g.GPA
FROM GradeAverages g
JOIN Rusitn_Students s ON s.StudentID = g.StudentID
WHERE g.GPA > (SELECT AVG(GPA) FROM GradeAverages);
```

**Explanation:**  
- The CTE `GradeAverages` calculates GPA for each student.  
- The main query selects students whose GPA is above the overall average.
- **Why Advanced?** CTEs improve query readability and enable complex data transformations.

---

## 2. Demonstrating a Stored Procedure

Stored procedures are reusable SQL code blocks that perform operations on the database.

```sql
DELIMITER //

CREATE PROCEDURE GetStudentCourses(IN sid INT)
BEGIN
    SELECT c.CourseName, e.Grade
    FROM Rusitn_Enrollments e
    JOIN Rusitn_Courses c ON e.CourseID = c.CourseID
    WHERE e.StudentID = sid;
END //

DELIMITER ;
```

**Usage:**
```sql
CALL GetStudentCourses(1);
```

**Opportunities:**  
- Encapsulation of complex logic.
- Centralized updates to business rules.
- Improved security by restricting direct table access.

---

## 3. Demonstrating a Trigger

Triggers automatically execute predefined actions in response to specified events on a table.

```sql
-- Trigger: Log updates to student grades
CREATE TABLE Rusitn_GradeLog (
    LogID INT PRIMARY KEY AUTO_INCREMENT,
    EnrollmentID INT,
    OldGrade CHAR(2),
    NewGrade CHAR(2),
    ChangedAt TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

DELIMITER //

CREATE TRIGGER trg_GradeUpdate
AFTER UPDATE ON Rusitn_Enrollments
FOR EACH ROW
BEGIN
    IF OLD.Grade <> NEW.Grade THEN
        INSERT INTO Rusitn_GradeLog (EnrollmentID, OldGrade, NewGrade)
        VALUES (OLD.EnrollmentID, OLD.Grade, NEW.Grade);
    END IF;
END //

DELIMITER ;
```

**Adaptation:**  
- This trigger logs every grade update, which is helpful for audits and rollback.

---

## 4. Demonstrating Cursor, Function, and Event

### Cursor Example

```sql
DELIMITER //

CREATE PROCEDURE ListAllStudentEmails()
BEGIN
    DECLARE finished INT DEFAULT 0;
    DECLARE email VARCHAR(100);
    DECLARE email_cursor CURSOR FOR SELECT Email FROM Rusitn_Students;
    DECLARE CONTINUE HANDLER FOR NOT FOUND SET finished = 1;

    OPEN email_cursor;

    read_loop: LOOP
        FETCH email_cursor INTO email;
        IF finished = 1 THEN
            LEAVE read_loop;
        END IF;
        SELECT email;
    END LOOP;

    CLOSE email_cursor;
END //

DELIMITER ;
```

### Function Example

```sql
DELIMITER //

CREATE FUNCTION CountEnrollments(course INT) RETURNS INT
DETERMINISTIC
BEGIN
    DECLARE total INT;
    SELECT COUNT(*) INTO total FROM Rusitn_Enrollments WHERE CourseID = course;
    RETURN total;
END //

DELIMITER ;
```

### Event Example

```sql
-- Enable event scheduler if not already enabled
SET GLOBAL event_scheduler = ON;

-- Event: Automatic grade reset at semester start
CREATE EVENT ResetGrades
ON SCHEDULE AT '2025-07-01 00:00:00'
DO
    UPDATE Rusitn_Enrollments SET Grade = NULL;
```

**Trends:**  
- Cursors process row-by-row logic (not common but useful for certain tasks).
- Functions enable reusable logic for computed values.
- Events automate scheduled maintenance tasks.

---

## 5. Reflection

### a. Evaluation of Advanced Queries  
Advanced SQL queries enhance database management by enabling automation (Events), encapsulation (Procedures/Functions), and reactive actions (Triggers). They ensure data integrity, simplify maintenance, and support complex business logic.

### b. Experience  
Using these queries deepened my understanding of database automation, error handling, and modular design. Writing triggers and events required careful analysis to avoid unintended consequences.

### c. Takeaway  
Advanced queries allow for powerful, efficient, and reliable data operations. They save time and reduce human error by automating repetitive or critical tasks.

### d. Limitations  
- Complexity increases debugging difficulty.
- Some features (like events) require elevated privileges.
- Overuse can impact performance if not managed properly.

---
