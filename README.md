# SQL Homework

## SQL Tutorial
### Select
Select all the different values from the Country column in the Customers table.
SELECT DISTINCT Country FROM Customers;

### Where
Select all records where the City column is NOT the value "Berlin".
select * from customers where city <> 'Berlin';

### Order by
Select all records from the Customers table, sort the result reversed alphabetically by the column City.
SELECT * FROM Customers Order by city desc;

Select all records from the Customers table, sort the result alphabetically, first by the column Country, then, by the column City.
SELECT * FROM Customers order by country, city;

### Insert
Insert a new record in the Customers table.

INSERT INTO table_name
VALUES (value1, value2, value3, ...);

INSERT INTO table_name (column1, column2, column3, ...)
VALUES (value1, value2, value3, ...);

### NULL
It is not possible to test for NULL values with comparison operators, such as =, <, or <>.

SELECT column_names
FROM table_name
WHERE column_name IS NULL;

SELECT column_names
FROM table_name
WHERE column_name IS NOT NULL;

### Update
UPDATE table_name
SET column1 = value1, column2 = value2, ...
WHERE condition;

Be careful when updating records in a table! Notice the WHERE clause in the UPDATE statement. The WHERE clause specifies which record(s) that should be updated. If you omit the WHERE clause, all records in the table will be updated!

### Delete
DELETE FROM table_name
WHERE condition;

Be careful when deleting records in a table! Notice the WHERE clause in the DELETE statement. The WHERE clause specifies which record(s) should be deleted. If you omit the WHERE clause, all records in the table will be deleted!

 ### Like
% - The percent sign represents zero, one, or multiple characters
_ - The underscore represents a single character

WHERE CustomerName LIKE 'a%'	Finds any values that start with "a"
WHERE CustomerName LIKE '%or%'	Finds any values that have "or" in any position
WHERE CustomerName LIKE '_r%'	Finds any values that have "r" in the second position

Select all records where the value of the City column does NOT start with the letter "a".
SELECT * FROM Customers where city not like 'a%';

Select all records where the first letter of the City is an "a" or a "b" or a "c".
SELECT * FROM Customers WHERE City LIKE '[abc]%';

Select all records where the first letter of the City is NOT an "a" or a "b" or a "c".
SELECT * FROM Customers WHERE City LIKE '[!abc]%';

### In
SELECT * FROM Customers
WHERE Country IN ('Germany', 'France', 'UK');

SELECT * FROM Customers
WHERE Country NOT IN ('Germany', 'France', 'UK');

### Join

## SQL Database

### CREATE
이미 존재하는 테이블을 이용해서 테이블 생성하기
CREATE TABLE new_table_name AS
    SELECT column1, column2,...
    FROM existing_table_name
    WHERE ....;
### DROP
DROP TABLE table_name;

테이블을 지우지 않고 데이터만 지우고 싶을 때
TRUNCATE TABLE table_name;

### ALTER
ALTER TABLE table_name
ADD column_name datatype;

ALTER TABLE table_name
DROP COLUMN column_name;

ALTER TABLE table_name
MODIFY COLUMN column_name datatype;

### CONSTRAINTS
CREATE TABLE table_name (
    column1 datatype constraint,
    column2 datatype constraint,
    ....
);

* NOT NULL - Ensures that a column cannot have a NULL value
* UNIQUE - Ensures that all values in a column are different
* PRIMARY KEY - A combination of a NOT NULL and UNIQUE. Uniquely identifies each row in a table
* FOREIGN KEY - Uniquely identifies a row/record in another table
* CHECK - Ensures that all values in a column satisfies a specific condition
* DEFAULT - Sets a default value for a column when no value is specified
* INDEX - Used to create and retrieve data from the database very quickly

### UNIQUE
CREATE TABLE Persons (
    ID int NOT NULL,
    UNIQUE (ID)
);

CREATE TABLE Persons (
    ID int NOT NULL,
    LastName varchar(255) NOT NULL,
    CONSTRAINT UC_Person UNIQUE (ID,LastName)
);

ALTER TABLE Persons
ADD UNIQUE (ID);

ALTER TABLE Persons
ADD CONSTRAINT UC_Person UNIQUE (ID,LastName);

ALTER TABLE Persons
DROP INDEX UC_Person;

### PRIMARY KEY
CREATE TABLE Persons (
    ID int NOT NULL,
    PRIMARY KEY (ID)
);

CREATE TABLE Persons (
    ID int NOT NULL,
    LastName varchar(255) NOT NULL,
    CONSTRAINT PK_Person PRIMARY KEY (ID,LastName)
);

ALTER TABLE Persons
ADD PRIMARY KEY (ID);

ALTER TABLE Persons
ADD CONSTRAINT PK_Person PRIMARY KEY (ID,LastName);

ALTER TABLE Persons
DROP PRIMARY KEY;

### FOREIGN KEY
CREATE TABLE Orders (
    OrderID int NOT NULL,
    PersonID int,
    PRIMARY KEY (OrderID),
    FOREIGN KEY (PersonID) REFERENCES Persons(PersonID)
);

CREATE TABLE Orders (
    OrderID int NOT NULL,
    PersonID int,
    PRIMARY KEY (OrderID),
    CONSTRAINT FK_PersonOrder FOREIGN KEY (PersonID)
    REFERENCES Persons(PersonID)
);

ALTER TABLE Orders
ADD FOREIGN KEY (PersonID) REFERENCES Persons(PersonID);

ALTER TABLE Orders
ADD CONSTRAINT FK_PersonOrder
FOREIGN KEY (PersonID) REFERENCES Persons(PersonID);

ALTER TABLE Orders
DROP FOREIGN KEY FK_PersonOrder;

### CHECK
CREATE TABLE Persons (
    Age int,
    CHECK (Age>=18)
);

CREATE TABLE Persons (
    Age int,
    City varchar(255),
    CONSTRAINT CHK_Person CHECK (Age>=18 AND City='Sandnes')
);

ALTER TABLE Persons
ADD CHECK (Age>=18);

ALTER TABLE Persons
ADD CONSTRAINT CHK_PersonAge CHECK (Age>=18 AND City='Sandnes');

ALTER TABLE Persons
DROP CHECK CHK_PersonAge;

### DEFAULT
CREATE TABLE Persons (
    City varchar(255) DEFAULT 'Sandnes'
);

CREATE TABLE Orders (
    OrderDate date DEFAULT GETDATE()
);

ALTER TABLE Persons
ALTER City SET DEFAULT 'Sandnes';

ALTER TABLE Persons
ALTER City DROP DEFAULT;

### INDEX
CREATE (UNIQUE) INDEX idx_pname
ON Persons (LastName, FirstName);

ALTER TABLE Persons
DROP INDEX UC_Person;

### AUTO INCREMENT
CREATE TABLE Persons (
    ID int NOT NULL AUTO_INCREMENT,
    PRIMARY KEY (ID)
);

ALTER TABLE Persons AUTO_INCREMENT=100;

### Date
* DATE - format YYYY-MM-DD
* DATETIME - format: YYYY-MM-DD HH:MI:SS
* TIMESTAMP - format: YYYY-MM-DD HH:MI:SS
* YEAR - format YYYY or YY


- [이한영](https://lhy.kr/)
