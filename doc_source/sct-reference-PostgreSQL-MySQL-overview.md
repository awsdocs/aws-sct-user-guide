# PostgreSQL to MySQL Conversion Reference<a name="sct-reference-PostgreSQL-MySQL-overview"></a>

## AGGREGATE FUNCTION<a name="sct-reference-PostgreSQL-MySQL-aggregate-function"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  bit\_and, bit\_or  |   [Issue 6680: Check working of function with null values](sct-reference-PostgreSQL-MySQL-AGGREGATEFUNCTION.md#sct-reference-6680)   |  Perform a manual conversion\.  | 
|  OVER/ORDER BY/WITHIN GROUP/FILTER  |   [Issue 6678: MySQL doesn't support function %s with OVER/ORDER BY/WITHIN GROUP/FILTER clause](sct-reference-PostgreSQL-MySQL-AGGREGATEFUNCTION.md#sct-reference-6678)   |  Perform a manual conversion\.  | 

## ALTER<a name="sct-reference-PostgreSQL-MySQL-alter-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  ALTER  |   [Issue 6676: Automatic conversion of the ALTER statement isn't supported](sct-reference-PostgreSQL-MySQL-ALTER.md#sct-reference-6676)   |  Perform a manual conversion\.  | 

## Arithmetic Operators<a name="sct-reference-PostgreSQL-MySQL-arithmetic-operators-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  Arithmetic operators and string type  |   [Issue 6681: Unable to perform an automated migration of arithmetic operations with string and other types](sct-reference-PostgreSQL-MySQL-Arithmeticoperators.md#sct-reference-6681)   |  Make cast operands to the expected type\.  | 

## ARRAY<a name="sct-reference-PostgreSQL-MySQL-array-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  ARRAY  |   [Issue 6608: MySQL doesn't support arrays](sct-reference-PostgreSQL-MySQL-ARRAY.md#sct-reference-6608)   |  Perform a manual conversion\.  | 

## Buildin function<a name="sct-reference-PostgreSQL-MySQL-buildin-function-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  DateTime  |   [Issue 6677: MySQL does not support time zone](sct-reference-PostgreSQL-MySQL-Buildinfunction.md#sct-reference-6677)   |  Perform a manual conversion\.  | 

## BUILT\-IN SQL FUNCTIONS<a name="sct-reference-PostgreSQL-MySQL-built-in-sql-functions-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  BUILT\-IN SQL FUNCTIONS  |   [Issue 6667: MySQL doesn't support the %s function](sct-reference-PostgreSQL-MySQL-BUILT-INSQLFUNCTIONS.md#sct-reference-6667)   |  Create a user\-defined function\.  | 

## CREATE<a name="sct-reference-PostgreSQL-MySQL-create-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  CREATE  |   [Issue 6094: Unable to convert object due to %s not created](sct-reference-PostgreSQL-MySQL-CREATE.md#sct-reference-6094)   |  Review the %s object\.  | 

## CURSOR<a name="sct-reference-PostgreSQL-MySQL-cursor-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  CURSOR with clause NEXT, PRIOR, FIRST, LAST, ABSOLUTE, RELATIVE, FORWARD or BACKWARD  |   [Issue 6639: MySQL doesn't support the direction clause](sct-reference-PostgreSQL-MySQL-CURSOR.md#sct-reference-6639)   |  Perform a manual conversion\.  | 
|  CURSOR with MOVE option  |   [Issue 6640: MySQL doesn't support the MOVE option](sct-reference-PostgreSQL-MySQL-CURSOR.md#sct-reference-6640)   |  Perform a manual conversion\.  | 
|  CURSOR with options SCROLL or NO SCROLL  |   [Issue 6638: MySQL doesn't support the SCROLL option in cursors](sct-reference-PostgreSQL-MySQL-CURSOR.md#sct-reference-6638)   |  Revise your code to eliminate cursors with the SCROLL option\.  | 
|  REFCURSOR  |   [Issue 6337: MySQL doesn't support a variable of REFCURSOR type](sct-reference-PostgreSQL-MySQL-CURSOR.md#sct-reference-6337)   |  Try using temporary tables\.  | 

## Databases<a name="sct-reference-PostgreSQL-MySQL-databases-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  ALTER DATABASE  |   [Issue 6101: MySQL doesn't support this clause in an ALTER DATABASE statement](sct-reference-PostgreSQL-MySQL-Databases.md#sct-reference-6101)   |  Perform a manual conversion\.  | 
|  CREATE DATABASE, DROP DATABASE  |   [Issue 6100: The database\-to\-database migration is not provided](sct-reference-PostgreSQL-MySQL-Databases.md#sct-reference-6100)   |  Use the schema\-to\-database migration plan\.  | 

## DATA TYPES<a name="sct-reference-PostgreSQL-MySQL-datatypes-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  CAST\( \.\.\. AS BIT | BIT VARYING | VARBIT | DECIMAL | NUMERIC | REAL | FLOAT4 | DOUBLE PRECISION | FLOAT8 | CHARACTER | CHAR | CHARACTER VARYING | TEXT | TIME WITH TIME ZONE | TIME\(p\) WITH TIME ZONE | TIMESTAMP WITH TIME ZONE | TIMESTAMP\(p\) WITH TIME \)  |   [Issue 6673: MySQL doesn't support %s type in the CAST function, and a loss of precision or accuracy of data is possible](sct-reference-PostgreSQL-MySQL-DATATYPES.md#sct-reference-6673)   |  Check if the data violates these restrictions\. If so, perform a manual migration\.  | 
|  CAST\( \.\.\. AS BOX | POINT | LINE | LSEG | PATH | POLYGON | CIRCLE | TXID\_SNAPSHOT\)  |   [Issue 6674: MySQL doesn't support %s type in the CAST function](sct-reference-PostgreSQL-MySQL-DATATYPES.md#sct-reference-6674)   |  Check if the data violates these restrictions\. If so, perform a manual migration\.  | 

## DELETE<a name="sct-reference-PostgreSQL-MySQL-delete-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  RETURNING  |   [Issue 6069: MySQL doesn't support the DELETE statement with the RETURNING option](sct-reference-PostgreSQL-MySQL-DELETE.md#sct-reference-6069)   |  To perform this operation, divide the DELETE statement with the RETURNING clause into a DELETE statement with following INSERT statements and use the same key conditions in each SELECT\.  | 
|  WHERE CURRENT OF  |   [Issue 6672: MySQL does not support delete by cursor](sct-reference-PostgreSQL-MySQL-DELETE.md#sct-reference-6672)   |  Perform a manual conversion\.  | 

## Domains<a name="sct-reference-PostgreSQL-MySQL-domains-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  CREATE DOMAIN, ALTER DOMAIN, DROP DOMAIN  |   [Issue 6050: MySQL doesn't support domains](sct-reference-PostgreSQL-MySQL-Domains.md#sct-reference-6050)   |  Perform a manual conversion\.  | 

## DYNAMIC SQL<a name="sct-reference-PostgreSQL-MySQL-dynamic-sql-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  RETURN QUERY EXECUTE  |   [Issue 6334: MySQL doesn't support the dynamic SQL statement RETURN QUERY EXECUTE](sct-reference-PostgreSQL-MySQL-DYNAMICSQL.md#sct-reference-6334)   |  Review and modify the execution string\.  | 

## Error Handling<a name="sct-reference-PostgreSQL-MySQL-error-handling-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  GET \[CURRENT\] DIAGNOSTICS \.\.\. PG\_ CONTEXT  |   [Issue 6665: MySQL doesn't support the GET \[ CURRENT \] DIAGNOSTICS command](sct-reference-PostgreSQL-MySQL-Errorhandling.md#sct-reference-6665)   |  Perform a manual conversion\.  | 
|  GET STACKED DIAGNOSTICS PG\_DATATYPE\_NAME| TABLE\_NAME| SCHEMA\_NAME| PG\_EXCEPTION\_DETAIL| PG\_EXCEPTION\_HINT| PG\_EXCEPTION\_CONTEXT  |   [Issue 6664: MySQL doesn't support the condition information %s](sct-reference-PostgreSQL-MySQL-Errorhandling.md#sct-reference-6664)   |  Perform a manual conversion\.  | 
|  RAISE \[exception\]  |   [Issue 6329: MySQL doesn't support the RAISE exception](sct-reference-PostgreSQL-MySQL-Errorhandling.md#sct-reference-6329)   |  Review the RAISE exception used, and if possible convert it to an exception using the SIGNAL or RESIGNAL statement\.  | 

## EXCEPTIONS<a name="sct-reference-PostgreSQL-MySQL-exceptions-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  EXCEPTIONS  |   [Issue 6342: MySQL doesn't support the %s condition name](sct-reference-PostgreSQL-MySQL-EXCEPTIONS.md#sct-reference-6342)   |  Review the exception used, and if possible convert it to an exception using the SIGNAL or RESIGNAL statement\.  | 

## FROM<a name="sct-reference-PostgreSQL-MySQL-from-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  FROM  |   [Issue 6603: Can't use function in from clause](sct-reference-PostgreSQL-MySQL-FROM.md#sct-reference-6603)   |  Perform a manual conversion\.  | 
|  QUERY  |   [Issue 6682: Can't use the table\-value function in the from clause](sct-reference-PostgreSQL-MySQL-FROM.md#sct-reference-6682)   |  MySQL does not support the table\-value function\.  | 

## FUNCTION<a name="sct-reference-PostgreSQL-MySQL-function-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  language  |   [Issue 6675: Automatic conversion function on %s language isn't supported](sct-reference-PostgreSQL-MySQL-FUNCTION.md#sct-reference-6675)   |  Perform a manual conversion\.  | 
|  RECORD  |   [Issue 6613: Unable to convert a function without OUT parameters returning a RECORD type](sct-reference-PostgreSQL-MySQL-FUNCTION.md#sct-reference-6613)   |  Perform a manual conversion\.  | 

## Functions<a name="sct-reference-PostgreSQL-MySQL-functions-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  RETURN NEXT  |   [Issue 6604: MySQL doesn't support RETURN NEXT clause](sct-reference-PostgreSQL-MySQL-Functions.md#sct-reference-6604)   |  Perform a manual conversion\.  | 
|  VARIADIC  |   [Issue 6605: MySQL doesn't support VARIADIC mode of an argument](sct-reference-PostgreSQL-MySQL-Functions.md#sct-reference-6605)   |  Perform a manual conversion\.  | 

## Indexes<a name="sct-reference-PostgreSQL-MySQL-indexes-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  CREATE INDEX: GiST, SPGiST, Gin methods  |   [Issue 6091: MySQL doesn't support %s index method](sct-reference-PostgreSQL-MySQL-Indexes.md#sct-reference-6091)   |  Perform a manual conversion\.  | 
|  Expression\-based indexes  |   [Issue 6090: MySQL doesn't support indexes on expressions](sct-reference-PostgreSQL-MySQL-Indexes.md#sct-reference-6090)   |  Perform a manual conversion\.  | 
|  Ordered indexes  |   [Issue 6092: MySQL doesn't support explicit sort ordering in the index definition](sct-reference-PostgreSQL-MySQL-Indexes.md#sct-reference-6092)   |  If default \(ascending\) sort order in the index might cause performance degradation, perform a manual conversion or rewrite statements supposed to use it\.  | 
|  Partial indexes  |   [Issue 6093: MySQL doesn't support partial indexes](sct-reference-PostgreSQL-MySQL-Indexes.md#sct-reference-6093)   |  If the full index might cause performance degradation, perform a manual conversion\.  | 

## INSERT<a name="sct-reference-PostgreSQL-MySQL-insert-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  RETURNING  |   [Issue 6172: MySQL doesn't support the INSERT statement with the RETURNING option](sct-reference-PostgreSQL-MySQL-INSERT.md#sct-reference-6172)   |  To perform this operation, divide the INSERT statement with the RETURNING clause into an INSERT statement with following SELECT statements and use the same key conditions in each SELECT\. You can also use the last value that was generated by AUTO\_INCREMENT column in the key condition\.  | 

## INTERSECT, EXCEPT<a name="sct-reference-PostgreSQL-MySQL-intersect-except-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  INTERSECT, EXCEPT  |   [Issue 6612: Query with INTERSECT/EXCEPT ALL operator was transformed](sct-reference-PostgreSQL-MySQL-INTERSECT-EXCEPT.md#sct-reference-6612)   |  Perform a manual conversion\.  | 

## LABEL<a name="sct-reference-PostgreSQL-MySQL-label-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  LABEL  |   [Issue 6344: MySQL doesn't support labeled variables](sct-reference-PostgreSQL-MySQL-LABEL.md#sct-reference-6344)   |  Try rewriting variables without using labels\.  | 

## LIMIT<a name="sct-reference-PostgreSQL-MySQL-limit-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  LIMIT, OFFSET  |   [Issue 6611: LIMIT/OFFSET option was omitted](sct-reference-PostgreSQL-MySQL-LIMIT.md#sct-reference-6611)   |  Perform a manual conversion\.  | 

## Materialized Views<a name="sct-reference-PostgreSQL-MySQL-materialized-views-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  CREATE MATERIALIZED VIEW  |   [Issue 6130: MySQL doesn't support materialized views; the source materialized view is converted to a table with triggers](sct-reference-PostgreSQL-MySQL-Materializedviews.md#sct-reference-6130)   |  If this migration approach is unsuitable for any reason, perform a manual conversion\.  | 

## Message from Stored Routines<a name="sct-reference-PostgreSQL-MySQL-message-from-stored-routines-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  RAISE DEBUG|LOG|INFO|NOTICE|WARNING  |   [Issue 6332: MySQL doesn't support the RAISE statement to report messages](sct-reference-PostgreSQL-MySQL-Messagefromstoredroutines.md#sct-reference-6332)   |  Try using INSERT in the log table\. To do this, you must add code into AWS\_POSTGRESQL\_EXT\.RAISE\_DEBUG, AWS\_POSTGRESQL\_EXT\.RAISE\_LOG, AWS\_POSTGRESQL\_EXT\.RAISE\_INFO, AWS\_POSTGRESQL\_EXT\.RAISE\_NOTICE, and AWS\_POSTGRESQL\_EXT\.RAISE\_WARNING\.  | 

## Operators and Date Functions<a name="sct-reference-PostgreSQL-MySQL-operators-and-date-functions-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  Date/Time Operators  |   [Issue 6660: Unable to convert the %s operation with the interval value as one or more arguments](sct-reference-PostgreSQL-MySQL-OperatorsandDateFunctions.md#sct-reference-6660)   |  Perform a manual conversion\.  | 
|  Date/Time Operators  |   [Issue 6661: The operation will return the number of days instead of the interval value](sct-reference-PostgreSQL-MySQL-OperatorsandDateFunctions.md#sct-reference-6661)   |  Check if the resulting type meets your requirements\. If it doesn't, perform a manual conversion\.  | 
|  Date/Time Operators  |   [Issue 6662: Unsupported format for the interval's value](sct-reference-PostgreSQL-MySQL-OperatorsandDateFunctions.md#sct-reference-6662)   |  Currently, the only supported format is a SQL ANSI format for interval literals\. Perform a manual conversion\.  | 

## ORDER BY<a name="sct-reference-PostgreSQL-MySQL-order-by-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  NULLS FIRST|LAST  |   [Issue 6610: AI nulls first/last transformation was performed](sct-reference-PostgreSQL-MySQL-ORDERBY.md#sct-reference-6610)   |  Perform a manual conversion\.  | 
|  USING  |   [Issue 6609: ORDER option was omitted because MySQL doesn't support key word USING in order by clause](sct-reference-PostgreSQL-MySQL-ORDERBY.md#sct-reference-6609)   |  Perform a manual conversion\.  | 

## Parser Error<a name="sct-reference-PostgreSQL-MySQL-parser-error-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  Parser Error  |   [Issue 6663: Unable to resolve the object](sct-reference-PostgreSQL-MySQL-ParserError.md#sct-reference-6663)   |  Verify if object %s is present in the database\. If it isn't, check the object name or add the object\. If the object is present, transform the code manually\.  | 

## Patterns<a name="sct-reference-PostgreSQL-MySQL-patterns-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  SIMILAR TO  |   [Issue 6607: Could not convert pattern to MySQL version; check pattern manually](sct-reference-PostgreSQL-MySQL-Patterns.md#sct-reference-6607)   |  Perform a manual conversion\.  | 

## ROW/RECORD Type<a name="sct-reference-PostgreSQL-MySQL-row-record-type-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  ROW\(\)  |   [Issue 6606: MySQL doesn't support ROW\(\) function with any, some, or all predicates](sct-reference-PostgreSQL-MySQL-ROW-RECORDtype.md#sct-reference-6606)   |  Perform a manual conversion\.  | 
|  ROW/RECORD  |   [Issue 6668: MySQL doesn't support ROW/RECORD type](sct-reference-PostgreSQL-MySQL-ROW-RECORDtype.md#sct-reference-6668)   |  Perform a manual conversion\.  | 

## Select<a name="sct-reference-PostgreSQL-MySQL-SELECT-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  DISTINCT ON  |      |  Perform a manual conversion\.  | 
|  ONLY | \*  |      |  Perform a manual conversion\.  | 
|  DateTime  |   [Issue 6679: Value don't fixed on start transaction ](sct-reference-PostgreSQL-MySQL-SELECT.md#sct-reference-6679)   |  Review your code, and if needed use a local variable  | 

## SELECT INTO<a name="sct-reference-PostgreSQL-MySQL-select-into-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  SELECT INTO  |   [Issue 6666: Transformation of not strict into clause was performed](sct-reference-PostgreSQL-MySQL-SELECTINTO.md#sct-reference-6666)   |  Perform a manual conversion\.  | 

## SELECT, UPDATE, INSERT, DELETE<a name="sct-reference-PostgreSQL-MySQL-select-update-insert-delete-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  WITH  |   [Issue 6127: MySQL doesn't support the WITH RECURSIVE clause](sct-reference-PostgreSQL-MySQL-SELECT-UPDATE-INSERT-DELETE.md#sct-reference-6127)   |  Use a stored procedure to prepare data, or rewrite your query to avoid the WITH clause\.  | 

## Sequences<a name="sct-reference-PostgreSQL-MySQL-sequences-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  CREATE SEQUENCE, ALTER SEQUENCE, DROP SEQUENCE  |   [Issue 6060: MySQL doesn't support sequences](sct-reference-PostgreSQL-MySQL-Sequences.md#sct-reference-6060)   |  Perform a manual conversion\.  | 

## SQL Functions<a name="sct-reference-PostgreSQL-MySQL-sql-functions-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  COLLATION  |   [Issue 6343: MySQL doesn't support the COLLATE option; automatic conversion cannot be performed](sct-reference-PostgreSQL-MySQL-SQLFunctions.md#sct-reference-6343)   |  You must use the COLLATION settings that were assigned when the database was created\.  | 

## Table Columns<a name="sct-reference-PostgreSQL-MySQL-table-columns-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  Application data types: CIDR, INET, MACADDR, UUID, XML, JSON, JSONB, TSVECTOR, TSQUERY  |   [Issue 6006: MySQL doesn't support %s type](sct-reference-PostgreSQL-MySQL-TableColumns.md#sct-reference-6006)   |  Check the target data type and correct it if inappropriate\.  | 
|  ARRAY  |   [Issue 6008: MySQL doesn't support array types for table column definition](sct-reference-PostgreSQL-MySQL-TableColumns.md#sct-reference-6008)   |  Perform a manual conversion\.  | 
|  CIRCLE  |   [Issue 6011: MySQL doesn't support CIRCLE as a spatial type; the approximated results of BUFFER function of POLYGON data type is used to perform a conversion](sct-reference-PostgreSQL-MySQL-TableColumns.md#sct-reference-6011)   |  If the approximated representation is not suitable for any reason, perform a manual conversion\.  | 
|  DECIMAL types  |   [Issue 6002: MySQL doesn't support %s with precision more than 65 digits and scale more than 30 digits; the loss of precision or accuracy of data is possible](sct-reference-PostgreSQL-MySQL-TableColumns.md#sct-reference-6002)   |  Check, if the data violates these restrictions\. If so, perform a manual migration\.  | 
|  INTERVAL  |   [Issue 6005: MySQL doesn't support INTERVAL type](sct-reference-PostgreSQL-MySQL-TableColumns.md#sct-reference-6005)   |  Perform a manual conversion\.  | 
|  LINE  |   [Issue 6010: MySQL doesn't support infinite lines; a LINESTRING with two points on the line is used for conversion](sct-reference-PostgreSQL-MySQL-TableColumns.md#sct-reference-6010)   |  If the two\-pointed representation is not suitable for any reason, perform a manual conversion\.  | 
|  Range types  |   [Issue 6009: MySQL doesn't support range types](sct-reference-PostgreSQL-MySQL-TableColumns.md#sct-reference-6009)   |  Perform a manual conversion\.  | 
|  Serial types: BIGSERIAL / SERIAL8 / SERIAL / SERIAL4 / SMALLSERIAL / SERIAL2  |   [Issue 6001: Unable to provide full migration for auto\-increment table columns](sct-reference-PostgreSQL-MySQL-TableColumns.md#sct-reference-6001)   |  MySQL supports only one auto\-increment column per table and it must be a key\. Decide whether the column should be an auto\-incremented key or not, and if it should, alter it manually\.  | 
|  TIME WITH TIME ZONE  |   [Issue 6003: MySQL doesn't support time zone information for %s type](sct-reference-PostgreSQL-MySQL-TableColumns.md#sct-reference-6003)   |  Perform a manual conversion\.  | 
|  Timestamps with time zone  |   [Issue 6004: MySQL doesn't support time zone information for %s type](sct-reference-PostgreSQL-MySQL-TableColumns.md#sct-reference-6004)   |  Perform a manual conversion\. If the time zone information has no value, you can choose DATETIME\(6\) as a target data type\. Otherwise, try to convert the data into TIMESTAMP\(6\), taking into account the value of time\_zone server setting\.  | 

## Table Columns, Function Arguments, Local Variables<a name="sct-reference-PostgreSQL-MySQL-table-columns-function-arguments-local-variables-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  Bit strings  |   [Issue 6012: Converted bit strings are right\-padded by zero bits to full\-byte length](sct-reference-PostgreSQL-MySQL-TableColumns-FunctionArguments-LocalVariables.md#sct-reference-6012)   |  If the approximated representation is not suitable for any reason, perform a manual conversion\.  | 

## Tables<a name="sct-reference-PostgreSQL-MySQL-tables-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  Constraints  |   [Issue 6111: MySQL doesn't support deferrable constraints](sct-reference-PostgreSQL-MySQL-Tables.md#sct-reference-6111)   |  Check your schema and ensure that non\-deferrable constraints can provide the necessary level of integrity\. Otherwise, perform a manual conversion on the constraints\.  | 
|  Constraints  |   [Issue 6112: MySQL doesn't support exclusion constraints](sct-reference-PostgreSQL-MySQL-Tables.md#sct-reference-6112)   |  Perform a manual conversion of the exclusion constraint to provide the same level of data integrity\.  | 
|  Constraints  |   [Issue 6113: MySQL doesn't support check constraints; the source constraint is converted to a conditional error raising in triggers](sct-reference-PostgreSQL-MySQL-Tables.md#sct-reference-6113)   |  If the approach with triggers is unsuitable, perform a manual conversion of the check constraint to provide the same level of data integrity\.  | 
|  Constraints  |   [Issue 6114: MySQL doesn't support SET DEFAULT as a referential action in foreign keys](sct-reference-PostgreSQL-MySQL-Tables.md#sct-reference-6114)   |  Check that SET NULL is an appropriate referential action, otherwise perform a manual conversion of the constraint\.  | 
|  Constraints  |   [Issue 6115: MySQL doesn't support expressions in DEFAULT constraints, so they are converted to a BEFORE INSERT trigger](sct-reference-PostgreSQL-MySQL-Tables.md#sct-reference-6115)   |  Right now, explicitly inserted NULL values are not distinguished from those specially omitted to use default values\. Also, updating values to DEFAULT is not supported at the present time\. If you need that functionality, perform a manual conversion\.  | 
|  Constraints  |   [Issue 6117: Unable to keep the NOT NULL constraint for %s column while converting its DEFAULT constraint based on an expression](sct-reference-PostgreSQL-MySQL-Tables.md#sct-reference-6117)   |  Due to the transformation of the DEFAULT constraint based on an expression into the part of a trigger, the NOT NULL constraint is converted as another part of the same trigger\.  | 
|  Tables without columns  |   [Issue 6110: MySQL doesn't support tables without columns](sct-reference-PostgreSQL-MySQL-Tables.md#sct-reference-6110)   |  Perform a manual conversion\.  | 
|  Typed tables  |   [Issue 6107: MySQL doesn't support unlogged tables](sct-reference-PostgreSQL-MySQL-Tables.md#sct-reference-6107)   |  If a regular table is unsuitable, perform a manual conversion\.  | 
|  Typed tables  |   [Issue 6108: MySQL doesn't support inherited tables](sct-reference-PostgreSQL-MySQL-Tables.md#sct-reference-6108)   |  Perform a manual conversion\.  | 
|  Typed tables  |   [Issue 6109: MySQL doesn't support typed tables](sct-reference-PostgreSQL-MySQL-Tables.md#sct-reference-6109)   |  Perform a manual conversion\.  | 

## Triggers<a name="sct-reference-PostgreSQL-MySQL-triggers-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  Conditional triggers  |   [Issue 6083: MySQL doesn't support conditional triggers that fire on updates of particular column\(s\); a conversion will omit such a condition](sct-reference-PostgreSQL-MySQL-Triggers.md#sct-reference-6083)   |  If a resulting trigger must fire for updates of only the particular column\(s\), perform a manual conversion\.  | 
|  Constraint triggers  |   [Issue 6082: MySQL doesn't support constraint triggers](sct-reference-PostgreSQL-MySQL-Triggers.md#sct-reference-6082)   |  Perform a manual conversion\.  | 
|  Disabled triggers  |   [Issue 6087: MySQL doesn't support disabling triggers](sct-reference-PostgreSQL-MySQL-Triggers.md#sct-reference-6087)   |  Perform a manual conversion\.  | 
|  DROP TRIGGER  |   [Issue 6086: Unable to automatically transform dropping a trigger](sct-reference-PostgreSQL-MySQL-Triggers.md#sct-reference-6086)   |  Perform a manual conversion\.  | 
|  Instead\-of triggers  |   [Issue 6084: MySQL doesn't support INSTEAD OF triggers](sct-reference-PostgreSQL-MySQL-Triggers.md#sct-reference-6084)   |  Perform a manual conversion\.  | 
|  Multiple triggers on the same event  |   [Issue 6085: MySQL doesn't support multiple triggers on the same event; triggers are merged into one in alphabetical order by trigger name](sct-reference-PostgreSQL-MySQL-Triggers.md#sct-reference-6085)   |  If a result of merging is unappropriate, perform a manual conversion\.  | 
|  One trigger on multiple events  |   [Issue 6081: MySQL doesn't support triggers firing on multiple events; such a trigger is converted to multiple single\-event triggers with the same body](sct-reference-PostgreSQL-MySQL-Triggers.md#sct-reference-6081)   |  If this migration approach is not suitable for the trigger, perform a manual conversion\.  | 
|  Statement\-level triggers  |   [Issue 6080: MySQL doesn't support statement\-level triggers](sct-reference-PostgreSQL-MySQL-Triggers.md#sct-reference-6080)   |  Perform a manual conversion\.  | 
|  Trigger functions  |   [Issue 6650: Unable to convert the statement with TG\_ARGV automatically](sct-reference-PostgreSQL-MySQL-Triggers.md#sct-reference-6650)   |  Perform a manual conversion\.  | 
|  Trigger functions  |   [Issue 6651: Unsupported using of RETURN statement in the trigger converted to LEAVE statement](sct-reference-PostgreSQL-MySQL-Triggers.md#sct-reference-6651)   |  Check flow of execution and perform a manual conversion if necessary\.  | 
|  Trigger functions  |   [Issue 6652: MySQL doesn't support OLD record in triggers on INSERT or NEW record in triggers on DELETE](sct-reference-PostgreSQL-MySQL-Triggers.md#sct-reference-6652)   |  Check, if NULL instead of a field of the unsupported record is appropriate\.  | 
|  Trigger on TRUNCATE event  |   [Issue 6088: MySQL doesn't support TRUNCATE event for triggers](sct-reference-PostgreSQL-MySQL-Triggers.md#sct-reference-6088)   |  Perform a manual conversion\.  | 

## UDT<a name="sct-reference-PostgreSQL-MySQL-udt-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  CREATE TYPE, ALTER TYPE, DROP TYPE  |   [Issue 6120: MySQL doesn't support user\-defined data types](sct-reference-PostgreSQL-MySQL-UDT.md#sct-reference-6120)   |  Perform a manual conversion\.  | 

## Unknown<a name="sct-reference-PostgreSQL-MySQL-unknown-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  Unknown  |   [Issue 6013: This syntactic element conversion is not supported yet](sct-reference-PostgreSQL-MySQL-Unknown.md#sct-reference-6013)   |  Perform a manual conversion\.  | 

## UPDATE<a name="sct-reference-PostgreSQL-MySQL-update-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  FROM  |   [Issue 6669: FROM clause was rewritten](sct-reference-PostgreSQL-MySQL-UPDATE.md#sct-reference-6669)   |  Perform a manual conversion\.  | 
|  RETURNING  |   [Issue 6066: MySQL doesn't support the UPDATE statement with the RETURNING option](sct-reference-PostgreSQL-MySQL-UPDATE.md#sct-reference-6066)   |  To perform this operation, divide the UPDATE statement with the RETURNING clause into an UPDATE statement with following INSERT statements that have the specified key conditions in the SELECT part\.  | 
|  WHERE CURRENT OF  |   [Issue 6670: MySQL does not support update by cursor](sct-reference-PostgreSQL-MySQL-UPDATE.md#sct-reference-6670)   |  Perform a manual conversion\.  | 

## User\-Defined Aggregate Functions<a name="sct-reference-PostgreSQL-MySQL-user-defined-aggregate-functions-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  CREATE AGGREGATE, ALTER AGREGGATE, DROP AGREGGATE  |   [Issue 6140: Unable to convert user\-defined aggregate statements](sct-reference-PostgreSQL-MySQL-User-definedaggregatefunctions.md#sct-reference-6140)   |  Perform a manual conversion\.  | 

## VIEW<a name="sct-reference-PostgreSQL-MySQL-view-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  QUERY  |   [Issue 6076: The SELECT statement cannot contain a subquery in the FROM clause](sct-reference-PostgreSQL-MySQL-VIEW.md#sct-reference-6076)   |  Rewrite the view query without a subquery, or create an auxiliary table for the subquery\.  | 

## Views<a name="sct-reference-PostgreSQL-MySQL-views-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  Default values for the view's columns  |   [Issue 6072: MySQL doesn't support default values for the view's column](sct-reference-PostgreSQL-MySQL-Views.md#sct-reference-6072)   |  If the same functionality is necessary, perform a manual conversion\.  | 
|  Row\-level secured views  |   [Issue 6071: MySQL doesn't support row\-level security](sct-reference-PostgreSQL-MySQL-Views.md#sct-reference-6071)   |  If the same functionality is necessary, perform a manual conversion\.  | 
|  Temporary views  |   [Issue 6070: MySQL doesn't support temporary views or views on temporary tables](sct-reference-PostgreSQL-MySQL-Views.md#sct-reference-6070)   |  Perform a manual conversion\.  | 

## Related Topics<a name="sct-reference-PostgreSQL-MySQL-related"></a>

+  [AWS Schema Conversion Tool Reference](CHAP_SchemaConversionTool.Reference.md) 

+  [What Is the AWS Schema Conversion Tool?](Welcome.md) 