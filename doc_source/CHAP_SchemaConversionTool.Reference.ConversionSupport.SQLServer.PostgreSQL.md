# Microsoft SQL Server to PostgreSQL Supported Schema Conversion<a name="CHAP_SchemaConversionTool.Reference.ConversionSupport.SQLServer.PostgreSQL"></a>

The following sections list the schema elements from a Microsoft SQL Server database and whether they are supported for automatic conversion to PostgreSQL using the AWS Schema Conversion Tool\. 

## Data Definition Language \(DDL\)<a name="w3ab1c37b9b7"></a>

### Naming Objects<a name="w3ab1c37b9b7b2"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  Schemas  |  Yes  |   | 
|  Tables, Columns  |  Yes  |   | 

### Statements<a name="w3ab1c37b9b7b4"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  ALTER INDEX  |  No  |      | 
|  ALTER PROCEDURE  |  No  |      | 
|  ALTER TRIGGER  |  No  |      | 
|  ALTER VIEW  |  No  |      | 
|  CREATE FUNCTION  |  Partial  |   Automatic migration of inline functions is not supported\. Default parameters specified for any function are skipped\.   | 
|  CREATE PROCEDURE  |  Yes  |   | 
|  CREATE SEQUENCE  |  Yes  |   | 
|  IDENTITY \(x,y\)  |  Yes  |   | 
|  TRUNCATE TABLE  |  Yes  |   | 
|  UPDATE STATISTICS  |  No  |      | 

### ALTER TABLE<a name="w3ab1c37b9b7b6"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  ADD   |  Yes  |   | 
|  ALTER COLUMN  |  No  |      | 
|  DROP COLUMN  |  No  |      | 
|  DROP CONSTRAINT   |  No  |      | 
|  ENABLE/DISABLE TRIGGER   |  Yes  |   | 

### CREATE INDEX<a name="w3ab1c37b9b7b8"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  CLUSTER option  |  Partial  |      | 
|  COLUMNSTORE index  |  Partial  |      | 
|  INCLUDE clause  |  Partial  |      | 
|  Other INDEX options  |  Partial  |      | 
|  SPATIAL index  |  Partial  |      | 
|  UNIQUE option  |  Yes  |   | 
|  XML index  |  Partial  |      | 

### CREATE TABLE<a name="w3ab1c37b9b7c10"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  Partitioned tables  |  Yes  |   | 
|  Regular tables  |  Yes  |   | 
|  Temporary tables   | Partial |      | 
|  Wide tables  |  Yes  |   | 

### CREATE TRIGGER<a name="w3ab1c37b9b7c12"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  FOR EACH STATEMENT Triggers  |  Partial  |      | 
|  INSTEAD OF Triggers  |  Partial  |      | 
|  Trigger event \(INSERT/UPDATE/DELETE \)  |  Partial  |      | 
|  Trigger time \(BEGORE/AFTER\)  |  Partial  |      | 

### CREATE VIEW<a name="w3ab1c37b9b7c14"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  CREATE VIEW  |  Yes  |   | 
|  Updatable Views  |  Yes  |   | 
|  VIEW  |  Yes  |   | 

### DROP Statements<a name="w3ab1c37b9b7c16"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  DROP TABLE  |  Yes  |   | 
|  DROP VIEW  |  Yes  |   | 
|  Other types of objects  |  Yes  |   | 

## Data Manipulation Language \(DML\)<a name="w3ab1c37b9b9"></a>

### Clause for Statements<a name="w3ab1c37b9b9b2"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  Join Hints  |  No  |      | 
|  Query Hints  |  No  |      | 
|  Table Hint  |  No  |      | 
|  WHERE  |  Yes  |   | 

### Joins<a name="w3ab1c37b9b9b4"></a>

#### Cross Joins<a name="w3ab1c37b9b9b4b2"></a>

##### <a name="w3ab1c37b9b9b4b2b2"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  Cross join  |  Yes  |   | 
|  Cross join with condition  |  Yes  |   | 

#### Inner Joins<a name="w3ab1c37b9b9b4b4"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  Inner Joins  |  Yes  |   | 

#### Outer Joins<a name="w3ab1c37b9b9b4b6"></a>

##### <a name="w3ab1c37b9b9b4b6b2"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  Full join  |  Yes  |   | 
|  Full outer join  |  Yes  |   | 
|  Left join  |  Yes  |   | 
|  Left outer join  |  Yes  |   | 
|  Right join  |  Yes  |   | 
|  Right outer join  |  Yes  |   | 

### Predicates for Statements<a name="w3ab1c37b9b9b6"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  Boolean conditions  |  Yes  |   | 
|  Exists conditions  |  Yes  |   | 
|  In conditions  |  Yes  |   | 
|  Null conditions  |  Yes  |   | 
|  Pattern matching conditions  |  Yes  |   | 
|  Range conditions  |  Yes  |   | 

#### Comparison Conditions<a name="w3ab1c37b9b9b6b4"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  =, <>, <, <=, >, >=  |  Yes  |   | 
|  ANY, SOME, ALL  |  Partial  |      | 

