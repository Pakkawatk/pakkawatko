Data Definition Language (DDL)
Create
Alter
Drop
Data Manipulation Language (DML)
SELECT, INSERT, UPDATE, DELETE
Data Control Language (DCL)
GRANT, REVOKE

---

CREATE DATABASE database_name;
SHOW DATABASES;
USE database_name;
DROP DATABASE database_name ;

---

CREATE TABLE table_name (column1 datatype,column2 datatype,column3 datatype,....) ;
CREATE TABLE Persons (PersonID int,LastName varchar(255),FirstName varchar(255),Address varchar(255),) ;
CREATE TABLE new_table_name ASSELECT column1, column2, ...FROM existing_table_nameWHERE .... ;
CREATE TABLE TestTable ASSELECT customer_name, contactFROM customers ;
DROP TABLE table_name ;
The TRUNCATE TABLE statement is used to delete the data inside a table, but not the table itself
TRUNCATE TABLE table_name ;
ALTER TABLE table_nameADD column_name datatype ;
ALTER TABLE CustomersADD Email varchar(255 );
ALTER TABLE - DROP Column
ALTER TABLE table_nameDROP COLUMN column_name ;
ALTER TABLE - ALTER/MODIFY Column;
ALTER TABLE table_nameALTER COLUMN column_name datatype;
SQL Create Constraints
CREATE TABLE table_name (column1 datatype constraint,column2 datatype constraint,column3 datatype constraint,....);
The following constraints are commonly used in SQL:▪ NOT NULL - Ensures that a column cannot have a NULL value▪ UNIQUE - Ensures that all values in a column are different▪ PRIMARY KEY - A combination of a NOT NULL and UNIQUE. Uniquely identifies each row in a table▪ FOREIGN KEY - Prevents actions that would destroy links between tables▪ CHECK - Ensures that the values in a column satisfy a specific condition▪ DEFAULT - Sets a default value for a column if no value is specified▪ CREATE INDEX - Used to create and retrieve data from the database very quickly
SQL StatementsBig Data Engineering Program - CITE - DPU Page 18❑SQL NOT NULL on CREATE TABLEExample     CREATE TABLE Persons (ID int NOT NULL,LastName varchar(255) NOT NULL,FirstName varchar(255) NOT NULL,Age int) ;
CREATE TABLE Persons (ID int NOT NULL UNIQUE,LastName varchar(255) NOT NULL,FirstName varchar(255),Age int) ;
