# SQL Homework

## SQL Tutorial
### SELECT
```{.sql}
Select all the different values
SELECT DISTINCT Country FROM Customers;
```

### WHERE
```{.sql}
Where the City column is NOT the value "Berlin".
Select * from customers where city <> 'Berlin';
```

### ORDER BY
```{.sql}
Sort the result reversed alphabetically by the column City.
SELECT * FROM Customers Order by city desc;

Sort the result alphabetically, first by the column Country, then, by the column City.
SELECT * FROM Customers order by country, city;
```

### INSERT
```{.sql}
INSERT INTO table_name
VALUES (value1, value2, value3, ...);

특정 col에만 삽입할 경우
INSERT INTO table_name (column1, column2, column3, ...)
VALUES (value1, value2, value3, ...);
```

### NULL
IS, IS NOT을 사용함
```{.sql}
SELECT column_names
FROM table_name
WHERE column_name IS NULL;

SELECT column_names
FROM table_name
WHERE column_name IS NOT NULL;
```

### UPDATE
```{.sql}
UPDATE table_name
SET column1 = value1, column2 = value2, ...
WHERE condition; => 적지 않을 경우 모든 데이터가 바뀌므로 빼먹지 않도록 주의
```

### DELETE
```{.sql}
DELETE FROM table_name
WHERE condition; => update와 마찬가지로 빼먹지 않도록 주의
```

### LIKE, WILDCARDS
* % - The percent sign represents zero, one, or multiple characters
* _ - The underscore represents a single character
    - WHERE CustomerName LIKE 'a%'	Finds any values that start with "a"
    - WHERE CustomerName LIKE '%or%'	Finds any values that have "or" in any position
    - WHERE CustomerName LIKE '_r%'	Finds any values that have "r" in the second position

```{.sql}
Select all records where the value of the City column does NOT start with the letter "a".
SELECT * FROM Customers where city not like 'a%';

Select all records where the first letter of the City is an "a" or a "b" or a "c".
SELECT * FROM Customers WHERE City LIKE '[abc]%';

Select all records where the first letter of the City is NOT an "a" or a "b" or a "c".
SELECT * FROM Customers WHERE City LIKE '[!abc]%';
```
### IN
```{.sql}
SELECT * FROM Customers
WHERE Country IN ('Germany', 'France', 'UK');

SELECT * FROM Customers
WHERE Country NOT IN ('Germany', 'France', 'UK');
```

### ALIAS
```{.sql}
SELECT column_name AS alias_name
FROM table_name;

SELECT column_name(s)
FROM table_name AS alias_name;
```

### JOIN
```{.sql}
SELECT column_name(s)
FROM table1
INNER JOIN table2 ON table1.column_name = table2.column_name;

SELECT column_name(s)
FROM table1
LEFT JOIN table2 ON table1.column_name = table2.column_name;

SELECT column_name(s)
FROM table1
RIGHT JOIN table2 ON table1.column_name = table2.column_name;

SELECT column_name(s)
FROM table1
FULL OUTER JOIN table2 ON table1.column_name = table2.column_name;
```
<img src="https://user-images.githubusercontent.com/10782878/46259512-5cfefd00-c515-11e8-86da-0921b7dfb62e.png" width="500" height="200"></img>

#### SELF JOIN
```{.sql}
SELECT A.CustomerName AS CustomerName1, B.CustomerName AS CustomerName2, A.City
FROM Customers A, Customers B
WHERE A.CustomerID <> B.CustomerID
AND A.City = B.City 
ORDER BY A.City;
```

### UNION
```{.sql}
Only distinct value, 자동으로 정렬
SELECT City FROM Customers
UNION
SELECT City FROM Suppliers
ORDER BY City;  => 생략 가능

duplicate values also
SELECT City FROM Customers
UNION ALL
SELECT City FROM Suppliers
ORDER BY City;
```

### GROUP BY
```{.sql}
SELECT COUNT(CustomerID), Country
FROM Customers
GROUP BY Country
ORDER BY COUNT(CustomerID) DESC;
```

### HAVING
```{.sql}
The HAVING clause was added to SQL because the WHERE keyword could not be used with aggregate functions.

SELECT column_name(s)
FROM table_name
WHERE condition
GROUP BY column_name(s)
HAVING condition
ORDER BY column_name(s);

SELECT Employees.LastName, COUNT(Orders.OrderID) AS NumberOfOrders
FROM Orders
INNER JOIN Employees ON Orders.EmployeeID = Employees.EmployeeID
WHERE LastName = 'Davolio' OR LastName = 'Fuller'
GROUP BY LastName
HAVING COUNT(Orders.OrderID) > 25;
```

### EXISTS
```{.sql}
SELECT SupplierName
FROM Suppliers
WHERE EXISTS (SELECT ProductName FROM Products WHERE SupplierId = Suppliers.supplierId AND Price < 20);
```

## SQL Database
### CREATE
```{.sql}
이미 존재하는 테이블을 이용해서 테이블 생성하기
CREATE TABLE new_table_name AS
    SELECT column1, column2,...
    FROM existing_table_name
    WHERE ....;
```
### DROP
```{.sql}
DROP TABLE table_name;

테이블을 지우지 않고 데이터만 지우고 싶을 때
TRUNCATE TABLE table_name;
```
### ALTER
```{.sql}
ALTER TABLE table_name
ADD column_name datatype;

ALTER TABLE table_name
DROP COLUMN column_name;

ALTER TABLE table_name
MODIFY COLUMN column_name datatype;
```
### CONSTRAINTS
```{.sql}
CREATE TABLE table_name (
    column1 datatype constraint,
    column2 datatype constraint,
    ....
);
```
* NOT NULL - Ensures that a column cannot have a NULL value
* UNIQUE - Ensures that all values in a column are different
* PRIMARY KEY - A combination of a NOT NULL and UNIQUE. Uniquely identifies each row in a table
* FOREIGN KEY - Uniquely identifies a row/record in another table
* CHECK - Ensures that all values in a column satisfies a specific condition
* DEFAULT - Sets a default value for a column when no value is specified
* INDEX - Used to create and retrieve data from the database very quickly

### UNIQUE
```{.sql}
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
```
### PRIMARY KEY
```{.sql}
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
```
### FOREIGN KEY
```{.sql}
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
```
### CHECK
```{.sql}
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
```
### DEFAULT
```{.sql}
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
```
### INDEX
```{.sql}
CREATE (UNIQUE) INDEX idx_pname
ON Persons (LastName, FirstName);

ALTER TABLE Persons
DROP INDEX UC_Person;
```
### AUTO INCREMENT
```{.sql}
CREATE TABLE Persons (
    ID int NOT NULL AUTO_INCREMENT,
    PRIMARY KEY (ID)
);

ALTER TABLE Persons AUTO_INCREMENT=100;
```
### DATE
* DATE - format YYYY-MM-DD
* DATETIME - format: YYYY-MM-DD HH:MI:SS
* TIMESTAMP - format: YYYY-MM-DD HH:MI:SS
* YEAR - format YYYY or YY