### Statements<a name="w3ab1c37b9b9b8"></a>

#### DELETE<a name="w3ab1c37b9b9b8b2"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  CURRENT OF  |  Yes  |   | 
|  FROM  |  Partial  |      | 
|  OUTPUT  |  Partial  |      | 
|  TOP  |  No  |      | 
|  VALUES  |  Yes  |   | 
|  WITH  |  Yes  |   | 

#### INSERT<a name="w3ab1c37b9b9b8b4"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  DEFAULT   |  Yes  |   | 
|  DEFAULT VALUES   |  Yes  |   | 
|  FROM  |  Yes  |   | 
|  INTO  |  Yes  |   | 
|  OUTPUT  |  No  |      | 
|  TOP  |  No  |      | 
|  VALUES  |  Yes  |   | 
|  WITH  |  Yes  |   | 

#### SELECT<a name="w3ab1c37b9b9b8b6"></a>

##### <a name="w3ab1c37b9b9b8b6b2"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  GROUP BY clause with an expression  |  Yes  |   | 
|  GROUP BY clause with multiple tables  |  Yes  |   | 
|  GROUP BY CUBE  |  No  |      | 
|  Group By Grouping Sets  |  No  |      | 
|  GROUP BY ROLLUP  |  No  |      | 
|  Limiting the number of rows returned  |  Yes  |   | 
|  Select all columns \(using the \* and aliases\)  |  Yes  |   | 
|  Select all columns \(using the \*\)  |  Yes  |   | 
|  Select subset of the columns  |  Yes  |   | 
|  Select with calculations  |  Yes  |   | 
|  Select with column heading  |  Yes  |   | 
|  Select with constants  |  Yes  |   | 
|  Specifying a ascending order  |  Yes  |   | 
|  Specifying a collation  |  Yes  |   | 
|  Specifying a conditional order  |  Yes  |   | 
|  Specifying a descending order  |  Yes  |   | 
|  Specifying a percentage  |  Yes  |   | 
|  Specifying a percentage \(argument 100 percent\)  |  Yes  |   | 
|  Specifying an alias as the sort column  |  Yes  |   | 
|  Specifying an expression as the sort column  |  Yes  |   | 
|  Specifying both ascending and descending order  |  Yes  |   | 
|  TOP with a variable  |  Yes  |   | 
|  Using ORDER BY and OFFSET command   |  Yes  |   | 
|  Using ORDER BY in a ranking function  |  Yes  |   | 
|  Using ORDER BY with UNION  |  Yes  |   | 
|  Using WITH TIES  |  No  |      | 
|  WHERE with BETWEEN  |  Yes  |   | 
|  WHERE with combination of predicates  |  Yes  |   | 
|  WHERE with CONTAINS  |  No  |      | 
|  WHERE with EXISTS subquery  |  Yes  |   | 
|  WHERE with FREETEXT  |  No  |      | 
|  WHERE with IN custom list  |  Yes  |   | 
|  WHERE with IN subquery  |  Yes  |   | 
|  WHERE with LIKE  |  Partial  |      | 
|  WHERE with negates a Boolean input  |  Yes  |   | 
|  WHERE with NULL  |  Yes  |   | 

##### DISTINCT<a name="w3ab1c37b9b9b8b6b4"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  DISTINCT  |  Yes  |   | 

##### FROM<a name="w3ab1c37b9b9b8b6b6"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  FROM  |  Yes  |   | 

##### GROUP BY<a name="w3ab1c37b9b9b8b6b8"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  GROUP BY  |  Yes  |   | 

##### HAVING<a name="w3ab1c37b9b9b8b6c10"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  HAVING   |  Yes  |   | 

##### ORDER BY<a name="w3ab1c37b9b9b8b6c12"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  ORDER BY  |  Yes  |   | 

##### TOP<a name="w3ab1c37b9b9b8b6c14"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  TOP   |  Yes  |   | 

##### WHERE<a name="w3ab1c37b9b9b8b6c16"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  WHERE  |  Yes  |   | 

#### UPDATE<a name="w3ab1c37b9b9b8b8"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  CURRENT OF  |  Yes  |   | 
|  DEFAULT  |  Yes  |   | 
|  FILESTREAM Data  |  No  |      | 
|  FROM  |  Yes  |   | 
|  OUTPUT  |  Partial  |      | 
|  TOP  |  No  |      | 
|  VALUES  |  Yes  |   | 
|  WITH  |  Yes  |   | 

## Data Types<a name="w3ab1c37b9c11"></a>

