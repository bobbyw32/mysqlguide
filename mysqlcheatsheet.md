How to log in to mysql from terminal:
    -ssh user@ipaddress -p port
    -mysql -u username(root) -p
    - enter password

How to show all users:
    -select user FROM user;
    -show current user - select user();

Privileges:
    granting users to database and all tables
        - grant all privileges on testdb.* to 'username'@'localhost';
    
    granting users to db and single table
        -grant all privileges on testdb.books to 'username'@'localhost';

    granting read access only
        - grant select on testdb.books to 'username'@'localhost';
    
    revoke privileges:
        - revoke all privileges, grant option from 'username';

Show, delete, create, select Databases:
    Show: show databases;
    Delete: drop database testdb;
    Create: create database testdb;
    Select: use testdb;

Creat Table:

CREATE TABLE renter (
renterID INT NOT NULL auto_increment,
fullName VARCHAR(50) NOT NULL,
phone VARCHAR(15) NOT NULL,
address VARCHAR(50) NOT NULL,
email VARCHAR(50) NOT NULL,
PRIMARY KEY (renterID)
);

Show, delete, drop tables:
    Show: select * from renter
    Delete: truncate table renter;
    Drop: drop table renter;

Insert Row and Record:
    INSERT INTO renter (name, birth_date, phone)
    VALUES ('Person Name', '1987-11-15', '555-555-5555');

Select with where clause:
    SELECT * FROM tablename
    WHERE salary > 10000;

Select with where clause with range:
    select * from tablename
    where age between 19 and 30;

Delete single row:
    delete from 'renter' where 'renterID' = 2;

Update a row:
    UPDATE inventory
    SET availability = 0
    WHERE inventoryID = 5;

Add new column and modify:
    alter table inventory
    add availability boolean not null default 1;

Order by:
    Ascending:
    SELECT * FROM employees 
    ORDER BY emp_name ASC;

    Descending:
    SELECT * FROM employees 
    ORDER BY salary DESC;

    Multiple rows:
    SELECT * FROM employees 
    ORDER BY first_name, last_name;

    Distinct - generate list skipping duplicate entries
    SELECT DISTINCT city FROM customers;

Concatenate Columns:
    Using customerName for first column, concat Address, PostalCode, and City to create column Address using data from table Customers.

    SELECT customerName, CONCAT(Address, " " , PostalCode, " ", City) AS Address
    FROM Customers;


How to select distinct rows:
    To select a specific row based on an id or name in the renter table.
        SELECT * FROM renter WHERE renterID = 2;
        SELECT * FROM renter WHERE fullName = 'joe smith';

How to use LIKE to search:
    LIKE operator used in a WHERE clause to search for pattern.

        SELECT column1, column2
        FROM table_name
        WHERE columnA like pattern

        Pattern Examples:
            'a%' finds any value that starts with "a"
            '%a' values that end with "a"
            '%or%' values that have "or" in any position
            '_r%' values that have "r" in second position
            'a_%' values that start with "a" and are at least 2 char in length
                - add more _ to add char
            'a%o' values that start with "a" and ends with "o"

How to select using IN:
    SELECT *        (or column_name)
    FROM table_name
    WHERE column_name IN (value1, value2);

    Can also use NOT IN


How to create Index:
    Creates an index on a table, allows duplicate values

    CREATE INDEX index_name
    ON table_name (column1, column2);

    UNIQUE INDEX does not allow duplicate values

    CREATE UNIQUE INDEX index_name
    ON table_name (column1, column2);

    DROP INDEX is used to delete an index

    DROP INDEX index_name ON table_name;


    Two tables with a one to many relationship with Primary and Foreign keys:

    Category table has individual categories of item and there may be many inventory items of that category but each inventory item only has one category.


    CREATE TABLE category (
        catID varchar(55),
        primary key (catID)
    );



    CREATE TABLE inventory (
        inventoryID INT NOT NULL auto_increment,
        invValue int,
        invSize varchar(5) NOT NULL,
        invCost int,
        catID varchar(55),
        primary key (inventoryID),
        foreign key (catID) references category (catID)
    );


How to use INNER JOIN:

    INNER JOIN selects records that have matching values in both tables. INNER JOIN selects all rows from both tables as long as there is a match, if there is not a match then that record is not selected.

        SELECT table1.column_name1
        FROM table1
        INNER JOIN table2
        ON table1.column_name2 = table2.column_name2;

JOIN multiple tables:

    Works similarily as inner join but uses another INNER JOIN statement.

        SELECT Orders.OrderID, Customers.CustomerName, Shippers.ShipperName
        FROM ((Orders
        INNER JOIN Customers ON Orders.CustomerID = Customers.CustomerID)
        INNER JOIN Shippers ON Orders.ShipperID = Shippers.ShipperID);