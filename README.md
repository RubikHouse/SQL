# SQL Homework
<div>
<table class="w3-table-all notranslate">
  <tr>
    <th>CustomerID</th>
    <th>CustomerName</th>
    <th>ContactName</th>
    <th>Address</th>
    <th>City</th>
    <th>PostalCode</th>
    <th>Country</th>
  </tr>
  <tr>
    <td>1<br><br></td>
    <td>Alfreds Futterkiste</td>
    <td>Maria Anders</td>
    <td>Obere Str. 57</td>
    <td>Berlin</td>
    <td>12209</td>
    <td>Germany</td>
  </tr>
  <tr>
    <td>2</td>
    <td>Ana Trujillo Emparedados y helados</td>
    <td>Ana Trujillo</td>
    <td>Avda. de la Constitución 2222</td>
    <td>México D.F.</td>
    <td>05021</td>
    <td>Mexico</td>
  </tr>
  <tr>
    <td>3</td>
    <td>Antonio Moreno Taquería</td>
    <td>Antonio Moreno</td>
    <td>Mataderos 2312</td>
    <td>México D.F.</td>
    <td>05023</td>
    <td>Mexico</td>
  </tr>
  <tr>
    <td>4<br><br></td>
    <td>Around the Horn</td>
    <td>Thomas Hardy</td>
    <td>120 Hanover Sq.</td>
    <td>London</td>
    <td>WA1 1DP</td>
    <td>UK</td>
  </tr>
  <tr>
    <td>5</td>
    <td>Berglunds snabbköp</td>
    <td>Christina Berglund</td>
    <td>Berguvsvägen 8</td>
    <td>Luleå</td>
    <td>S-958 22</td>
    <td>Sweden</td>
  </tr>
</table>
</div>

-----------------------

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

- [이한영](https://lhy.kr/)