### <a name="w3ab1c37b9c11b2"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  BIGINT  |  Yes  |   | 
|  BINARY  |  Yes  |   | 
|  BIT  |  Yes  |   | 
|  CHAR, CHARACTER  |  Yes  |   | 
|  DATETIME  |  Yes  |   | 
|  DATETIMEOFFSET  |  No  |      | 
|  DEC, DECIMAL  |  Yes  |   | 
|  DOUBLE PRECISION  |  Yes  |   | 
|  FLOAT  |  Yes  |   | 
| GEOGRAPHY |  No  |      | 
| GEOMETRY |  No  |      | 
|  HIERARCHYID  |  No  |      | 
|  IDENTITY   |  No  |      | 
|  INT, INTEGER  |  Yes  |   | 
|  MONEY  |  Yes  |   | 
|  NCHAR  |  Yes  |   | 
|  NTEXT  |  Yes  |   | 
|  NUMERIC  |  Yes  |   | 
|  NVARCHAR  |  Yes  |   | 
|  REAL  |  Yes  |   | 
|  ROWVERSION  |  No  |      | 
|  SMALL MONEY  |  Yes  |   | 
|  SMALLDATETIME  |  Yes  |   | 
|  SMALLINT  |  Yes  |   | 
| SQL\_VARIANT |  No  |      | 
|  SYSNAME  |  Yes  |   | 
| TABLE |  No  |      | 
|  TEXT  |  Yes  |   | 
|  TIMESTAMP  |  Yes  |   | 
|  TINYINT  |  Yes  |   | 
|  UNIQUEIDENTIFIER  |  Yes  |   Converted to a universally unique identifier \(UUID\) if the PostgreSQL instance has the uuid\-ossp module installed\. The uuid\-ossp module provides functions to generate UUIDs using one of several standard algorithms\.    | 
|  VARBINARY  |  Yes  |   | 
|  VARCHAR  |  Yes  |   | 
| XML |  No  |      | 

## Database Mail<a name="w3ab1c37b9c13"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  Accounts and Profiles  |  Yes  |   | 
|  Database Mail Configuration Objects  |  Yes  |   | 
|  Database Mail Messaging Objects  |  Yes  |   | 
|  Database Mail Settings  |  Yes  |   | 
|  Security  |  Yes  |   | 
|  sp\_send\_dbmail  |  No  |   | 
|  sysmail\_add\_account\_sp  |  No  |   | 
|  sysmail\_add\_principalprofile\_sp  |  No  |   | 
|  sysmail\_add\_profile\_sp  |  No  |   | 
|  sysmail\_add\_profileaccount\_sp  |  No  |   | 
|  sysmail\_allitems  |  No  |   | 
|  sysmail\_configure\_sp  |  No  |   | 
|  sysmail\_delete\_account\_sp  |  No  |   | 
|  sysmail\_delete\_log\_sp  |  No  |   | 
|  sysmail\_delete\_mailitems\_sp  |  No  |   | 
|  sysmail\_delete\_principalprofile\_sp  |  No  |   | 
|  sysmail\_delete\_profile\_sp  |  No  |   | 
|  sysmail\_delete\_profileaccount\_sp  |  No  |   | 
|  sysmail\_event\_log  |  No  |   | 
|  sysmail\_faileditems  |  No  |   | 
|  sysmail\_help\_account\_sp  |  No  |   | 
|  sysmail\_help\_configure\_sp  |  No  |   | 
|  sysmail\_help\_principalprofile\_sp  |  No  |   | 
|  sysmail\_help\_profile\_sp  |  No  |   | 
|  sysmail\_help\_profileaccount\_sp  |  No  |   | 
|  sysmail\_help\_queue\_sp  |  No  |   | 
|  sysmail\_help\_status\_sp  |  No  |   | 
|  sysmail\_help\_status\_sp  |  No  |   | 
|  sysmail\_mailattachments  |  No  |   | 
|  sysmail\_sentitems  |  No  |   | 
|  sysmail\_start\_sp  |  No  |   | 
|  sysmail\_start\_sp  |  No  |   | 
|  sysmail\_stop\_sp  |  No  |   | 
|  sysmail\_stop\_sp  |  No  |   | 
|  sysmail\_unsentitems  |  No  |   | 
|  sysmail\_update\_account\_sp  |  No  |   | 
|  sysmail\_update\_principalprofile\_sp  |  Yes  |   | 
|  sysmail\_update\_principalprofile\_sp  |  No  |   | 
|  sysmail\_update\_profile\_sp  |  No  |   | 
|  sysmail\_update\_profileaccount\_sp  |  No  |   | 
|  System State  |  Yes  |   | 

## Functions<a name="w3ab1c37b9c15"></a>

