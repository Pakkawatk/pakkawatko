Data Definition Language (DDL)
Create
Alter
Drop
Data Manipulation Language (DML)
SELECT, INSERT, UPDATE, DELETE
Data Control Language (DCL)
GRANT, REVOKE

```

CREATE DATABASE database_name;
SHOW DATABASES;
USE database_name;
DROP DATABASE database_name ;
DROP TABLE table_name;

```


```
# Add column
ALTER TABLE table_name 
ADD col_name datatype; 
```
```
# Change data type
ALTER TABLE table_name 
MODIFY COLUMN col_name datatype; 
```

```
# Add constraint
ALTER TABLE table_name 
MODIFY col_name datatype CONSTRAINT; 
```
```
# Drop Column
ALTER TABLE table_name 
DROP COLUMN col_name; 
```
```
# Delete the data inside a table, but not the table itself
TRUNCATE TABLE table_name ;
```

```
LOAD DATA LOCAL INFILE '[path][fileneme]' INTO TABLE table_name;
```

