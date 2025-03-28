1. `sudo systemctl start mariadb`: Starts the MariaDB service.
2. `sudo systemctl status mariadb`: Checks the status of the MariaDB service.
3. `sudo mysql -u root -p`: Logs into the MariaDB server as the root user with password prompt.
4. `CREATE DATABASE rustin_230500226_home_affairs;`: Creates a new database named `rustin_230500226_home_affairs`.
5. `SHOW DATABASES;`: Lists all databases in the MariaDB server.
6. `USE rustin_230500226_home_affairs;`: Selects the `rustin_230500226_home_affairs` database to use.
7. `CREATE TABLE Citizens (CitizenID INT PRIMARY KEY, FirstName VARCHAR(50), LastName VARCHAR(50), DateOfBirth DATE, Gender VARCHAR(10), NationalID VARCHAR(20) UNIQUE);`: Creates the `Citizens` table with specified columns and constraints.
8. `CREATE TABLE Services (ServiceID INT PRIMARY KEY, ServiceName VARCHAR(100), Description TEXT, Fee DECIMAL(10, 2), DurationMinutes INT);`: Creates the `Services` table with specified columns and constraints.
9. `CREATE TABLE Appointments (AppointmentID INT PRIMARY KEY, CitizenID INT, ServiceID INT, AppointmentDate DATE, Status VARCHAR(20), FOREIGN KEY (CitizenID) REFERENCES Citizens(CitizenID), FOREIGN KEY (ServiceID) REFERENCES Services(ServiceID));`: Creates the `Appointments` table with specified columns and constraints.
10. `CREATE TABLE Employees (EmployeeID INT PRIMARY KEY, FirstName VARCHAR(50), LastName VARCHAR(50), Role VARCHAR(50), HireDate DATE, Salary DECIMAL(15, 2));`: Creates the `Employees` table with specified columns and constraints.
11. `CREATE TABLE Feedback (FeedbackID INT PRIMARY KEY, CitizenID INT, ServiceID INT, FeedbackDate DATE, Rating INT CHECK(Rating BETWEEN 1 AND 5), Comments TEXT, FOREIGN KEY (CitizenID) REFERENCES Citizens(CitizenID), FOREIGN KEY (ServiceID) REFERENCES Services(ServiceID));`: Creates the `Feedback` table with specified columns and constraints.
12. `SHOW TABLES;`: Lists all tables in the current database.
13. `DESCRIBE Citizens;`: Describes the structure of the `Citizens` table.
14. `DESCRIBE Services;`: Describes the structure of the `Services` table.
15. `DESCRIBE Appointments;`: Describes the structure of the `Appointments` table.
16. `DESCRIBE Employees;`: Describes the structure of the `Employees` table.
17. `DESCRIBE Feedback;`: Describes the structure of the `Feedback` table.
18. `INSERT INTO Citizens (CitizenID, FirstName, LastName, DateOfBirth, Gender, NationalID) VALUES (1, 'John', 'Doe', '1980-01-01', 'Male', '1234567890'), (2, 'Jane', 'Smith', '1990-02-02', 'Female', '0987654321'), (3, 'Alice', 'Johnson', '1985-03-03', 'Female', '1122334455'), (4, 'Bob', 'Brown', '1975-04-04', 'Male', '6677889900'), (5, 'Charlie', 'Davis', '2000-05-05', 'Male', '3344556677');`: Inserts multiple records into the `Citizens` table.
19. `INSERT INTO Services (ServiceID, ServiceName, Description, Fee, DurationMinutes) VALUES (1, 'Passport Application', 'Application for a new passport', 100.00, 30), (2, 'ID Renewal', 'Renewal of national ID', 50.00, 20), (3, 'Birth Certificate', 'Issuance of birth certificate', 20.00, 15), (4, 'Marriage Certificate', 'Issuance of marriage certificate', 30.00, 25), (5, 'Driver's License', 'Application for driver's license', 70.00, 45);`: Inserts multiple records into the `Services` table.
20. `INSERT INTO Appointments (AppointmentID, CitizenID, ServiceID, AppointmentDate, Status) VALUES (1, 1, 1, '2025-03-10', 'Completed'), (2, 2, 2, '2025-03-11', 'Pending'), (3, 3, 3, '2025-03-12', 'Cancelled'), (4, 4, 4, '2025-03-13', 'Completed'), (5, 5, 5, '2025-03-14', 'Pending');`: Inserts multiple records into the `Appointments` table.
21. `INSERT INTO Employees (EmployeeID, FirstName, LastName, Role, HireDate, Salary) VALUES`: Inserts multiple records into the `Employees` table (incomplete in the provided commands).
22. `SELECT * FROM Citizens;`: Selects and displays all records from the `Citizens` table.
23. `SELECT * FROM Services;`: Selects and displays all records from the `Services` table.
24. `INSERT INTO Services (ServiceID, ServiceName, Description, Fee, DurationMinutes) VALUES (6, 'New Service', 'Description', 25.00, 10);`: Inserts a new record into the `Services` table.
25. `DELETE FROM Citizens;`: Attempts to delete all records from the `Citizens` table, but fails due to foreign key constraints.
