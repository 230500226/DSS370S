Creating a Markdown file containing all possible MySQL commands with explanations and examples would be extensive. Instead, I'll provide a structured list of common MySQL commands with explanations and examples. You can add more commands as needed.

Here's a sample Markdown file:

```markdown
# MySQL Commands Cheat Sheet

## Connecting to MySQL
### Command
```sh
mysql -u [username] -p
```
### Explanation
Connect to the MySQL server as the specified user. You will be prompted for the password.
### Example
```sh
mysql -u root -p
```

## Creating a Database
### Command
```sql
CREATE DATABASE [database_name];
```
### Explanation
Creates a new database with the specified name.
### Example
```sql
CREATE DATABASE my_database;
```

## Dropping a Database
### Command
```sql
DROP DATABASE [database_name];
```
### Explanation
Deletes the specified database and all of its data.
### Example
```sql
DROP DATABASE my_database;
```

## Selecting a Database
### Command
```sql
USE [database_name];
```
### Explanation
Selects the specified database for subsequent operations.
### Example
```sql
USE my_database;
```

## Creating a Table
### Command
```sql
CREATE TABLE [table_name] (
    column1 datatype,
    column2 datatype,
    ...
);
```
### Explanation
Creates a new table with the specified columns and data types.
### Example
```sql
CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    username VARCHAR(50),
    email VARCHAR(100)
);
```

## Dropping a Table
### Command
```sql
DROP TABLE [table_name];
```
### Explanation
Deletes the specified table and all of its data.
### Example
```sql
DROP TABLE users;
```

## Inserting Data into a Table
### Command
```sql
INSERT INTO [table_name] (column1, column2, ...)
VALUES (value1, value2, ...);
```
### Explanation
Inserts a new row into the specified table with the given values.
### Example
```sql
INSERT INTO users (username, email)
VALUES ('john_doe', 'john@example.com');
```

## Selecting Data from a Table
### Command
```sql
SELECT column1, column2, ...
FROM [table_name]
WHERE condition;
```
### Explanation
Selects data from the specified columns in the table, optionally filtering by a condition.
### Example
```sql
SELECT username, email
FROM users
WHERE id = 1;
```

## Updating Data in a Table
### Command
```sql
UPDATE [table_name]
SET column1 = value1, column2 = value2, ...
WHERE condition;
```
### Explanation
Updates the specified columns with new values for rows matching the condition.
### Example
```sql
UPDATE users
SET email = 'john_new@example.com'
WHERE id = 1;
```

## Deleting Data from a Table
### Command
```sql
DELETE FROM [table_name]
WHERE condition;
```
### Explanation
Deletes rows from the specified table that match the condition.
### Example
```sql
DELETE FROM users
WHERE id = 1;
```

## Creating an Index
### Command
```sql
CREATE INDEX [index_name]
ON [table_name] (column1, column2, ...);
```
### Explanation
Creates an index on the specified columns to improve query performance.
### Example
```sql
CREATE INDEX idx_users_username
ON users (username);
```

## Dropping an Index
### Command
```sql
DROP INDEX [index_name] ON [table_name];
```
### Explanation
Deletes the specified index from the table.
### Example
```sql
DROP INDEX idx_users_username ON users;
```

## Joining Tables
### Command
```sql
SELECT columns
FROM table1
JOIN table2
ON table1.column = table2.column;
```
### Explanation
Combines rows from two or more tables based on a related column between them.
### Example
```sql
SELECT users.username, orders.order_date
FROM users
JOIN orders
ON users.id = orders.user_id;
```

## Granting Privileges
### Command
```sql
GRANT ALL PRIVILEGES ON [database_name].* TO '[username]'@'localhost' IDENTIFIED BY '[password]';
```
### Explanation
Grants the specified privileges to a user for the specified database.
### Example
```sql
GRANT ALL PRIVILEGES ON my_database.* TO 'john'@'localhost' IDENTIFIED BY 'password';
```

## Revoking Privileges
### Command
```sql
REVOKE ALL PRIVILEGES ON [database_name].* FROM '[username]'@'localhost';
```
### Explanation
Revokes the specified privileges from a user for the specified database.
### Example
```sql
REVOKE ALL PRIVILEGES ON my_database.* FROM 'john'@'localhost';
```

## Showing Databases
### Command
```sql
SHOW DATABASES;
```
### Explanation
Lists all databases on the MySQL server.
### Example
```sql
SHOW DATABASES;
```

## Showing Tables
### Command
```sql
SHOW TABLES;
```
### Explanation
Lists all tables in the selected database.
### Example
```sql
SHOW TABLES;
```

## Describing a Table
### Command
```sql
DESCRIBE [table_name];
```
### Explanation
Shows the structure of the specified table.
### Example
```sql
DESCRIBE users;
```

## Backup a Database
### Command
```sh
mysqldump -u [username] -p [database_name] > [backup_file].sql
```
### Explanation
Creates a backup of the specified database and saves it to a file.
### Example
```sh
mysqldump -u root -p my_database > my_database_backup.sql
```

## Restore a Database
### Command
```sh
mysql -u [username] -p [database_name] < [backup_file].sql
```
### Explanation
Restores the specified database from a backup file.
### Example
```sh
mysql -u root -p my_database < my_database_backup.sql
```

This Markdown file provides a good starting point for common MySQL commands. Feel free to expand it with additional commands and examples as needed.
```

You can save this content in a `.md` file, such as `mysql_commands_cheat_sheet.md`. This file can be used as a reference for common MySQL commands, their explanations, and examples.