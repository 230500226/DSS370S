1. `sudo systemctl start mariadb`: To stop the MariaDB service, use `sudo systemctl stop mariadb`.
2. `sudo systemctl status mariadb`: This command checks the status and has no action to reverse.
3. `sudo mysql -u root -p`: This command logs into the MariaDB server and has no action to reverse.
4. `CREATE DATABASE rustin_230500226_home_affairs;`: To drop the database, use `DROP DATABASE rustin_230500226_home_affairs;`.
5. `SHOW DATABASES;`: This command lists databases and has no action to reverse.
6. `USE rustin_230500226_home_affairs;`: This command selects the database and has no action to reverse.
7. `CREATE TABLE Citizens (CitizenID INT PRIMARY KEY, FirstName VARCHAR(50), LastName VARCHAR(50), DateOfBirth DATE, Gender VARCHAR(10), NationalID VARCHAR(20) UNIQUE);`: To drop the table, use `DROP TABLE Citizens;`.
8. `CREATE TABLE Services (ServiceID INT PRIMARY KEY, ServiceName VARCHAR(100), Description TEXT, Fee DECIMAL(10, 2), DurationMinutes INT);`: To drop the table, use `DROP TABLE Services;`.
9. `CREATE TABLE Appointments (AppointmentID INT PRIMARY KEY, CitizenID INT, ServiceID INT, AppointmentDate DATE, Status VARCHAR(20), FOREIGN KEY (CitizenID) REFERENCES Citizens(CitizenID), FOREIGN KEY (ServiceID) REFERENCES Services(ServiceID));`: To drop the table, use `DROP TABLE Appointments;`.
10. `CREATE TABLE Employees (EmployeeID INT PRIMARY KEY, FirstName VARCHAR(50), LastName VARCHAR(50), Role VARCHAR(50), HireDate DATE, Salary DECIMAL(15, 2));`: To drop the table, use `DROP TABLE Employees;`.
11. `CREATE TABLE Feedback (FeedbackID INT PRIMARY KEY, CitizenID INT, ServiceID INT, FeedbackDate DATE, Rating INT CHECK(Rating BETWEEN 1 AND 5), Comments TEXT, FOREIGN KEY (CitizenID) REFERENCES Citizens(CitizenID), FOREIGN KEY (ServiceID) REFERENCES Services(ServiceID));`: To drop the table, use `DROP TABLE Feedback;`.
12. `SHOW TABLES;`: This command lists tables and has no action to reverse.
13. `DESCRIBE Citizens;`: This command describes the table and has no action to reverse.
14. `DESCRIBE Services;`: This command describes the table and has no action to reverse.
15. `DESCRIBE Appointments;`: This command describes the table and has no action to reverse.
16. `DESCRIBE Employees;`: This command describes the table and has no action to reverse.
17. `DESCRIBE Feedback;`: This command describes the table and has no action to reverse.
18. `INSERT INTO Citizens (CitizenID, FirstName, LastName, DateOfBirth, Gender, NationalID) VALUES (1, 'John', 'Doe', '1980-01-01', 'Male', '1234567890'), (2, 'Jane', 'Smith', '1990-02-02', 'Female', '0987654321'), (3, 'Alice', 'Johnson', '1985-03-03', 'Female', '1122334455'), (4, 'Bob', 'Brown', '1975-04-04', 'Male', '6677889900'), (5, 'Charlie', 'Davis', '2000-05-05', 'Male', '3344556677');`: To delete the inserted records, use `DELETE FROM Citizens WHERE CitizenID IN (1, 2, 3, 4, 5);`.
19. `INSERT INTO Services (ServiceID, ServiceName, Description, Fee, DurationMinutes) VALUES (1, 'Passport Application', 'Application for a new passport', 100.00, 30), (2, 'ID Renewal', 'Renewal of national ID', 50.00, 20), (3, 'Birth Certificate', 'Issuance of birth certificate', 20.00, 15), (4, 'Marriage Certificate', 'Issuance of marriage certificate', 30.00, 25), (5, 'Driver's License', 'Application for driver's license', 70.00, 45);`: To delete the inserted records, use `DELETE FROM Services WHERE ServiceID IN (1, 2, 3, 4, 5);`.
20. `INSERT INTO Appointments (AppointmentID, CitizenID, ServiceID, AppointmentDate, Status) VALUES (1, 1, 1, '2025-03-10', 'Completed'), (2, 2, 2, '2025-03-11', 'Pending'), (3, 3, 3, '2025-03-12', 'Cancelled'), (4, 4, 4, '2025-03-13', 'Completed'), (5, 5, 5, '2025-03-14', 'Pending');`: To delete the inserted records, use `DELETE FROM Appointments WHERE AppointmentID IN (1, 2, 3, 4, 5);`.
21. `INSERT INTO Employees (EmployeeID, FirstName, LastName, Role, HireDate, Salary) VALUES`: To delete the inserted records, use `DELETE FROM Employees WHERE EmployeeID IN (...);` (replace `...` with actual EmployeeIDs once provided).
22. `SELECT * FROM Citizens;`: This command selects records and has no action to reverse.
23. `SELECT * FROM Services;`: This command selects records and has no action to reverse.
24. `INSERT INTO Services (ServiceID, ServiceName, Description, Fee, DurationMinutes) VALUES (6, 'New Service', 'Description', 25.00, 10);`: To delete the inserted record, use `DELETE FROM Services WHERE ServiceID = 6;`.
25. `DELETE FROM Citizens;`: This command attempts to delete all records from the `Citizens` table but fails due to foreign key constraints. To reverse a deletion, you would generally restore from a backup if not constrained.
