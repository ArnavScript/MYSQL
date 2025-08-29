STRUCTURE QUERY LANGUAGE(SQL)

1. SQL: Structured Query Language, used to access and manipulate data.
2. SQL used CRUD operations to communicate with DB.
    1. CREATE - execute INSERT statements to insert new tuple into the relation.
    2. READ - Read data already in the relations.
    3. UPDATE - Modify already inserted data in the relation.
    4. DELETE - Delete specific data point/tuple/row or multiple rows.
3. SQL is not DB, is a query language.
4. What is RDBMS? (Relational Database Management System)
   Software that enable us to implement designed relational model.
   e.g., MySQL, MS SQL, Oracle, IBM etc.
5. Table/Relation is the simplest form of data storage object in R-DB.
4. MySQL is open-source RDBMS, and it uses SQL for all CRUD operations
5. MySQL used client-server model, where client is CLI or frontend that used services provided by MySQL server.
6. Difference between SQL and MySQL
   SQL is Structured Query language used to perform CRUD operations in R-DB, while MySQL is a RDBMS used tostore, manage and administrate DB (provided by itself) using SQL.
7. SQL DATA TYPES (Ref: https://www.w3schools.com/sql/sql_datatypes.asp)
    In SQL DB, data is stored in the form of tables.
    Data can be of different types, like INT, CHAR etc.

8. DATATYPE Description--


CHAR          string(0-255), string with size = (0, 255], e.g.,CHAR(251)
VARCHAR       string(0-255)
TINYTEXT      String(0-255)
TEXT          string(0-65535)
BLOB          string(0-65535)
MEDIUMTEXT    string(0-16777215)
MEDIUMBLOB    string(0-16777215)
LONGTEXT      string(0-4294967295)
LONGBLOB      string(0-4294967295)
TINYINT       integer(-128 to 127)
SMALLINT      integer(-32768 to 32767)
MEDIUMINT     integer(-8388608 to 8388607)
INT           integer(-2147483648 to 2147483647)
BIGINT        integer (-9223372036854775808 to 9223372036854775807)
FLOAT         Decimal with precision to 23 digits
DOUBLE        Decimal with 24 to 53 digits

10. Size: TINY < SMALL < MEDIUM < INT < BIGINT.
11. Variable length Data types e.g., VARCHAR, are better to use as they occupy space  equal    the   actual data size.
12. Values can also be unsigned e.g., INT UNSIGNED.
13. Types of SQL commands:
    DDL (data definition language): defining relation schema.
    1. CREATE: create table, DB, view.
    2. ALTER TABLE: modification in table structure. e.g, change column datatype or add/remove     columns.
    3. DROP: delete table, DB, view.
    4. TRUNCATE: remove all the tuples from the table.
    5. RENAME: rename DB name, table name, column name etc.

    DRL/DQL (data retrieval language / data query language):
     retrieve data from the tables.
    1. SELECT
    
    DML (data modification language):
     use to perform modifications in the DB
    1. INSERT: insert data into a relation
    2. UPDATE: update relation data.
    3. DELETE: delete row(s) from the relation.

    DCL (Data Control language):
    grant or revoke authorities from user.
    1. GRANT: access privileges to the DB
    2. REVOKE: revoke user access privileges.
    
    TCL (Transaction control language):
    to manage transactions done in the DB
    1. START TRANSACTION: begin a transaction
    2. COMMIT: apply all the changes and end transaction
    3. ROLLBACK: discard changes and end transaction
    4. SAVEPOINT: checkout within the group of transactions in which to rollback.
 

MANAGING DB (DDL)

    Creation of DB
    
    1. CREATE DATABASE IF NOT EXISTS db-name;
    2. USE db-name; //need to execute to choose on which DB CREATE TABLE etc commands will be executed.
     //make switching between DBs possible.
    3. DROP DATABASE IF EXISTS db-name; //dropping database.
    4. SHOW DATABASES; //list all the DBs in the server. 
    5. SHOW TABLES; //list tables in the selected DB.

DATA RETRIEVAL LANGUAGE (DRL)

    1. Syntax: SELECT <set of column names> FROM <table_name>;
    
    2. Order of execution from RIGHT to LEFT.
       Q. Can we use SELECT keyword without using FROM clause?
          Yes, using DUAL Tables.
          Dual tables are dummy tables created by MySQL, help users to do certain obvious actions without referring to user defined tables.
          e.g., SELECT 55 + 11;
                SELECT now();
                SELECT ucase(); etc.
                
    3. WHERE
       Reduce rows based on given conditions.
       E.g., SELECT * FROM customer WHERE age > 18;
       
    4. BETWEEN
       SELECT * FROM customer WHERE age between 0 AND 100;
       In the above e.g., 0 and 100 are inclusive.
       
    5. IN
       Reduces OR conditions;
       e.g., SELECT * FROM officers WHERE officer_name IN ('Lakshay', ‘Maharana Pratap',‘Deepika’); 
       
    6. AND/OR/NOT
       AND: WHERE cond1 AND cond2
       OR: WHERE cond1 OR cond2
       NOT: WHERE col_name NOT IN (1,2,3,4);
       
    7. IS NULL
       e.g., SELECT * FROM customer WHERE prime_status is NULL;
       
    8. Pattern Searching / Wildcard (‘%’, ‘_’)
       ‘%’, any number of character from 0 to n. Similar to ‘*’ asterisk in regex.
       ‘_’, only one character.
       SELECT * FROM customer WHERE name LIKE ‘%p_’;
       
    9. ORDER BY
       Sorting the data retrieved using WHERE clause.
       ORDER BY <column-name> DESC;
       DESC = Descending and ASC = Ascending
       e.g., SELECT * FROM customer ORDER BY name DESC;
       
    10. GROUP BY
       GROUP BY Clause is used to collect data from multiple records and group the result by one or more column. It is generally used in a SELECT statement.
       Groups into category based on column given.
       SELECT c1, c2, c3 FROM sample_table WHERE cond GROUP BY c1, c2, c3.
       All the column names mentioned after SELECT statement shall be repeated in GROUP BY, in order to successfully execute the query.
       Used with aggregation functions to perform various actions.
       1. COUNT()
       2. SUM()
       3. AVG()
       4. MIN()
       5. MAX()
       
    11. DISTINCT
        Find distinct values in the table.
        SELECT DISTINCT(col_name) FROM table_name;
        GROUP BY can also be used for the same
        “Select col_name from table GROUP BY col_name;” same output as above DISTINCT query

    12. GROUP BY HAVING
       Out of the categories made by GROUP BY, we would like to know only particular thing (cond).
       Similar to WHERE.
       Select COUNT(cust_id), country from customer GROUP BY country HAVING COUNT(cust_id) > 50;

       WHERE vs HAVING
      1. Both have same function of filtering the row base on certain conditions.
      2. WHERE clause is used to filter the rows from the table based on specified condition
      3. HAVING clause is used to filter the rows from the groups based on the specified condition.
      4. HAVING is used after GROUP BY while WHERE is used before GROUP BY clause.
      5. If you are using HAVING, GROUP BY is necessary.
      6. WHERE can be used with SELECT, UPDATE & DELETE keywords while GROUP BY used with SELECT.


CONSTRAINTS (DDL)

    1. Primary Key
       PK is not null, unique and only one per table.

    2. Foreign Key
       FK refers to PK of other table.
       Each relation can having any number of FK.
       
 EXAMPLE--
 
    CREATE TABLE ORDER (
    id INT PRIMARY KEY,
    delivery_date DATE,
    order_placed_date DATE,
    cust_id INT,
    FOREIGN KEY (cust_id) REFERENCES customer(id)
    );

    3. UNIQUE
        Unique, can be null, table can have multiple unique attributes.
        
        CREATE TABLE customer (
    email VARCHAR(1024) UNIQUE,  
    );

    4. CHECK
    CREATE TABLE customer (  
    CONSTRAINT age_check CHECK (age > 12), 
     );
   
    “age_check”, can also avoid this, MySQL generates name of constraint automatically.
    
    5. DEFAULT
    Set default value of the column.
    CREATE TABLE account (
    saving-rate DOUBLE NOT NULL DEFAULT 4.25,
     );
    An attribute can be PK and FK both in a table.


ALTER OPERATIONS -

     Changes schema 
     1. ADD
     Add new column.
     ALTER TABLE table_name ADD new_col_name datatype ADD new_col_name_2 datatype;
     e.g., ALTER TABLE customer ADD age INT NOT NULL;

     2. MODIFY
     Change datatype of an attribute.
     ALTER TABLE table-name MODIFY col-name col-datatype;
     E.g., VARCHAR TO CHAR
     ALTER TABLE customer MODIFY name CHAR(1024);

     3. CHANGE COLUMN
     Rename column name.
     ALTER TABLE table-name CHANGE COLUMN old-col-name new-col-name new-col-datatype;
     e.g., ALTER TABLE customer CHANGE COLUMN name customer-name VARCHAR(1024);

     4. DROP COLUMN
     Drop a column completely.
     ALTER TABLE table-name DROP COLUMN col-name;
     e.g., ALTER TABLE customer DROP COLUMN middle-name;

     5. RENAME
     Rename table name itself.
     ALTER TABLE table-name RENAME TO new-table-name;
     e.g., ALTER TABLE customer RENAME TO customer-details;


DATA MANIPULATION LANGUAGE (DML)-

1. INSERT
    INSERT INTO table-name(col1, col2, col3) VALUES (v1, v2, v3), (val1, val2, val3);
   
3. UPDATE
   UPDATE table-name SET col1 = 1, col2 = ‘abc’ WHERE id = 1;
   
2. Update multiple rows e.g.,
   UPDATE student SET standard = standard + 1;
   
4. ON UPDATE CASCADE
    Can be added to the table while creating constraints. Suppose there is a situation where we have two tables such that primary key of one table is the foreign key for another table. if we update the primary key of the first table then using the ON UPDATE CASCADE foreign key of the second table automatically get updated.
   
5. DELETE
   DELETE FROM table-name WHERE id = 1;
   DELETE FROM table-name; //all rows will be deleted.
   DELETE CASCADE - (to overcome DELETE constraint of Referential constraints)
   What would happen to child entry if parent table’s entry is deleted?
   CREATE TABLE ORDER (
     order_id int PRIMARY KEY,
     delivery_date DATE,
     cust_id INT,
     FOREIGN KEY(cust_id) REFERENCES customer(id) ON DELETE CASCADE
 );

6. ON DELETE NULL - (can FK have null values?)
    CREATE TABLE ORDER (
    order_id int PRIMARY KEY,
    delivery_date DATE,
    cust_id INT,
    FOREIGN KEY(cust_id) REFERENCES customer(id) ON DELETE SET NULL
   );

7. REPLACE
   Primarily used for already present tuple in a table.
   As UPDATE, using REPLACE with the help of WHERE clause in PK, then that row will be replaced.
   As INSERT, if there is no duplicate data new tuple will be inserted.
   REPLACE INTO student (id, class) VALUES(4, 3);
   REPLACE INTO table SET col1 = val1, col2 = val2;



JOINING TABLES-

   All RDBMS are relational in nature, we refer to other tables to get meaningful outcomes.
   FK are used to do reference to other table.
   
  1. INNER JOIN
    Returns a resultant table that has matching values from both the tables or all the tables.
    SELECT column-list FROM table1 INNER JOIN table2 ON condition1
    INNER JOIN table3 ON condition2;
    Alias in MySQL (AS)
    Aliases in MySQL is used to give a temporary name to a table or a column in a table for the purpose of a particular query. It works as a nickname for expressing the tables or column names. It makes the query short and neat.
   SELECT col_name AS alias_name FROM table_name;
   SELECT col_name1, col_name2,... FROM table_name AS alias_name;

2. OUTER JOIN --

   1. LEFT JOIN
   This returns a resulting table that all the data from left table and the matched data from the right table.
   SELECT columns FROM table LEFT JOIN table2 ON Join_Condition;

   2. RIGHT JOIN
   This returns a resulting table that all the data from right table and the matched data from the left table.
   SELECT columns FROM table RIGHT JOIN table2 ON join_cond;

   3. FULL JOIN
   This returns a resulting table that contains all data when there is a match on left or right table data.
   Emulated in MySQL using LEFT and RIGHT JOIN.
   LEFT JOIN UNION RIGHT JOIN.
   SELECT columns FROM table1 as t1 LEFT JOIN table2 as t2 ON t1.id = t2.id
   UNION
   SELECT columns FROM table1 as t1 RIGHT JOIN table2 as t2 ON t1.id = t2.id;
   UNION ALL, can also be used this will duplicate values as well while UNION gives unique values.

  4. CROSS JOIN
    This returns all the cartesian products of the data present in both tables. Hence, all possible variations are reflected in the output.
     Used rarely in practical purpose.
    Table-1 has 10 rows and table-2 has 5, then resultant would have 50 rows.
    SELECT column-lists FROM table1 CROSS JOIN table2;

  5. SELF JOIN
   1. It is used to get the output from a particular table when the same table is joined to itself.
   2. Used very less.
   3. Emulated using INNER JOIN.
   4. SELECT columns FROM table as t1 INNER JOIN table as t2 ON t1.id = t2.id;
   5. Join without using join keywords.
   6. SELECT * FROM table1, table2 WHERE condition;
      e.g., SELECT artist_name, album_name, year_recordedFROM artist, albumWHERE artist.id = album.artist_id   
   


SET OPERATIONS----

      Used to combine multiple select statements.
      Always gives distinct rows.
      
    1. UNION
       Combines two or more SELECT statements.
       SELECT * FROM table1
       UNION
       SELECT * FROM table2;
       Number of column, order of column must be same for table1 and table2.

    2. INTERSECT
      Returns common values of the tables.
      Emulated.
      SELECT DISTINCT column-list FROM table-1 INNER JOIN table-2 USING(join_cond);
      SELECT DISTINCT * FROM table1 INNER JOIN table2 ON USING(id);

    3. MINUS
      This operator returns the distinct row from the first table that does not occur in the second  table.
      Emulated.
      SELECT column_list FROM table1 LEFT JOIN table2 ON condition WHERE table2.column_name IS NULL;
      e.g., SELECT id FROM table-1 LEFT JOIN table-2 USING(id) WHERE table-2.id IS NULL;



    
SUB QUERIES----
   1. Outer query depends on inner query.
   2. Alternative to joins.
   3. Nested queries.
   4. SELECT column_list(s) FROM table_name WHERE column_name OPERATOR
      (SELECT column_list(s) FROM table_name [WHERE]);
   5. e.g., SELECT * FROM table1 WHERE col1 IN (SELECT col1 FROM table1);
   6. Sub queries exist mainly in 3 clauses
       1. Inside a WHERE clause.
       2. Inside a FROM clause.    
       3. Inside a SELECT clause.
   7. Subquery using FROM clause
      SELECT MAX(rating) FROM (SELECT * FROM movie WHERE country = ‘India’) as temp;
   8. Subquery using SELECT
      SELECT (SELECT column_list(s) FROM T_name WHERE condition), columnList(s) FROM T2_name WHERE   condition;
   9. Derived Subquery
      SELECT columnLists(s) FROM (SELECT columnLists(s) FROM table_name WHERE [condition]) as new_table_name;
   10. Co-related sub-queries
      With a normal nested subquery, the inner SELECT query runs first and executes once, returning values to be used by the main query. A correlated subquery, however, executes once for each candidate row considered by the outer query. In other words, the inner query is driven by the outer query




      MySQL VIEWS----
     1. A view is a database object that has no values. Its contents are based on the basetable.    It contains rows and columns similar to the real table.
     2. In MySQL, the View is a virtual table created by a query by joining one or more tables. It is operated similarly to the base table but does not contain any data of its own.
     3. The View and table have one main difference that the views are definitions built on top of other tables (or views). If any changes occur in the underlying table, the same changes reflected in the View also.
     4. CREATE VIEW view_name AS SELECT columns FROM tables [WHERE conditions];
     5. ALTER VIEW view_name AS SELECT columns FROM table WHERE conditions;
     6. DROP VIEW IF EXISTS view_name;
     7. CREATE VIEW Trainer AS SELECT c.course_name, c.trainer, t.email FROM courses c, contact t WHERE c.id = t.id; (View using Join clause).
     NOTE: We can also import/export table schema from files (.csv or json).