### @@functions<a name="w3ab1c37b9c15b2"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  @@CONNECTIONS  |  No  |   | 
|  @@CPU\_BUSY  |  No  |   | 
|  @@CURSOR\_ROWS  |  No  |   | 
|  @@DATEFIRST  |  No  |   | 
|  @@DBTS  |  No  |   | 
|  @@ERROR  |  No  |   | 
|  @@FETCH\_STATUS  |  Yes  |   | 
|  @@IDENTITY  |  Yes  |   | 
|  @@IDLE  |  No  |   | 
|  @@IO\_BUSY  |  No  |   | 
|  @@LANGID  |  No  |   | 
|  @@LANGUAGE  |  No  |   | 
|  @@LOCK\_TIMEOUT  |  No  |   | 
|  @@MAX\_CONNECTIONS  |  No  |   | 
|  @@MAX\_PRECISION  |  No  |   | 
|  @@NESTLEVEL  |  No  |   | 
|  @@OPTIONS  |  No  |   | 
|  @@PACK\_RECEIVED  |  No  |   | 
|  @@PACK\_SENT  |  No  |   | 
|  @@PACKET\_ERRORS  |  No  |   | 
|  @@PROCID  |  No  |   | 
|  @@REMSERVER  |  No  |   | 
|  @@ROWCOUNT  |  No  |   | 
|  @@SERVERNAME  |  No  |   | 
|  @@SERVICENAME  |  No  |   | 
|  @@SPID  |  No  |   | 
|  @@TEXTSIZE  |  No  |   | 
|  @@TIMETICKS  |  No  |   | 
|  @@TOTAL\_ERRORS  |  No  |   | 
|  @@TOTAL\_READ  |  No  |   | 
|  @@TOTAL\_WRITE  |  No  |   | 
|  @@TRANCOUNT  |  No  |   | 
|  @@VERSION  |  No  |   | 

### Aggregate<a name="w3ab1c37b9c15b4"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  AVG  |  Partial  |   | 
|  CHECKSUM\_AGG  |  No  |   | 
|  COUNT  |  Yes  |   | 
|  COUNT\_BIG  |  Yes  |   | 
|  GROUPING  |  No  |   | 
|  GROUPING\_ID  |  No  |   | 
|  MAX  |  Yes  |   | 
|  MIN  |  Yes  |   | 
|  STDEV  |  Yes  |   | 
|  STDEVP  |  Yes  |   | 
|  SUM  |  Yes  |   | 
|  VAR  |  Yes  |   | 
|  VARP  |  Yes  |   | 

### Built\-in Functions<a name="w3ab1c37b9c15b6"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  Aggregate Functions  |  Yes  |   | 
|  Cursor Functions  |  No  |      | 
|  Metadata Functions  |  No  |      | 
|  Security Functions  |  No  |      | 
|  System Functions  |  No  |      | 
|  System Statistical Functions  |  No  |      | 
|  Text and Image Functions  |  No  |      | 

### Conversion<a name="w3ab1c37b9c15b8"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  CAST  |  Partial  |   | 
|  CONVERT  |  Partial  |   | 
|  PARSE  |  No  |   | 
|  TRY\_CAST  |  No  |   | 
|  TRY\_CONVERT  |  No  |   | 
|  TRY\_PARSE  |  No  |   | 

### Date and Time<a name="w3ab1c37b9c15c10"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  CURRENT\_TIMESTAMP  |  Partial  |   | 
|  DATEADD  |  Partial  |   | 
|  DATEDIFF  |  Partial  |   | 
|  DATEFROMPARTS  |  Yes  |   | 
|  DATENAME  |  Partial  |   | 
|  DATEPART  |  Partial  |   | 
|  DATETIME2FROMPARTS  |  Partial  |   | 
|  DATETIMEFROMPARTS  |  Partial  |   | 
|  DATETIMEOFFSETFROMPARTS  |  Partial  |   | 
|  DAY  |  Yes  |   | 
|  EOMONTH  |  Yes  |   | 
|  GETDATE  |  Yes  |   | 
|  GETUTCDATE  |  Yes  |   | 
|  ISDATE  |  No  |   | 
|  MONTH  |  Yes  |   | 
|  SMALLDATETIMEFROMPARTS  |  Yes  |   | 
|  SWITCHOFFSET  |  No  |   | 
|  SYSDATETIME  |  Yes  |   | 
|  SYSDATETIMEOFFSET  |  No  |   | 
|  SYSUTCDATETIME  |  Yes  |   | 
|  TIMEFROMPARTS  |  Yes  |   | 
|  TODATETIMEOFFSET  |  No  |   | 
|  YEAR  |  Yes  |   | 

### Mathematical Functions<a name="w3ab1c37b9c15c12"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  ABS\(\)  |  Yes  |   | 
|  ACOS\(\)  |  Yes  |   | 
|  ASIN\(\)  |  Yes  |   | 
|  ATAN\(\)  |  Yes  |   | 
|  ATN2 \(\)  |  Yes  |   | 
|  CEILING\(\)  |  Yes  |   | 
|  COS\(\)  |  Yes  |   | 
|  COT\(\)  |  Yes  |   | 
|  DEGREES\(\)  |  Yes  |   | 
|  EXP\(\)  |  Yes  |   | 
|  FLOOR\(\)  |  Yes  |   | 
|  LOG\(\)  |  Yes  |   | 
|  LOG10\(\)  |  Yes  |   | 
|  PI\(\)  |  Yes  |   | 
|  POWER\(\)  |  Yes  |   | 
|  RADIANS\(\)  |  Yes  |   | 
|  RAND\(\)  |  Yes  |   | 
|  RAND\(seed\)  |  Partial  |   | 
|  ROUND\(\)  |  Partial  |   | 
|  ROUND\(\)  |  Partial  |   | 
|  SIGN\(\)  |  Yes  |   | 
|  SIN\(\)  |  Yes  |   | 
|  SQRT\(\)  |  Yes  |   | 
|  SQUARE\(\)  |  Yes  |   | 
|  TAN\(\)  |  Yes  |   | 

