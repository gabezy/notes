<h2>What is a Database</h2>
<ol>
  <li> A structured set if computerized data with an accessible interface</li>
  <li>A collection of data</li>
  <li>A method for acessing nad manipulating that data</li>
</ol>
Jargion</br>

- Database Manager System (DBMS) -> PostgreSQL, Oracle Database, MySQL, SQLite

## MySQL vs SQL

### Structred Query Language (SQL)

Basically is the language we use to "talk" to our databases, like update, delete, create data.

```SQL
-- Find all users who are 18 or older
SELECT * FROM Users WHERE Age >= 18;
```

### MySQL

MySQL is a Relational Database Manager System (RDBMS), other examples of RDBMS are:

<ul>
  <li>SQLite</li>
  <li>PostgreSQL</li>
  <li>Oracle</li>
</ul>

and all use SQL.

### Creating a Database

```SQL
show databases; -- show all databease
CREATE DATABASE MyApp; -- create a database
DROP DATABASE MyApp; -- delete the database
USE MyApp; -- use the database
SELECT DATABASE() -- show the currently database
```

### Tables

Tables hold tge data (RDB). "A collection of related data held in a structured format within a database"

<h2>Table</h2>
<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>LastName</th>
      <th>Age</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Jonh</td>
      <td>Silva</td>
      <td>45</td>
    </tr>
    <tr>
      <td>Ned</td>
      <td>Flandres</td>
      <td>30</td>
    </tr>
    <tr>
      <td>Home</td>
      <td>Simpsons</td>
      <td>50</td>
    </tr>
  </tbody>
</table>

```SQL
    CREATE TABLE Users
    (
      Name VARCHAR(50),
      LastName VARCHAR(50),
      Age INT,
    );
```

<h2>Columns</h2>
<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>LastName</th>
      <th>Age</th>
    </tr>
  </thead>
</table>
<h2>Rows (the actual data)</h2>
<table>
<tbody>
    <tr>
      <td>Jonh</td>
      <td>Silva</td>
      <td>45</td>
    </tr>
    <tr>
      <td>Ned</td>
      <td>Flandres</td>
      <td>30</td>
    </tr>
    <tr>
      <td>Home</td>
      <td>Simpsons</td>
      <td>50</td>
    </tr>
  </tbody>
</table>

## Adding data to a table

```SQL
INSERT INTO Users (Name,lastname, Age)
VALUES ("Gabriel", "Toledo" 30);
```

## Date

"YYYY-MM-DD" format
