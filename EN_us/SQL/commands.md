```SQL
SHOW TABLES; -- show all tables inside the database
SHOW COLUMNS FROM  Users;
DESC cats; -- samething that show columns

show databases; -- show all databease
CREATE DATABASE MyApp; -- create a database
DROP DATABASE MyApp; -- delete the database
USE MyApp; -- use the database
SELECT DATABASE() -- show the currently database

CREATE TABLE tablename
    (
      column_name data_type,
      column_name data_type,
    );

-- CRUD
  --CREATE
  INSERT INTO tableName (columnsNames) VALUES(data);
  --READ
  SELECT columnName FROM tableName WHERE conditional -- * for select all columns inside a table
  --UPDATE
  UPDATE tableName SET columnName='new data';
  --DELETE
  DELETE FROM tableName WHERE conditional;

-- Open a external sql file
source file_path.sql
```

## String function

```SQL
SELECT CONCAT('Hello', ' Wolrd');
SELECT CONCAT_WS(separator, string1, string2);
SELECT SUBSTR(string, startChar, length);
SELECT CONCAT(SUBSTR(author_fname, 1, 1),'.',SUBSTR(author_lname, 1, 1), '.') AS author_initials FROM books;

```

## Query Functions

```SQL
SELECT DISTINCT colunmName FROM tableName; -- RETURN ONLY UNIQUE VALUES
SELECT colunmName from tableName ORDER BY colunmName DESC;
SELECT book_id, title, released_year FROM books ORDER BY released_year LIMIT 5; -- LIMIT THE RETURN TO 5 ROWS
SELECT title FROM books WHERE title LIKE '%stories%'; -- %word% MEANS SERACH THE WORD ANYWHRE IN TITLE

```

## Aggregate Fuctions

```SQL
SELECT COUNT(*) FROM books; -- COUNT THE NUMBER OF ROWS IN A TABLE
SELECT COUNT(author_fname) FROM books; -- COUNT EVERY TIME A VALUE IS PRESENT IN THE author_fname COLUNM (DON'T COUNT NULL VALUE)
SELECT COUNT(DISTINCT author_fname) FROM books; -- COUNT ONLY UNIQUE VALUES
SELECT released_year, COUNT(*) AS quantity FROM books GROUP BY released_year ORDER BY quantity DESC;
SELECT title, CONCAT(author_fname, ' ', author_lname) AS author, pages FROM books WHERE pages = (SELECT MAX(pages) FROM books);

```

## MySQL Server commands

```Bash
sudo service mysql stop # server status
sudo service mysql start # start server
sudo service mysql stop # stop server
```

## Floating point numbers

```SQL
DECIMAL(5, 2); -- First arg is the total number's length and second agr is the length after the point -> 999.99
FLOAT; -- 4 bytes and 7 digit precision
DOUBLE;  -- 8 bytes and 17 digit precision
```

## Date & Time

```SQL
-- DATE -> YYYY-MM-DD Format
-- TIME -> HH:MM:SS Format
-- DATETIME -> YYYY-MM-DD HH:MM:SS format
SELECT CURDATE();
SELECT CURTIME();
SELECT NOW();
DATE_FORMAT(date, format);


CREATE TABLE captions (
  text VARCHAR(150),
  created_at DEFAULT CURRENT_TIMESTAMP,
  updated_at TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);

```