### Ranking Functions<a name="w3ab1c37b9c15c14"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  DENSE\_RANK  |  Yes  |   | 
|  NTILE  |  Yes  |   | 
|  RANK  |  Yes  |   | 
|  ROW\_NUMBER  |  Yes  |   | 

### Rowset Functions<a name="w3ab1c37b9c15c16"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  CONTAINSTABLE  |  No  |      | 
|  FREETEXTTABLE  |  No  |      | 
|  OPENDATASOURCE  |  No  |      | 
|  OPENQUERY  |  No  |      | 
|  OPENROWSET  |  No  |      | 
|  OPENXML  |  No  |      | 

### Scalar Functions<a name="w3ab1c37b9c15c18"></a>

#### <a name="w3ab1c37b9c15c18b2"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  ABS\(\)  |  Yes  |   | 
|  ACOS\(\)  |  Yes  |   | 
|  ASCII  |  Yes  |   | 
|  ASIN\(\)  |  Yes  |   | 
|  ATAN\(\)  |  Yes  |   | 
|  ATN2 \(\)  |  Yes  |   | 
|  AVG  |  Yes  |   | 
|  CEILING\(\)  |  Yes  |   | 
|  CHAR  |  Yes  |   | 
|  CHARINDEX  |  Yes  |   | 
|  CHECKSUM  |  No  |      | 
|  CHECKSUM\_AGG  |  No  |      | 
|  CHOOSE  |  No  |      | 
|  CONCAT  |  Yes  |   | 
|  COS\(\)  |  Yes  |   | 
|  COT\(\)  |  Yes  |   | 
|  COUNT  |  Yes  |   | 
|  COUNT\_BIG  |  Yes  |   | 
|  CURRENT\_TIMESTAMP  |  Yes  |   | 
|  CURRENT\_USER  |  No  |   | 
|  DATABASE\_PRINCIPAL\_ID  |  No  |   | 
|  DATEADD  |  Partial  |      | 
|  DATEDIFF  |  Partial  |      | 
|  DATEFROMPARTS  |  Yes  |   | 
|  DATENAME  |  Partial  |      | 
|  DATEPART  |  Partial  |      | 
|  DATETIME2FROMPARTS  |  Yes  |   | 
|  DATETIMEFROMPARTS  |  Yes  |   | 
|  DATETIMEOFFSETFROMPARTS  |  No  |      | 
|  DAY  |  Yes  |   | 
|  DEGREES\(\)  |  Yes  |   | 
|  DIFFERENCE  |  No  |      | 
|  EOMONTH  |  Yes  |   | 
|  ERROR\_LINE  |  No  |      | 
|  ERROR\_MESSAGE  |  No  |      | 
|  ERROR\_NUMBER  |  No  |      | 
|  ERROR\_PROCEDURE  |  No  |      | 
|  ERROR\_SEVERITY  |  No  |      | 
|  ERROR\_STATE  |  No  |      | 
|  EXP\(\)  |  Yes  |   | 
|  FLOOR\(\)  |  Yes  |   | 
|  FORMAT  |  No  |      | 
|  FORMATMESSAGE  |  No  |      | 
|  GETDATE  |  Yes  |   | 
|  GETUTCDATE  |  Yes  |   | 
|  GROUPING  |  No  |      | 
|  GROUPING\_ID  |  No  |      | 
|  HOST\_ID  |  No  |      | 
|  HOST\_NAME  |  No  |      | 
|  IIF  |  No  |      | 
|  ISDATE  |  No  |      | 
|  ISNULL  |  Yes  |   | 
|  ISNUMERIC  |  Implemented in Extension Library  |   | 
|  LEFT  |  Yes  |   | 
|  LEN  |  Yes  |   | 
|  LOG\(\)  |  Yes  |   | 
|  LOG10\(\)  |  Yes  |   | 
|  LOWER  |  Yes  |   | 
|  LTRIM  |  Yes  |   | 
|  MAX  |  Yes  |   | 
|  MIN  |  Yes  |   | 
|  MONTH  |  Yes  |   | 
|  NCHAR  |  No  |      | 
|  ORIGINAL\_LOGIN  |  No  |   | 
|  PARSENAME  |  No  |      | 
|  PATINDEX  |  No  |      | 
|  PI\(\)  |  Yes  |   | 
|  POWER\(\)  |  Yes  |   | 
|  PRINT  |  Yes  |   | 
|  QUOTENAME  |  Partial  |      | 
|  RADIANS\(\)  |  Yes  |   | 
|  RAND\(\)  |  Yes  |   | 
|  REPLACE  |  Yes  |   | 
|  REPLICATE  |  Yes  |   | 
|  REVERSE  |  Yes  |   | 
|  RIGHT  |  Yes  |   | 
|  ROUND\(\)  |  Yes  |   | 
|  RTRIM  |  Yes  |   | 
|  SCHEMA\_NAME  |  No  |   | 
|  SESSION\_USER  |  No  |   | 
|  SIGN\(\)  |  Yes  |   | 
|  SIN\(\)  |  Yes  |   | 
|  SMALLDATETIMEFROMPARTS  |  Yes  |   | 
|  SOUNDEX  |  Yes  |   | 
|  SPACE  |  Yes  |   | 
|  SQRT\(\)  |  Yes  |   | 
|  SQUARE\(\)  |  Yes  |   | 
|  STDEV  |  Yes  |   | 
|  STDEVP  |  Yes  |   | 
|  STR  |  No  |      | 
|  STUFF  |  Yes  |   | 
|  SUBSTRING  |  Yes  |   | 
|  SUM  |  Yes  |   | 
|  SWITCHOFFSET  |  No  |      | 
|  SYSDATETIME  |  Yes  |   | 
|  SYSDATETIMEOFFSET  |  No  |      | 
|  SYSUTCDATETIME  |  Yes  |   | 
|  TAN\(\)  |  Yes  |   | 
|  TIMEFROMPARTS  |  Yes  |   | 
|  TODATETIMEOFFSET  |  No  |      | 
|  UNICODE  |  No  |      | 
|  UPPER  |  Yes  |   | 
|  VAR  |  Yes  |   | 
|  VARP  |  Yes  |   | 
|  YEAR  |  Yes  |   | 

