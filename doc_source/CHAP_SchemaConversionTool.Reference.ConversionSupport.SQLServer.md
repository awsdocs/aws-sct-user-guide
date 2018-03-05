# Microsoft SQL Server to MySQL Supported Schema Conversion<a name="CHAP_SchemaConversionTool.Reference.ConversionSupport.SQLServer"></a>

The following sections list the schema elements from Microsoft SQL Server and whether they are supported for automatic conversion to MySQL using the AWS Schema Conversion Tool\.


+ [Statements](#w3ab1c37b7b7)
+ [Procedures](#w3ab1c37b7b9)
+ [Flow Control](#w3ab1c37b7c11)
+ [Functions](#w3ab1c37b7c13)
+ [Operators](#w3ab1c37b7c15)
+ [Transactions](#w3ab1c37b7c17)
+ [Data Types](#w3ab1c37b7c19)
+ [Data Definition Language \(DDL\)](#w3ab1c37b7c21)
+ [Cursors](#w3ab1c37b7c23)
+ [Related Topics](#w3ab1c37b7c25)

## Statements<a name="w3ab1c37b7b7"></a>


+ [SELECT](#w3ab1c37b7b7b4)
+ [INSERT](#w3ab1c37b7b7b6)
+ [UPDATE](#w3ab1c37b7b7b8)
+ [DELETE](#w3ab1c37b7b7c10)

### SELECT<a name="w3ab1c37b7b7b4"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
| WITH | No | Try converting the WITH\(query\) expression to a subquery and use it in a SELECT query\. | 
| UNION | Yes |  | 
| EXCEPT | INTERSECT | No |  | 
| ALL | DISTINCT | Yes |  | 
| TOP | Partial | MySQL doesn't support TOP with the PERCENT or WITH TIES options\. Try using the LIMIT option or perform a manual conversion\. | 
| <select\_list> | Yes |  | 
| INTO | No |  | 
| FROM | Partial | MySQL doesn't support the CONTAINS and FREETEXT predicates in the FROM clause search condition\. | 
| WHERE | Yes |  | 
| GROUP BY | Partial | MySQL doesn't support ORDER BY with the ROLLUP, CUBE, and GROUPING SETS options\. Try creating a stored procedure to replace the query\. | 
| HAVING | Yes |  | 
| ORDER BY | Partial | MySQL doesn't support ORDER BY with the OFFSET or FETCH options\. Try creating a stored procedure to replace the query\. MySQL doesn't support ORDER BY with the COLLATE option\. You must use the collation settings that were assigned when the database was created\. | 
| FOR | No |  | 
| OPTION | No |  | 

### INSERT<a name="w3ab1c37b7b7b6"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
| WITH | No | Try to convert the WITH query to a subquery, and then use the subquery in the INSERT query\. | 
| INSERT | Yes |  | 
| TOP | No | Get a count of all rows, and then use the following expression, where count\_of\_all\_rows is your row count: percent\_expression \* count\_of\_all\_rows / 100 | 
| INTO | Yes |  | 
| table\_name | Yes |  | 
| WITH \(<Table\_Hint\_Limited>\) | No | Use MySQL methods of performance tuning\. | 
| OUTPUT | No | Create a trigger for INSERT statements for the table, and then save the inserted rows in a temporary table\. After the INSERT operation, you can make use of the rows saved in the temporary table\. This logic can be placed in a stored procedure\. | 
| VALUES | Yes |  | 
| derived\_table  | Yes |  | 
| execute\_statement  | No | Create a temporary table, fill it with the data to insert, and use the temporary table in the query\. | 
| <dml\_table\_source> | No |  | 
| DEFAULT VALUES  | No |  | 

### UPDATE<a name="w3ab1c37b7b7b8"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
| WITH | No | Try to convert the WITH query to a subquery, and then use the subquery in the UPDATE query\. | 
| TOP | Partial | MySQL doesn't support UPDATE with the PERCENT option\. Get a count of all rows, and then use the following expression, where count\_of\_all\_rows is your row count: percent\_expression \* count\_of\_all\_rows / 100 | 
| WITH \(<Table\_Hint\_Limited>\) | No | Use MySQL methods of performance tuning\. | 
| SET | No |  | 
| OUTPUT | No | Create a trigger for UPDATE statements for the table, and then save the changed rows in a temporary table\. After the UPDATE operation, you can make use of the rows saved in the temporary table\. This logic can be placed in a stored procedure\. | 
| FROM | Partial | MySQL doesn't support a FROM clause\. AWS Schema Conversion Tool moves <table\-source> to the UPDATE clause\. | 
| WHERE | Yes |  | 
| CURRENT OF  | No | Replace the CURRENT OF clause with an expression that consists of conditions that use unique key fields of the table\.  | 
| GLOBAL | No |  | 
| OPTION | No |  | 

**Note**  
MySQL doesn't support FILESTREAM DATA\. Perform a manual conversion to update the data in the file system file\. 

### DELETE<a name="w3ab1c37b7b7c10"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
| WITH | No | Try to convert the WITH query to a subquery, and then use the subquery in the DELETE query\. | 
| TOP | Partial | MySQL doesn't support the PERCENT option\. A manual conversion is required\. Get a count of all rows, and then use the following expression, where count\_of\_all\_rows is your row count: percent\_expression \* count\_of\_all\_rows / 100 | 
| FROM | Yes |  | 
| table\_or\_view\_name  | Yes |  | 
| rowset\_function\_limited  | No |  | 
| WITH | No | MySQL doesn't support hints in DELETE statements, so the AWS Schema Conversion Tool skips options in the format WITH\(Table\_Hint\_Limited\)\. Use MySQL methods of performance tuning\. | 
| OUTPUT | No | Create a trigger for DELETE statements for the table, and then save the deleted rows in a temporary table\. After the DELETE operation, you can make use of the rows saved in the temporary table\. This logic can be placed in a stored procedure\. | 
| WHERE | Yes |  | 
| CURRENT OF  | No | Replace the CURRENT OF clause with an expression that consists of conditions that use unique key fields of the table\.  | 
| GLOBAL | No |  | 
| OPTION | No |  | 

## Procedures<a name="w3ab1c37b7b9"></a>


+ [CREATE PROCEDURE](#w3ab1c37b7b9b4)

### CREATE PROCEDURE<a name="w3ab1c37b7b9b4"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
| @parameter | Yes | MySQL doesn't support procedure arguments of the CURSOR data type\. Change the business logic to eliminate the need to send cursors through arguments to a stored procedure\. | 
| VARYING | Partial |  | 
| OUT |  |  | 
| OUTPUT | Partial |  | 
| READONLY | Partial |  | 
| WITH | No |  | 
| FOR REPLICATION | No |  | 
| AS BEGIN … END | No |  | 
| ENCRYPTION  | Yes |  | 
| RECOMPILE  | No |  | 
| EXECUTE AS | No |  | 

## Flow Control<a name="w3ab1c37b7c11"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
| TRY…CATCH THROW | No | Try using the DECLARE HANDLER for the CATCH emulation block and the SIGNAL SQLSTATE operator to emulate the THROW operator\. | 
| WAITFOR | No | Perform a manual conversion\. | 
| DECLARE | No | Perform a manual conversion\. | 
| GOTO | No | Revise your code to eliminate GOTO operators, using BEGIN\.\.\.END blocks in combination with LEAVE, REPEAT, UNTIL, and WHILE operators\. | 
| BREAK | Yes |  | 
| CONTINUE | Yes |  | 
| IF…ELSE | Yes |  | 
| RETURN | No | MySQL does not support returning a value from a procedure using the RETURN statement\. To return a value, use the OUT parameter or a result set\. | 
| WHILE | Yes |  | 
| CASE | Yes |  | 
| COALESCE | Yes |  | 
| NULLIF | Yes |  | 

## Functions<a name="w3ab1c37b7c13"></a>


+ [Aggregate Functions](#w3ab1c37b7c13b6)
+ [Date and Time Functions](#w3ab1c37b7c13b8)
+ [Mathematical Functions](#w3ab1c37b7c13c10)
+ [String Functions](#w3ab1c37b7c13c12)
+ [Configuration Functions](#w3ab1c37b7c13c14)
+ [Conversion Functions](#w3ab1c37b7c13c16)
+ [Security Functions](#w3ab1c37b7c13c18)
+ [System Functions](#w3ab1c37b7c13c20)
+ [Logical Functions](#w3ab1c37b7c13c22)
+ [CREATE FUNCTION](#w3ab1c37b7c13c24)
+ [EXECUTE](#w3ab1c37b7c13c26)

In this section, you can find a list of the Microsoft SQL Server built\-in functions that indicates whether the AWS Schema Conversion Tool performs an automatic conversion\. Where MySQL doesn't support a function, consider creating a user\-defined function\. 

### Aggregate Functions<a name="w3ab1c37b7c13b6"></a>


| Function | Automatically Converted | Details | 
| --- | --- | --- | 
| AVG | Yes |  | 
| COUNT | Yes |  | 
| COUNT\_BIG | Partial |  | 
| MIN | Yes |  | 
| MAX | Yes |  | 
| SUM | Yes |  | 
| CHECKSUM\_AGG | No |  | 
| STDEV | Partial | MySQL doesn't support the STDEV function with the DISTINCT clause\. | 
| STDEVP | Partial | MySQL doesn't support the STDEVP function with the DISTINCT clause\. | 
| GROUPING | No |  | 
| GROUPING\_ID | No |  | 
| VAR | Partial | MySQL doesn't support the VAR function with the DISTINCT clause\. | 
| VARP | Partial | MySQL doesn't support the VARP function with the DISTINCT clause\. | 

### Date and Time Functions<a name="w3ab1c37b7c13b8"></a>


| Function | Automatically Converted | Details | 
| --- | --- | --- | 
| DATEADD | Partial | MySQL doesn't support the DATEADD function with the nanosecond datepart\. | 
| DATEDIFF | Partial | MySQL doesn't support the DATEDIFF function with the week, millisecond, or nanosecond datepart\. | 
| DATENAME | Partial | MySQL doesn't support the DATENAME function with the millisecond, nanosecond, or TZoffset datepart\. | 
| DATEPART | Partial | MySQL doesn't support the DATEPART function with the millisecond, nanosecond, or TZoffset datepart\. | 
| DAY | Partial |  | 
| GETDATE | Partial |  | 
| GETDATE \+ 1 | Partial |  | 
| GETUTCDATE | Partial |  | 
| MONTH | Partial |  | 
| YEAR | Partial |  | 
| DATETIMEOFFSETFROMPARTS | No |  | 
| ISDATE | No |  | 
| SWITCHOFFSET | No |  | 
| SYSDATETIMEOFFSET | No |  | 
| TODATETIMEOFFSET | No |  | 

### Mathematical Functions<a name="w3ab1c37b7c13c10"></a>


| Function | Automatically Converted | Details | 
| --- | --- | --- | 
| ABS | Yes |  | 
| ACOS | Yes |  | 
| ASIN | Yes |  | 
| ATN2 | Partial |  | 
| ATAN | Yes |  | 
| CEILING | Yes |  | 
| COS | Yes |  | 
| COT | Yes |  | 
| DEGREES | Yes |  | 
| EXP | Yes |  | 
| FLOOR | Yes |  | 
| LOG10 | Yes |  | 
| LOG | Yes |  | 
| PI | Yes |  | 
| POWER | Yes |  | 
| RADIANS | Yes |  | 
| RAND | Yes |  | 
| ROUND | Partial | MySQL doesn't support the ROUND function with the function argument\. | 
| SIGN | Yes |  | 
| SIN | Yes |  | 
| SQRT | Yes |  | 
| SQUARE | No |  | 
| TAN | Yes |  | 

### String Functions<a name="w3ab1c37b7c13c12"></a>


| Function | Automatically Converted | Details | 
| --- | --- | --- | 
| ASCII  | Yes |  | 
| CHAR  | Yes |  | 
| CHARINDEX  | No |  | 
| CONCAT  | Yes |  | 
| DIFFERENCE  | No |  | 
| FORMAT  | No |  | 
| LEFT  | Yes |  | 
| LEN  | Partial |  | 
| LOWER  | Yes |  | 
| LTRIM  | Yes |  | 
| NCHAR  | No |  | 
| PATINDEX  | No |  | 
| QUOTENAME  | Partial |  | 
| REPLACE  | Yes |  | 
| REPLICATE  | Partial |  | 
| REVERSE  | Yes |  | 
| RIGHT  | Yes |  | 
| RTRIM  | Yes |  | 
| SOUNDEX  | No |  | 
| SPACE  | Yes |  | 
| STR  | No |  | 
| STUFF  | No |  | 
| SUBSTRING  | Yes |  | 
| UNICODE  | No |  | 
| UPPER | Yes |  | 

### Configuration Functions<a name="w3ab1c37b7c13c14"></a>


| Function | Automatically Converted | Details | 
| --- | --- | --- | 
| @@DATEFIRST | No |  | 
| @@DBTS | Yes |  | 
| @@LANGID | Yes |  | 
| @@LANGUAGE | No |  | 
| @@LOCK\_TIMEOUT | Yes |  | 
| @@MAX\_CONNECTIONS | No |  | 
| @@MAX\_PRECISION | Yes |  | 
| @@NESTLEVEL | Yes |  | 
| @@OPTIONS | Yes |  | 
| @@REMSERVER | Yes |  | 
| @@SERVERNAME | No |  | 
| @@SERVICENAME | Yes |  | 
| @@SPID | Yes |  | 
| @@TEXTSIZE | Yes |  | 
| @@VERSION | No |  | 

### Conversion Functions<a name="w3ab1c37b7c13c16"></a>


| Function | Automatically Converted | Details | 
| --- | --- | --- | 
| CAST and CONVERT | No |  | 
| PARSE | No |  | 
| TRY\_CAST | No |  | 
| TRY\_CONVERT | No |  | 
| TRY\_PARSE | No |  | 

### Security Functions<a name="w3ab1c37b7c13c18"></a>


| Function | Automatically Converted | Details | 
| --- | --- | --- | 
| CERTENCODED | Yes |  | 
| CERTPRIVATEKEY | Yes |  | 
| CURRENT\_USER | No |  | 
| DATABASE\_PRINCIPAL\_ID | No |  | 
| HAS\_PERMS\_BY\_NAME | Yes |  | 
| IS\_MEMBER | Yes |  | 
| IS\_ROLEMEMBER | Yes |  | 
| IS\_SRVROLEMEMBER | Yes |  | 
| ORIGINAL\_LOGIN | No |  | 
| PERMISSIONS | Yes |  | 
| PWDCOMPARE | Yes |  | 
| PWDENCRYPT | Yes |  | 
| SCHEMA\_ID | Yes |  | 
| SCHEMA\_NAME | No |  | 
| SESSION\_USER | No |  | 
| SUSER\_ID | Yes |  | 
| SUSER\_NAME | Yes |  | 
| SUSER\_SID | Yes |  | 
| SUSER\_SNAME | Yes |  | 
| sys\.fn\_builtin\_permissions | Yes |  | 
| sys\.fn\_get\_audit\_file | Yes |  | 
| sys\.fn\_my\_permissions | Yes |  | 
| SYSTEM\_USER | Yes |  | 
| USER\_ID | Yes |  | 
| USER\_NAME | Yes |  | 

### System Functions<a name="w3ab1c37b7c13c20"></a>


| Function | Automatically Converted | Details | 
| --- | --- | --- | 
| $PARTITION | Yes |  | 
| @@ERROR | Yes |  | 
| @@IDENTITY | Yes |  | 
| @@PACK\_RECEIVED | Yes |  | 
| @@ROWCOUNT | Yes |  | 
| @@TRANCOUNT | Yes |  | 
| BINARY\_CHECKSUM | Yes |  | 
| CHECKSUM | No |  | 
| CONNECTIONPROPERTY | Yes |  | 
| CONTEXT\_INFO | Yes |  | 
| CURRENT\_REQUEST\_ID | Yes |  | 
| ERROR\_LINE | No |  | 
| ERROR\_MESSAGE | No |  | 
| ERROR\_NUMBER | No |  | 
| ERROR\_PROCEDURE | No |  | 
| ERROR\_SEVERITY | No |  | 
| ERROR\_STATE | No |  | 
| FORMATMESSAGE | No |  | 
| GET\_FILESTREAM\_TRANSACTION\_CONTEXT | Yes |  | 
| GETANSINULL | Yes |  | 
| HOST\_ID | No |  | 
| HOST\_NAME | No |  | 
| ISNULL | No |  | 
| MIN\_ACTIVE\_ROWVERSION | Yes |  | 
| NEWID | Yes |  | 
| NEWSEQUENTIALID | Yes |  | 
| PARSENAME | Yes |  | 
| ROWCOUNT\_BIG | Yes |  | 
| XACT\_STATE | Yes |  | 

### Logical Functions<a name="w3ab1c37b7c13c22"></a>


| Function | Automatically Converted | Details | 
| --- | --- | --- | 
| CHOOSE | No |  | 
| IIF | No |  | 

### CREATE FUNCTION<a name="w3ab1c37b7c13c24"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
| @parameter\_name | Yes |  | 
| type\_schema\_name | Yes |  | 
| parameter\_data\_type  | No |  | 
|  = default  | Yes |  | 
| READONLY  | No |  | 
| RETURNS return\_data\_type | No |  | 
| WITH function\_option | Yes |  | 
| BEGIN … END | No |  | 
| RETURN scalar\_expression | Yes | MySQL supports only functions that return a scalar value\. | 

### EXECUTE<a name="w3ab1c37b7c13c26"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
| @parameter\_name | Yes |  | 
| type\_schema\_name | Yes |  | 
| parameter\_data\_type  | No |  | 
|  = default  | Yes |  | 
| READONLY  | No |  | 
| RETURNS return\_data\_type | No |  | 
| WITH function\_option | Yes |  | 
| BEGIN … END | No |  | 
| RETURN scalar\_expression | Yes | MySQL supports only functions that return a scalar value\. | 

## Operators<a name="w3ab1c37b7c15"></a>


+ [Arithmetic Operators](#w3ab1c37b7c15b4)
+ [Assignment Operator](#w3ab1c37b7c15b6)
+ [Bitwise Operators](#w3ab1c37b7c15b8)
+ [Comparison Operators](#w3ab1c37b7c15c10)
+ [Logical Operators](#w3ab1c37b7c15c12)
+ [Set Operators](#w3ab1c37b7c15c14)
+ [String Concatenation Operator](#w3ab1c37b7c15c16)
+ [Unary Operators](#w3ab1c37b7c15c18)

### Arithmetic Operators<a name="w3ab1c37b7c15b4"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
| \+ | Yes |  | 
| \+= | Yes |  | 
| \- | Yes |  | 
| \-= | Yes |  | 
| \* | Yes |  | 
| \*= | Yes |  | 
| / | Yes |  | 
| /= | Yes |  | 
| % | Yes |  | 

### Assignment Operator<a name="w3ab1c37b7c15b6"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
| = | Yes |  | 

### Bitwise Operators<a name="w3ab1c37b7c15b8"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
| & | Yes |  | 
| | | Yes |  | 
| ^ | Yes |  | 
| \~ | Yes |  | 

### Comparison Operators<a name="w3ab1c37b7c15c10"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
| = | Yes |  | 
| > | Yes |  | 
| < | Yes |  | 
| >= | Yes |  | 
| <= | Yes |  | 
| <> | Yes |  | 
| \!= | Yes |  | 
| \!< | Yes |  | 
| \!> | Yes |  | 

### Logical Operators<a name="w3ab1c37b7c15c12"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
| ALL | Yes |  | 
| AND | Yes |  | 
| ANY | Yes |  | 
| BETWEEN | Yes |  | 
| EXISTS | Yes |  | 
| IN | Yes |  | 
| LIKE | Yes |  | 
| NOT | Yes |  | 
| OR | Yes |  | 
| SOME | Partial | The AWS Schema Conversion Tool converts SOME to ANY\. | 

### Set Operators<a name="w3ab1c37b7c15c14"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
| UNION | Yes |  | 
| UNION ALL | Yes |  | 
| EXCEPT | No | Perform a manual conversion\. | 
| INTERSECT | No | Perform a manual conversion\. | 

### String Concatenation Operator<a name="w3ab1c37b7c15c16"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
| \+ | Yes |  | 

### Unary Operators<a name="w3ab1c37b7c15c18"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
| \+ | Yes |  | 
| \- | Yes |  | 

## Transactions<a name="w3ab1c37b7c17"></a>


+ [BEGIN TRANSACTION](#w3ab1c37b7c17b4)

### BEGIN TRANSACTION<a name="w3ab1c37b7c17b4"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
| DISTRIBUTED | No | MySQL doesn't support distributed transactions\. Revise your architecture so that it doesn't use distributed transactions\. | 
| transaction\_name | No | MySQL doesn't support named transactions\. Revise your code to eliminate marked transactions\. | 
| WITH MARK | No | MySQL doesn't support the WITH MARK option\. Revise your code to eliminate marked transactions\. | 
| SAVE | Partial |  | 
| ROLLBACK | Partial |  | 
| transaction\_name | No | MySQL doesn't support named transactions\. Revise your code to eliminate named transactions\. | 
| savepoint\_name | Partial |  | 
| COMMIT | Partial |  | 
| DELAYED\_DURABILITY | No |  | 

## Data Types<a name="w3ab1c37b7c19"></a>


+ [Numerics](#w3ab1c37b7c19b4)
+ [Date and Time](#w3ab1c37b7c19b6)
+ [Character Strings](#w3ab1c37b7c19b8)
+ [Binary Strings](#w3ab1c37b7c19c10)
+ [Special Types](#w3ab1c37b7c19c12)

### Numerics<a name="w3ab1c37b7c19b4"></a>


| Data type | Automatically Converted | Default Conversion | Details | 
| --- | --- | --- | --- | 
| bigint | Yes | bigint |  | 
| int | Yes | int |  | 
| smallint | Yes | smallint |  | 
| tinyint | Yes | tinyint unsigned |  | 
| bit | Yes | bit\(1\) |  | 
| money | Yes | numeric\(19,4\) |  | 
| smallmoney | Yes | numeric\(10,4\) |  | 
| numeric | Yes | numeric |  | 
| decimal  | Yes | decimal  |  | 
| float  | Yes | double  |  | 
| real  | Yes | float  |  | 

### Date and Time<a name="w3ab1c37b7c19b6"></a>


| Data type | Automatically Converted | Default Conversion | Details | 
| --- | --- | --- | --- | 
| date | Partial | date | 0001\-01\-01 through 9999\-12\-31 | 
| datetime2\(7\) | Partial | datetime | 0001\-01\-01 through 9999\-12\-31 00:00:00 through 23:59:59\.9999999 | 
| datetime | Partial | datetime | 1753\-01\-01, through 9999\-12\-31 00:00:00 through 23:59:59\.997 | 
| datetimeoffset\(7\) | No |  |  | 
| smalldatetime | Yes | datetime |  | 
| time\(7\) | Yes | time |  | 

### Character Strings<a name="w3ab1c37b7c19b8"></a>


| Data type | Automatically Converted | Default Conversion | Details | 
| --- | --- | --- | --- | 
| char\(len\) | Partial | char | len= 1 \- 255 \(2^8 \- 1\) symbols \(loss range\)  | 
| varchar\(len\) | Yes | varchar |  | 
| varchar\(max\) | Yes | longtext |  | 
| text | Yes | longtext |  | 
| nchar\(len\) | len = 1 \- 4000 | char | len= 1 \- 255 \(2^8 \- 1\) symbols \(loss range\)  | 
| nvarchar\(len\) | Yes | varchar |  | 
| nvarchar\(max\) | Yes | longtext |  | 
| ntext | Yes | longtext |  | 

### Binary Strings<a name="w3ab1c37b7c19c10"></a>


| Data type | Automatically Converted | Default Conversion | Details | 
| --- | --- | --- | --- | 
| binary\(len\) | Yes | blob |  | 
| varbinary\(len\) | Yes | blob |  | 
| varbinary\(max\) | Yes | longblob |  | 
| hierarchyid | No |  |  | 
| sql\_variant | No |  |  | 
| table | No |  |  | 
| uniqueidentifier | No |  |  | 
| xml | No |  |  | 
| geography | No |  |  | 
| geometry | No |  |  | 

### Special Types<a name="w3ab1c37b7c19c12"></a>


| Data type | Automatically Converted | Default Conversion | Details | 
| --- | --- | --- | --- | 
| UNIQUEIDENTIFIER | Partial | CHAR\(38\) OR BINARY\(16\) |  | 
| DOUBLE PRECISION | Partial | FLOAT\(53\) |  | 
| IDENTITY | Partial | AUTO\_INCREMENT |  | 
| SYSNAME | Partial | NVARCHAR\(128\) NOT NULL |  | 

## Data Definition Language \(DDL\)<a name="w3ab1c37b7c21"></a>


+ [CREATE TABLE](#w3ab1c37b7c21b4)
+ [CREATE INDEX](#w3ab1c37b7c21b6)
+ [CREATE TRIGGER](#w3ab1c37b7c21b8)
+ [CREATE VIEW](#w3ab1c37b7c21c10)

### CREATE TABLE<a name="w3ab1c37b7c21b4"></a>

CREATE TABLE statements are converted automatically except for the following clause\. 


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
| SET DEFAULT | No | MySQL doesn't support the SET DEFAULT option for FOREIGN KEY\. | 

### CREATE INDEX<a name="w3ab1c37b7c21b6"></a>

The AWS Schema Conversion Tool does not support automatic migration of data definition language \(DDL\) code to create an index\. 

### CREATE TRIGGER<a name="w3ab1c37b7c21b8"></a>

CREATE TRIGGER statements are converted automatically except for the following clause\. 


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
| FOR | No | MySQL doesn't support a FOR clause in a CREATE TRIGGER statement\. | 

### CREATE VIEW<a name="w3ab1c37b7c21c10"></a>

CREATE VIEW statements are converted automatically except for the following clauses\. 


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
| SCHEMABINDING | No | AWS Schema Conversion Tool ignores this clause\. | 
| ENCRYPTION | No | AWS Schema Conversion Tool ignores this clause\. | 
| VIEW\_METADATA | No | AWS Schema Conversion Tool ignores this clause\. | 

## Cursors<a name="w3ab1c37b7c23"></a>


+ [DECLARE CURSOR](#w3ab1c37b7c23b4)

### DECLARE CURSOR<a name="w3ab1c37b7c23b4"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
| LOCAL | Yes | Change the global cursor to a local cursor, or revise your code so it doesn't require global cursors\. | 
| GLOBAL | No | Setting this option corresponds to the typical behavior of cursors in MySQL, so the AWS Schema Conversion Tool skips this option during conversion\. | 
| FORWARD\_ONLY | Partial | Revise your code to eliminate cursors with the SCROLL option\. | 
| SCROLL | No |  | 
| STATIC | Yes | The membership and order of rows never changes for cursors in MySQL, so the AWS Schema Conversion Tool skips this option during conversion\. Verify that the converted schema behavior is acceptable\. | 
| KEYSET | Partial | Revise your code to eliminate dynamic cursors\. | 
| DYNAMIC | No | Setting this option corresponds to the typical behavior of cursors in MySQL, so the AWS Schema Conversion Tool skips this option during conversion\. | 
| FAST\_FORWARD | Yes | All MySQL cursors are read\-only, so the AWS Schema Conversion Tool skips this option during conversion\. | 
| READ\_ONLY | Yes | MySQL doesn't support the option SCROLL\_LOCKS, so the AWS Schema Conversion Tool ignores this option during conversion\. Verify that the converted schema behavior is acceptable\. | 
| SCROLL\_LOCKS | Partial | MySQL doesn't support the option OPTIMISTIC, so the AWS Schema Conversion Tool ignores this option during conversion\. Verify that the converted schema behavior is acceptable\. | 
| OPTIMISTIC | Partial | MySQL doesn't support the option TYPE\_WARNING, so the AWS Schema Conversion Tool ignores this option during conversion\. Verify that the converted schema behavior is acceptable\. | 
| TYPE\_WARNING | Partial | Change the global cursor to a local cursor, or revise your code so it doesn't require global cursors\. | 

## Related Topics<a name="w3ab1c37b7c25"></a>

+ [What Is the AWS Schema Conversion Tool?](Welcome.md)

+ [Getting Started with the AWS Schema Conversion Tool](CHAP_SchemaConversionTool.GettingStarted.md)

+ [Installing, Verifying, and Updating the AWS Schema Conversion Tool](CHAP_SchemaConversionTool.Installing.md)