### String<a name="w3ab1c37b9c15c20"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  ASCII  |  Yes  |   | 
|  CHAR  |  Yes  |   | 
|  CHARINDEX  |  Yes  |   | 
|  CONCAT  |  Yes  |   | 
|  DIFFERENCE  |  No  |   | 
|  FORMAT  |  No  |   | 
|  LEFT  |  Yes  |   | 
|  LEN  |  Yes  |   | 
|  LOWER  |  Yes  |   | 
|  LTRIM  |  Yes  |   | 
|  NCHAR  |  No  |   | 
|  PATINDEX  |  No  |   | 
|  QUOTENAME  |  Partial  |   | 
|  REPLACE  |  Yes  |   | 
|  REPLICATE  |  Yes  |   | 
|  REVERSE  |  Yes  |   | 
|  RIGHT  |  Yes  |   | 
|  RTRIM  |  Yes  |   | 
|  SOUNDEX  |  No  |   | 
|  SPACE  |  Yes  |   | 
|  STR  |  No  |   | 
|  STUFF  |  Yes  |   | 
|  SUBSTRING  |  Yes  |   | 
|  UNICODE  |  No  |   | 
|  UPPER  |  Yes  |   | 

## Operators<a name="w3ab1c37b9c17"></a>

### Arithmetic Operators<a name="w3ab1c37b9c17b2"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  \- \(Subtract\)  |  Partial  |      | 
|  % \(Modulo\)  |  Partial  |      | 
|  \* \(Multiply\)  |  Partial  |      | 
|  / \(Divide\)  |  Partial  |      | 
|  \+ \(Add\)  |  Partial  |      | 

### Assignment Operator<a name="w3ab1c37b9c17b4"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  =  |  Yes  |   | 

### Bitwise Operators<a name="w3ab1c37b9c17b6"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  & \(Bitwise AND\)  |  Yes  |   | 
|  ^ \(Bitwise Exclusive OR\)  |  No  |      | 
|  | \(Bitwise OR\)  |  Yes  |   | 

### Comparison Operators<a name="w3ab1c37b9c17b8"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  Comparison Operators  |  Partial  |      | 

### Logical Operators<a name="w3ab1c37b9c17c10"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  Logical Operators  |  Yes  |   | 

### Set Operators<a name="w3ab1c37b9c17c12"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  EXCEPT  |  Yes  |   | 
|  INTERSECT  |  Yes  |   | 
|  UNION  |  Yes  |   | 
|  UNION ALL  |  Yes  |   | 

### String Concatenation Operator<a name="w3ab1c37b9c17c14"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  String Concatenation Operator   |  Yes  |   | 

### Unary Operators<a name="w3ab1c37b9c17c16"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  Unary Operators  |  Yes  |   | 

## Other<a name="w3ab1c37b9c19"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  CHECKSUM  |  No  |   | 
|  CHOOSE  |  No  |   | 
|  CURRENT\_USER  |  No  |   | 
|  DATABASE\_PRINCIPAL\_ID  |  No  |   | 
|  ERROR\_LINE  |  No  |   | 
|  ERROR\_MESSAGE  |  No  |   | 
|  ERROR\_NUMBER  |  No  |   | 
|  ERROR\_PROCEDURE  |  No  |   | 
|  ERROR\_SEVERITY  |  No  |   | 
|  ERROR\_STATE  |  No  |   | 
|  FORMATMESSAGE  |  No  |   | 
|  HOST\_ID  |  No  |   | 
|  HOST\_NAME  |  No  |   | 
|  IIF  |  No  |   | 
|  ISNULL  |  Yes  |   | 
|  ISNUMERIC  |  No  |   | 
|  Logical Functions  |  Yes  |   | 
|  NEWID  |  Yes  |   | 
|  ORIGINAL\_LOGIN  |  No  |   | 
|  Other  |  Yes  |   | 
|  PRINT  |  Yes  |   | 
|  SCHEMA\_NAME  |  No  |   | 
|  Security Functions  |  Yes  |   | 
|  SESSION\_USER  |  No  |   | 
|  System Functions  |  Yes  |   | 

## Service Broker<a name="w3ab1c37b9c21"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  ALTER QUEUE  |  No  |   | 
|  ALTER SERVICE  |  No  |   | 
|  BEGIN CONVERSATION TIMER  |  No  |   | 
|  BEGIN DIALOG CONVERSATION  |  No  |   | 
|  CREATE QUEUE  |  No  |   | 
|  CREATE SERVICE  |  No  |   | 
|  DROP QUEUE  |  No  |   | 
|  DROP SERVICE  |  No  |   | 
|  END CONVERSATION  |  No  |   | 
|  GET CONVERSATION GROUP  |  No  |   | 
|  GET TRANSMISSION\_STATUS  |  No  |   | 
|  MOVE CONVERSATION  |  No  |   | 
|  Queue management  |  Yes  |   | 
|  RECEIVE  |  No  |   | 
|  SEND  |  No  |   | 
|  Service Broker Catalog Views  |  Yes  |   | 
|  Service Broker Related Dynamic Management Views  |  Yes  |   | 
|  Service Broker Statements  |  Yes  |   | 
|  Service management  |  Yes  |   | 
|  sys\.conversation\_endpoints  |  No  |   | 
|  sys\.conversation\_groups  |  No  |   | 
|  sys\.conversation\_priorities  |  No  |   | 
|  sys\.dm\_broker\_activated\_tasks  |  No  |   | 
|  sys\.dm\_broker\_connections  |  No  |   | 
|  sys\.dm\_broker\_forwarded\_messages  |  No  |   | 
|  sys\.dm\_broker\_queue\_monitors  |  No  |   | 
|  sys\.message\_type\_xml\_schema\_collection\_usages  |  No  |   | 
|  sys\.remote\_service\_bindings  |  No  |   | 
|  sys\.routes  |  No  |   | 
|  sys\.service\_contract\_message\_usages  |  No  |   | 
|  sys\.service\_contract\_usages  |  No  |   | 
|  sys\.service\_contracts  |  No  |   | 
|  sys\.service\_message\_types  |  No  |   | 
|  sys\.service\_queue\_usages  |  No  |   | 
|  sys\.service\_queues  |  No  |   | 
|  sys\.services  |  No  |   | 
|  sys\.transmission\_queue  |  No  |   | 

## SQL Server Agent<a name="w3ab1c37b9c23"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  sp\_add\_alert  |  No  |   | 
|  sp\_add\_category  |  No  |   | 
|  sp\_add\_job  |  No  |   | 
|  sp\_add\_jobschedule  |  No  |   | 
|  sp\_add\_jobserver  |  No  |   | 
|  sp\_add\_jobstep  |  No  |   | 
|  sp\_add\_notification  |  No  |   | 
|  sp\_add\_operator  |  No  |   | 
|  sp\_add\_proxy  |  No  |   | 
|  sp\_add\_schedule  |  No  |   | 
|  sp\_add\_targetservergroup  |  No  |   | 
|  sp\_add\_targetsvrgrp\_member  |  No  |   | 
|  sp\_apply\_job\_to\_targets  |  No  |   | 
|  sp\_attach\_schedule  |  No  |   | 
|  sp\_cycle\_agent\_errorlog  |  No  |   | 
|  sp\_cycle\_errorlog  |  No  |   | 
|  sp\_delete\_alert  |  No  |   | 
|  sp\_delete\_category  |  No  |   | 
|  sp\_delete\_job  |  No  |   | 
|  sp\_delete\_jobschedule  |  No  |   | 
|  sp\_delete\_jobserver  |  No  |   | 
|  sp\_delete\_jobstep  |  No  |   | 
|  sp\_delete\_jobsteplog  |  No  |   | 
|  sp\_delete\_notification  |  No  |   | 
|  sp\_delete\_operator  |  No  |   | 
|  sp\_delete\_proxy  |  No  |   | 
|  sp\_delete\_schedule  |  No  |   | 
|  sp\_delete\_targetserver  |  No  |   | 
|  sp\_delete\_targetservergroup  |  No  |   | 
|  sp\_delete\_targetsvrgrp\_member  |  No  |   | 
|  sp\_detach\_schedule  |  No  |   | 
|  sp\_enum\_login\_for\_proxy  |  No  |   | 
|  sp\_enum\_proxy\_for\_subsystem  |  No  |   | 
|  sp\_enum\_sqlagent\_subsystems  |  No  |   | 
|  sp\_grant\_login\_to\_proxy  |  No  |   | 
|  sp\_grant\_proxy\_to\_subsystem  |  No  |   | 
|  sp\_help\_alert  |  No  |   | 
|  sp\_help\_category  |  No  |   | 
|  sp\_help\_downloadlist  |  No  |   | 
|  sp\_help\_job  |  No  |   | 
|  sp\_help\_jobactivity  |  No  |   | 
|  sp\_help\_jobcount  |  No  |   | 
|  sp\_help\_jobhistory  |  No  |   | 
|  sp\_help\_jobs\_in\_schedule  |  No  |   | 
|  sp\_help\_jobschedule  |  No  |   | 
|  sp\_help\_jobserver  |  No  |   | 
|  sp\_help\_jobstep  |  No  |   | 
|  sp\_help\_jobsteplog  |  No  |   | 
|  sp\_help\_notification  |  No  |   | 
|  sp\_help\_operator  |  No  |   | 
|  sp\_help\_proxy  |  No  |   | 
|  sp\_help\_schedule  |  No  |   | 
|  sp\_help\_targetserver  |  No  |   | 
|  sp\_help\_targetservergroup  |  No  |   | 
|  sp\_manage\_jobs\_by\_login  |  No  |   | 
|  sp\_msx\_defect  |  No  |   | 
|  sp\_msx\_enlist  |  No  |   | 
|  sp\_msx\_get\_account  |  No  |   | 
|  sp\_msx\_set\_account  |  No  |   | 
|  sp\_notify\_operator  |  No  |   | 
|  sp\_post\_msx\_operation  |  No  |   | 
|  sp\_purge\_jobhistory  |  No  |   | 
|  sp\_remove\_job\_from\_targetss  |  No  |   | 
|  sp\_resync\_targetserver  |  No  |   | 
|  sp\_revoke\_login\_from\_proxy  |  No  |   | 
|  sp\_revoke\_proxy\_from\_subsystem  |  No  |   | 
|  sp\_start\_job  |  No  |   | 
|  sp\_stop\_job  |  No  |   | 
|  sp\_update\_alert  |  No  |   | 
|  sp\_update\_category  |  No  |   | 
|  sp\_update\_job  |  No  |   | 
|  sp\_update\_jobschedule  |  No  |   | 
|  sp\_update\_jobstep  |  No  |   | 
|  sp\_update\_notification  |  No  |   | 
|  sp\_update\_operator  |  No  |   | 
|  sp\_update\_proxy  |  No  |   | 
|  sp\_update\_schedule  |  No  |   | 
|  sp\_update\_targetservergroup  |  No  |   | 

## SQL Server Backup<a name="w3ab1c37b9c25"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  BACKUP  |  No  |   | 
|  BACKUP CERTIFICATE  |  No  |   | 
|  BACKUP MASTER KEY  |  No  |   | 
|  BACKUP SERVICE MASTER KEY  |  No  |   | 
|  RESTORE  |  No  |   | 
|  RESTORE FILELISTONLY  |  No  |   | 
|  RESTORE HEADERONLY  |  No  |   | 
|  RESTORE LABELONLY  |  No  |   | 
|  RESTORE MASTER KEY  |  No  |   | 
|  RESTORE REWINDONLY  |  No  |   | 
|  RESTORE SERVICE MASTER KEY  |  No  |   | 
|  RESTORE VERIFYONLY  |  No  |   | 

## T\-SQL<a name="w3ab1c37b9c27"></a>

### BACKUP and RESTORE<a name="w3ab1c37b9c27b2"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  BACKUP and RESTORE Statements  |  No  |      | 

### Collation<a name="w3ab1c37b9c27b4"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  Collation  |  No  |      | 

### Control\-of\-Flow Language<a name="w3ab1c37b9c27b6"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  BEGIN\.\.\.END  |  Yes  |   | 
|  BREAK  |  Yes  |   | 
|  CONTINUE   |  Yes  |   | 
|  GOTO   |  No  |      | 
|  IF\.\.\.ELSE  |  Yes  |   | 
|  RETURN   |  Yes  |   | 
|  THROW   |  Yes  |   | 
|  TRY\.\.\.CATCH  |  Yes  |   | 
|  WAITFOR  |  Partial  |      | 
|  WHILE   |  Yes  |   | 

### Cursors<a name="w3ab1c37b9c27b8"></a>

#### DECLARE CURSOR<a name="w3ab1c37b9c27b8b2"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  DECLARE CURSOR  |  Yes  |   | 
|  CURSOR with option GLOBAL  |  No  |      | 
|  CURSOR with options FORWARD\_ONLY or SCROLL  |  No  |      | 

#### FETCH<a name="w3ab1c37b9c27b8b4"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  FETCH  |  Yes  |   | 

#### OPEN<a name="w3ab1c37b9c27b8b6"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  OPEN  |  Yes  |   | 

### DUMP and LOAD Statements<a name="w3ab1c37b9c27c10"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  DUMP and LOAD Statements  |  No  |      | 