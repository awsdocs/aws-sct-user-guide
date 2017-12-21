# Oracle to PostgreSQL Conversion Reference<a name="sct-reference-Oracle-PostgreSQL"></a>

Use the following sections to get information on the types of issues you might encounter during an Oracle to PostgreSQL conversion\. Choose the link in the Issue column to get more detailed resolution information about the issue if it is available\.

## Build\_in\_services<a name="sct-reference-Oracle-PostgreSQL-build_in_services-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  UTL\_SMTP DBMS\_JOB  |   [Issue 5590: The function was converted as procedure](sct-reference-Oracle-PostgreSQL-Build_in_services.md#sct-reference-5590)   |  Can't return a reply because this functionality is asynchronous\.  | 

## Built\-In SQL Functions<a name="sct-reference-Oracle-PostgreSQL-built-in-sql-functions-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  DateTime function  |   [Issue 5584: The function %s depends on the time zone setting](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5584)   |  Review the transformed code, and set time zone manually if necessary\.  | 
|  FUNCTION  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   |  Use suitable function or create user defined function\.  | 
|  GREATEST\(exp, exp2, \.\.\.\)  |   [Issue 5271: The Oracle GREATEST function and PostgreSQL GREATEST function might give different results](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5271)   |  Review your transformed code and modify it if necessary\. Change an argument's type if necessary\.  | 
|  LEAST\(exp, exp2, \.\.\.\)  |   [Issue 5272: The Oracle LEAST function and PostgreSQL LEAST function might give different results](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5272)   |  Review your transformed code and modify it if necessary\. Change an argument's type if necessary\.  | 
|  TO\_CHAR, TO\_DATE, TO\_NUMBER  |   [Issue 5579: The second parameter of %s function can be processed incorrectly](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5579)   |  Check converted code and make manual corrections if it's necessary\.  | 

## CREATE<a name="sct-reference-Oracle-PostgreSQL-create-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|   |   [Issue 5099: Unable convert object due to %s not created](sct-reference-Oracle-PostgreSQL-CREATE.md#sct-reference-5099)   |  Review the %s object\.  | 
|   |   [Issue 5332: The object has references on the object in %s schema](sct-reference-Oracle-PostgreSQL-CREATE.md#sct-reference-5332)   |  Convert the object in %s schema also\.  | 
|  Encrypted Objects  |   [Issue 5582: Encrypted Objects](sct-reference-Oracle-PostgreSQL-CREATE.md#sct-reference-5582)   |  Decrypt the object before conversion\.  | 

## CREATE CONSTRAINT<a name="sct-reference-Oracle-PostgreSQL-create-constraint-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  status=DISABLED  |   [Issue 5326: PostgreSQL doesn't support constraints with the status DISABLED](sct-reference-Oracle-PostgreSQL-CREATECONSTRAINT.md#sct-reference-5326)   |  Drop the constraint\.  | 

## CREATE INDEX<a name="sct-reference-Oracle-PostgreSQL-create-index-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  Creating a Domain Index  |   [Issue 5208: PostgreSQL doesn't support domain indexes](sct-reference-Oracle-PostgreSQL-CREATEINDEX.md#sct-reference-5208)   |  Revise your code and try to use simple index\.  | 
|  Creating a Function\-Based Index  |   [Issue 5555: PostgreSQL doesn't support functional indexes that aren't single\-column](sct-reference-Oracle-PostgreSQL-CREATEINDEX.md#sct-reference-5555)   |  Revise your code and try to use simple index\.  | 
|  Creating an BITMAP Index  |   [Issue 5206: PostgreSQL doesn't support bitmap indexes](sct-reference-Oracle-PostgreSQL-CREATEINDEX.md#sct-reference-5206)   |  Revise your code and try to use simple index\.  | 

## CREATE TABLE<a name="sct-reference-Oracle-PostgreSQL-create-table-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  BFILE Data Type  |   [Issue 5212: PostgreSQL doesn't have a data type BFILE](sct-reference-Oracle-PostgreSQL-CREATETABLE.md#sct-reference-5212)   |  Either store a named file with the data and create a routine that gets that file from the file system, or store the data blob inside your database\.  | 
|  CREATING A PARTITIONED TABLE  |   [Issue 5201: PostgreSQL doesn't support all partition types](sct-reference-Oracle-PostgreSQL-CREATETABLE.md#sct-reference-5201)   |  Perform a manual conversion for the partition types that aren't supported\.  | 
|  CREATING CLUSTERED TABLE  |   [Issue 5199: PostgreSQL doesn't support CLUSTERED TABLE](sct-reference-Oracle-PostgreSQL-CREATETABLE.md#sct-reference-5199)   |  Try using a table with triggers\.  | 
|  CREATING EXTERNAL TABLES  |   [Issue 5200: PostgreSQL doesn't support EXTERNAL TABLES](sct-reference-Oracle-PostgreSQL-CREATETABLE.md#sct-reference-5200)   |  Try using a table\.  | 
|  CREATING GLOBAL TEMPORARY TABLE  |   [Issue 5198: PostgreSQL doesn't support GLOBAL TEMPORARY TABLE](sct-reference-Oracle-PostgreSQL-CREATETABLE.md#sct-reference-5198)   |  Try using a local temporary table\.  | 
|  CREATING OBJECT TABLES  |   [Issue 5196: PostgreSQL doesn't support OBJECT TABLE](sct-reference-Oracle-PostgreSQL-CREATETABLE.md#sct-reference-5196)   |  Revise your code to avoid OBJECT TABLE\.  | 
|  Index\-organized table  |   [Issue 5581: PostgreSQL doesn't support index\-organized table](sct-reference-Oracle-PostgreSQL-CREATETABLE.md#sct-reference-5581)   |  Revise your architecture with a custom solution for the table type\.  | 
|  NESTED TABLE  |   [Issue 5348: PostgreSQL doesn't support NESTED TABLES](sct-reference-Oracle-PostgreSQL-CREATETABLE.md#sct-reference-5348)   |  Revise your code to avoid NESTED TABLE\.  | 
|  ROWID data type  |   [Issue 5550: PostgreSQL doesn't have a data type ROWID](sct-reference-Oracle-PostgreSQL-CREATETABLE.md#sct-reference-5550)   |  Review your transformed code and modify it if necessary\.  | 
|  TABLE WITH VIRTUAL COLUMNS  |   [Issue 5554: PostgreSQL doesn't support virtual columns](sct-reference-Oracle-PostgreSQL-CREATETABLE.md#sct-reference-5554)   |  They were emulated by a trigger\.  | 
|  TIMESTAMP\(n>6\) Data Type  |   [Issue 5213: PostgreSQL expands fractional seconds support for TIME, DATETIME, and TIMESTAMP values, with up to microseconds \(6 digits\) of precision](sct-reference-Oracle-PostgreSQL-CREATETABLE.md#sct-reference-5213)   |  Review your transformed code and modify it if necessary to avoid a loss of accuracy\.  | 
|  TIMESTAMP\(n>6\) WITH TIME ZONE data type  |   [Issue 5552: PostgreSQL expands fractional seconds support for TIME, DATETIME, and TIMESTAMP values, with up to microseconds \(6 digits\) of precision](sct-reference-Oracle-PostgreSQL-CREATETABLE.md#sct-reference-5552)   |  Review your transformed code and modify it if necessary to avoid a loss of accuracy\.  | 
|  TIMESTAMP\(n>6\) WITH LOCAL TIME ZONE data type  |   [Issue 5553: PostgreSQL expands fractional seconds support for TIME, DATETIME, and TIMESTAMP values, with up to microseconds \(6 digits\) of precision](sct-reference-Oracle-PostgreSQL-CREATETABLE.md#sct-reference-5553)   |  Review your transformed code and modify it if necessary to avoid a loss of accuracy\.  | 
|  UROWID data type  |   [Issue 5551: PostgreSQL doesn't have a data type UROWID](sct-reference-Oracle-PostgreSQL-CREATETABLE.md#sct-reference-5551)   |  Review your transformed code and modify it if necessary\.  | 

## CREATE TYPE<a name="sct-reference-Oracle-PostgreSQL-create-type-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  OBJECT TYPE  |   [Issue 5572: PostgreSQL doesn't support object type methods](sct-reference-Oracle-PostgreSQL-CREATETYPE.md#sct-reference-5572)   |  Revise your architecture with a custom solution for the user type\.  | 

## CURSOR<a name="sct-reference-Oracle-PostgreSQL-cursor-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  Cursor attributes  |   [Issue 5084: PostgreSQL doesn't support the cursor attribute %ISOPEN](sct-reference-Oracle-PostgreSQL-CURSOR.md#sct-reference-5084)   |  Revise how you are using this attribute in your code\.  | 
|  TYPE \.\. IS REF CURSOR  |   [Issue 5226: PostgreSQL doesn't support TYPE \.\.\. IS REF CURSOR](sct-reference-Oracle-PostgreSQL-CURSOR.md#sct-reference-5226)   |  Change the function to a stored procedure, and try using a table to store results\.  | 

## Datetime Expressions<a name="sct-reference-Oracle-PostgreSQL-datetime-expressions-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  at local at time zone  |   [Issue 5594: PostgreSQL doesn't support %s datetime expression\. The loss of precision and/or accuracy of data is possible](sct-reference-Oracle-PostgreSQL-DatetimeExpressions.md#sct-reference-5594)   |  Check, if the data violates these restrictions\. If so, perform a manual migration\.  | 

## DELETE<a name="sct-reference-Oracle-PostgreSQL-delete-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  ERROR LOG  |   [Issue 5067: PostgreSQL doesn't support the DELETE statement with the ERROR LOG option](sct-reference-Oracle-PostgreSQL-DELETE.md#sct-reference-5067)   |  You can add error records by inserting them into the log in the exception block\. Iterate through the errors in the exception block, add them to the log, and use the EXIT command when finished\.  | 
|  PARTITION  |   [Issue 5098: PostgreSQL doesn't support the DELETE statement for a PARTITION](sct-reference-Oracle-PostgreSQL-DELETE.md#sct-reference-5098)   |  Either insert data into the overlying partition, or perform a manual conversion using the DELETE statement\.  | 
|  QUERY  |   [Issue 5068: PostgreSQL doesn't support the DELETE statement for a subquery](sct-reference-Oracle-PostgreSQL-DELETE.md#sct-reference-5068)   |  Perform this operation on the underlying tables instead\.  | 

## DYNAMIC SQL<a name="sct-reference-Oracle-PostgreSQL-dynamic-sql-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  BULK COLLECT  |   [Issue 5088: PostgreSQL doesn't support the EXECUTE IMMEDIATE statement with BULK COLLECT](sct-reference-Oracle-PostgreSQL-DYNAMICSQL.md#sct-reference-5088)   |  Perform a manual conversion\.  | 
|  EXECUTE IMMEDIATE  |   [Issue 5334: PostgreSQL doesn't support the dynamic SQL statement](sct-reference-Oracle-PostgreSQL-DYNAMICSQL.md#sct-reference-5334)   |  Review and modify the execution string\.  | 
|  RETURNING BULK COLLECT INTO  |   [Issue 5087: PostgreSQL doesn't support the RETURNING BULK COLLECT INTO clause](sct-reference-Oracle-PostgreSQL-DYNAMICSQL.md#sct-reference-5087)   |  Perform a manual conversion\.  | 

## EXCEPTION<a name="sct-reference-Oracle-PostgreSQL-exception-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  ACCESS\_INTO\_NULL  |   [Issue 5561: PostgreSQL doesn't support the ACCESS\_INTO\_NULL exception](sct-reference-Oracle-PostgreSQL-EXCEPTION.md#sct-reference-5561)   |  Review the exception used, and if possible convert it to another condition\.  | 
|  COLLECTION\_IS\_NULL  |   [Issue 5562: PostgreSQL doesn't support the COLLECTION\_IS\_NULL exception](sct-reference-Oracle-PostgreSQL-EXCEPTION.md#sct-reference-5562)   |  Review the exception used, and if possible convert it to another condition\.  | 
|  EMPTY\_BLOCK  |   [Issue 5580: The exception block was emptied after conversion](sct-reference-Oracle-PostgreSQL-EXCEPTION.md#sct-reference-5580)   |  Check converted code and make manual corrections if it is necessary\.  | 
|  EXCEPTION  |   [Issue 5570: PostgreSQL doesn't support exception name declaration](sct-reference-Oracle-PostgreSQL-EXCEPTION.md#sct-reference-5570)   |  Review the exception used, and if possible convert it to another condition\.  | 
|  NO\_DATA\_NEEDED  |   [Issue 5563: PostgreSQL doesn't support the NO\_DATA\_NEEDED exception](sct-reference-Oracle-PostgreSQL-EXCEPTION.md#sct-reference-5563)   |  Review the exception used, and if possible convert it to another condition\.  | 
|  PROGRAM\_ERROR  |   [Issue 5560: PostgreSQL doesn't support the PROGRAM\_ERROR exception](sct-reference-Oracle-PostgreSQL-EXCEPTION.md#sct-reference-5560)   |  Review the exception used, and if possible convert it to another condition\.  | 
|  ROWTYPE\_MISMATCH  |   [Issue 5564: PostgreSQL doesn't support the ROWTYPE\_MISMATCH exception](sct-reference-Oracle-PostgreSQL-EXCEPTION.md#sct-reference-5564)   |  Review the exception used, and if possible convert it to another condition\.  | 
|  SELF\_IS\_NULL  |   [Issue 5565: PostgreSQL doesn't support the SELF\_IS\_NULL exception](sct-reference-Oracle-PostgreSQL-EXCEPTION.md#sct-reference-5565)   |  Review the exception used, and if possible convert it to another condition\.  | 
|  SUBSCRIPT\_BEYOND\_COUNT  |   [Issue 5566: PostgreSQL doesn't support the SUBSCRIPT\_BEYOND\_COUNT exception](sct-reference-Oracle-PostgreSQL-EXCEPTION.md#sct-reference-5566)   |  Review the exception used, and if possible convert it to another condition\.  | 
|  SUBSCRIPT\_OUTSIDE\_LIMIT  |   [Issue 5567: PostgreSQL doesn't support the SUBSCRIPT\_OUTSIDE\_LIMIT exception](sct-reference-Oracle-PostgreSQL-EXCEPTION.md#sct-reference-5567)   |  Review the exception used, and if possible convert it to another condition\.  | 
|  SYS\_INVALID\_ROWID  |   [Issue 5568: PostgreSQL doesn't support the SYS\_INVALID\_ROWID exception](sct-reference-Oracle-PostgreSQL-EXCEPTION.md#sct-reference-5568)   |  Review the exception used, and if possible convert it to another condition\.  | 

## EXPLICIT CURSORS<a name="sct-reference-Oracle-PostgreSQL-explicit-cursors-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  RETURN  |   [Issue 5559: PostgreSQL doesn't support the RETURN TYPE for the cursor](sct-reference-Oracle-PostgreSQL-EXPLICITCURSORS.md#sct-reference-5559)   |  Use cursor declaration without this statement\.  | 

## FUNCTION<a name="sct-reference-Oracle-PostgreSQL-function-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  FUNCTIONS WITH DML \(START TRANSACTION, COMMIT, or ROLLBACK\.\)  |   [Issue 5350: The function can't use statements that explicitly or implicitly begin or end a transaction, such as START TRANSACTION, COMMIT, or ROLLBACK](sct-reference-Oracle-PostgreSQL-FUNCTION.md#sct-reference-5350)   |  Revise you code to implement a transaction control at application side\.  | 

## INSERT<a name="sct-reference-Oracle-PostgreSQL-insert-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  ERROR LOG  |   [Issue 5070: PostgreSQL doesn't support the INSERT statement with the ERROR LOG option](sct-reference-Oracle-PostgreSQL-INSERT.md#sct-reference-5070)   |  You can add error records by inserting them into the log in the exception block\. Iterate through the errors in the exception block, add them to the log, and use the EXIT command when finished\.  | 
|  INSERT with partition\_extension\_clause  |   [Issue 5024: PostgreSQL doesn't support the INSERT statement with partition\_extension\_clause](sct-reference-Oracle-PostgreSQL-INSERT.md#sct-reference-5024)   |  Perform a manual conversion for the partition types that aren't supported\.  | 
|  QUERY  |   [Issue 5071: PostgreSQL doesn't support the INSERT statement for a subquery](sct-reference-Oracle-PostgreSQL-INSERT.md#sct-reference-5071)   |  Perform this operation on the underlying tables instead\.  | 
|  SUBPARTITION  |   [Issue 5090: PostgreSQL doesn't support the INSERT statement for a SUBPARTITION](sct-reference-Oracle-PostgreSQL-INSERT.md#sct-reference-5090)   |  Either insert data into the overlying partition, or perform a manual conversion using the INSERT statement\.  | 

## MATERIALIZED VIEW<a name="sct-reference-Oracle-PostgreSQL-materialized-view-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  CREATE  |   [Issue 5094: PostgreSQL doesn't support a materialized VIEW](sct-reference-Oracle-PostgreSQL-MATERIALIZEDVIEW.md#sct-reference-5094)   |  Revise your code to replace materialized VIEW with another solution\.  | 
|  USING MATERIALIZED VIEW  |   [Issue 5095: PostgreSQL doesn't support using a materialized VIEW](sct-reference-Oracle-PostgreSQL-MATERIALIZEDVIEW.md#sct-reference-5095)   |  Revise your code to replace materialized VIEW with another solution\.  | 

## MERGE<a name="sct-reference-Oracle-PostgreSQL-merge-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  MERGE  |   [Issue 5102: PostgreSQL doesn't support the MERGE statement](sct-reference-Oracle-PostgreSQL-MERGE.md#sct-reference-5102)   |  To achieve the effect of a MERGE statement, use separate INSERT, DELETE, and UPDATE statements\.  | 

## Optimizer Hints<a name="sct-reference-Oracle-PostgreSQL-optimizer-hints-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  HINT  |   [Issue 5103: PostgreSQL doesn't support the %s hint](sct-reference-Oracle-PostgreSQL-OptimizerHints.md#sct-reference-5103)   |  Use PostgreSQL methods for performance tuning\.  | 

## PACKAGES<a name="sct-reference-Oracle-PostgreSQL-packages-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  Package global cursor  |   [Issue 5330: PostgreSQL doesn't support global cursors](sct-reference-Oracle-PostgreSQL-PACKAGES.md#sct-reference-5330)   |  Use another method for this functionality\.  | 
|  Package global user EXCEPTION  |   [Issue 5331: PostgreSQL doesn't support a global user exception](sct-reference-Oracle-PostgreSQL-PACKAGES.md#sct-reference-5331)   |  Use another method for this functionality\.  | 
|  Package user type declaration  |   [Issue 5569: PostgreSQL only supports session variables using SQL standard date and time types](sct-reference-Oracle-PostgreSQL-PACKAGES.md#sct-reference-5569)   |  Revise your architecture with a custom solution for the user type\.  | 

## Parser Error<a name="sct-reference-Oracle-PostgreSQL-parser-error-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  Parser Error  |   [Issue 5293: Unable to resolve the object](sct-reference-Oracle-PostgreSQL-ParserError.md#sct-reference-5293)   |  Verify if object %s is present in the database\. If it isn't, check the object name or add the object\. If the object is present, transform the code manually\.  | 

## PRAGMA<a name="sct-reference-Oracle-PostgreSQL-pragma-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  PRAGMA  |   [Issue 5571: PostgreSQL doesn't support PRAGMA options](sct-reference-Oracle-PostgreSQL-PRAGMA.md#sct-reference-5571)   |  Review the exception used, and if possible convert it to another condition\.  | 

## SELECT<a name="sct-reference-Oracle-PostgreSQL-select-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  BULK COLLECT INTO  |   [Issue 5140: PostgreSQL doesn't support BULK COLLECT INTO](sct-reference-Oracle-PostgreSQL-SELECT.md#sct-reference-5140)   |  You can try to include all of the fields from your table in an INTO clause\.  | 
|  FOR UPDATE SKIP LOCKED  |   [Issue 5139: PostgreSQL doesn't support FOR UPDATE SKIP LOCKED](sct-reference-Oracle-PostgreSQL-SELECT.md#sct-reference-5139)   |  Try using FOR UPDATE without SKIP LOCKED\.  | 
|  FOR UPDATE WAIT  |   [Issue 5144: PostgreSQL doesn't support FOR UPDATE WAIT clauses](sct-reference-Oracle-PostgreSQL-SELECT.md#sct-reference-5144)   |  Try using FOR UPDATE without WAIT\.  | 
|  Hierarchical queries  |   [Issue 5586: Automatic conversion for queries with NOCYCLE clause not supported](sct-reference-Oracle-PostgreSQL-SELECT.md#sct-reference-5586)   |  Perform a manual conversion\.  | 
|  MODEL  |   [Issue 5126: PostgreSQL doesn't support the MODEL statement](sct-reference-Oracle-PostgreSQL-SELECT.md#sct-reference-5126)   |  Revise your code and try using user procedures and temporary tables\.  | 
|  OUTER JOIN  |   [Issue 5585: Automatic conversion of an outer join into a correlation query is not supported](sct-reference-Oracle-PostgreSQL-SELECT.md#sct-reference-5585)   |  Perform a manual conversion\.  | 
|  ROLLUP  |   [Issue 5557: PostgreSQL doesn't support GROUPING SETS, CUBE, and ROLLUP functions](sct-reference-Oracle-PostgreSQL-SELECT.md#sct-reference-5557)   |  It can be emulated using CTE expressions\. GROUPING SETS, CUBE, and ROLLUP ara available in PostgreSQL database v\.9\.5 or higher\.  | 
|  Unsupported statement  |   [Issue 5578: Unable to automatically transform the SELECT statement](sct-reference-Oracle-PostgreSQL-SELECT.md#sct-reference-5578)   |  Try rewriting the statement\.  | 

## SEQUENCE<a name="sct-reference-Oracle-PostgreSQL-sequence-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  STATUS=INVALID  |   [Issue 5574: PostgreSQL doesn't support the sequence's status](sct-reference-Oracle-PostgreSQL-SEQUENCE.md#sct-reference-5574)   |  Check the original sequence for errors, and perform the conversion again\.  | 

## Statements<a name="sct-reference-Oracle-PostgreSQL-statements-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  GOTO  |   [Issue 5335: PostgreSQL doesn't support the GOTO operator](sct-reference-Oracle-PostgreSQL-Statements.md#sct-reference-5335)   |  Perform a manual conversion\.  | 

## Synonym<a name="sct-reference-Oracle-PostgreSQL-synonym-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  private synonym  |   [Issue 5333: This object uses a private synonym](sct-reference-Oracle-PostgreSQL-Synonym.md#sct-reference-5333)   |  Check that a referenced object created after synonym conversion exists\.  | 
|  public synonym  |   [Issue 5592: This object uses a public synonym which references a table, a view, or a function](sct-reference-Oracle-PostgreSQL-Synonym.md#sct-reference-5592)   |  Check that a referenced object created after synonym conversion exists\.  | 
|  public synonym  |   [Issue 5593: This object uses a public synonym which doesn't reference any other objects](sct-reference-Oracle-PostgreSQL-Synonym.md#sct-reference-5593)   |  Check that a referenced object created after synonym conversion exists\.  | 

## System Package<a name="sct-reference-Oracle-PostgreSQL-system-package-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  APEX\_UTIL package  |   [Issue 5503: MySQL does not have functionality similar to %s module](sct-reference-Oracle-PostgreSQL-SystemPackage.md#sct-reference-5503)   |  Try using the Amazon Simple Workflow \(Amazon SWF\)\.  | 
|  DBMS\_DATAPUMP  |   [Issue 5502: MySQL does not have functionality similar to %s module](sct-reference-Oracle-PostgreSQL-SystemPackage.md#sct-reference-5502)   |  Try using the AWS Import/Export Snowball\.  | 
|  DBMS\_JOB module  |   [Issue 5501: MySQL does not have functionality similar to %s module](sct-reference-Oracle-PostgreSQL-SystemPackage.md#sct-reference-5501)   |  Try using the AWS Lambda Service with Scheduled Events\.  | 
|  UTL\_MAIL module  |   [Issue 5500: MySQL does not have functionality similar to %s module](sct-reference-Oracle-PostgreSQL-SystemPackage.md#sct-reference-5500)   |  Try using the Amazon Simple Notification Service \(Amazon SNS\)\.  | 

## TRIGGERS<a name="sct-reference-Oracle-PostgreSQL-triggers-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  action\-type=CALL or PL/SQL  |   [Issue 5313: PostgreSQL doesn't support the action\-type clause](sct-reference-Oracle-PostgreSQL-TRIGGERS.md#sct-reference-5313)   |  Use another method for this functionality\.  | 
|  base\-object\-type=DATABASE  |   [Issue 5415: PostgreSQL doesn't support system triggers](sct-reference-Oracle-PostgreSQL-TRIGGERS.md#sct-reference-5415)   |  Revise your code to replace system triggers with another solution\.  | 
|  base\-object\-type=SCHEMA  |   [Issue 5311: PostgreSQL doesn't support system triggers](sct-reference-Oracle-PostgreSQL-TRIGGERS.md#sct-reference-5311)   |  Revise your code to replace system triggers with another solution\.  | 
|  COMPOUND TRIGGER  |   [Issue 5242: PostgreSQL doesn't support COMPOUND TRIGGER](sct-reference-Oracle-PostgreSQL-TRIGGERS.md#sct-reference-5242)   |  Create a single trigger for each part of the compound trigger\.  | 
|  FOLLOWS | PRECEDES  |   [Issue 5241: PostgreSQL doesn't support the FOLLOWS | PRECEDES clause](sct-reference-Oracle-PostgreSQL-TRIGGERS.md#sct-reference-5241)   |  Try using the FOR EACH ROW trigger\.  | 
|  ON NESTED TABLE  |   [Issue 5240: PostgreSQL doesn't support triggers on nested table columns in views](sct-reference-Oracle-PostgreSQL-TRIGGERS.md#sct-reference-5240)   |  Revise your code to replace nested table with another solution\.  | 
|  REFERENCING NEW AS \.\. OLD AS \.\.  |   [Issue 5238: PostgreSQL doesn't support the REFERENCING clauses](sct-reference-Oracle-PostgreSQL-TRIGGERS.md#sct-reference-5238)   |  Modify references to pseudo\-rows to use OLD and NEW instead\.  | 
|  referencing\-names=PARENT  |   [Issue 5317: PostgreSQL doesn't support the PARENT referencing clause](sct-reference-Oracle-PostgreSQL-TRIGGERS.md#sct-reference-5317)   |  Use another method for this functionality\.  | 
|  status=invalid  |   [Issue 5306: Transformation from invalid trigger](sct-reference-Oracle-PostgreSQL-TRIGGERS.md#sct-reference-5306)   |  Check the original trigger for errors, and perform the conversion again\.  | 
|  UPDATING\(column\_name\)  |   [Issue 5556: PostgreSQL doesn't support conditional predicates](sct-reference-Oracle-PostgreSQL-TRIGGERS.md#sct-reference-5556)   |  Revise your code and try using simple triggers\.  | 

## TRUNCATE TABLE<a name="sct-reference-Oracle-PostgreSQL-truncate-table-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  DROP STORAGE  |   [Issue 5298: PostgreSQL doesn't support the DROP STORAGE clause in the TRUNCATE statement](sct-reference-Oracle-PostgreSQL-TRUNCATETABLE.md#sct-reference-5298)   |  Use TRUNCATE without this option\.  | 
|  PRESERVE MATERIALIZED VIEW LOG  |   [Issue 5300: PostgreSQL doesn't support the PRESERVE clause in the TRUNCATE statement](sct-reference-Oracle-PostgreSQL-TRUNCATETABLE.md#sct-reference-5300)   |  Use TRUNCATE without this option\.  | 
|  PURGE MATERIALIZED VIEW LOG  |   [Issue 5301: PostgreSQL doesn't support the PURGE clause in the TRUNCATE statement](sct-reference-Oracle-PostgreSQL-TRUNCATETABLE.md#sct-reference-5301)   |  Use TRUNCATE without this option\.  | 
|  REUSE STORAGE  |   [Issue 5299: PostgreSQL doesn't support the REUSE STORAGE clause in the TRUNCATE statement](sct-reference-Oracle-PostgreSQL-TRUNCATETABLE.md#sct-reference-5299)   |  Use TRUNCATE without this option\.  | 

## UDT<a name="sct-reference-Oracle-PostgreSQL-udt-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  STATUS=INVALID  |   [Issue 5577: PostgreSQL doesn't support a UDT with body](sct-reference-Oracle-PostgreSQL-UDT.md#sct-reference-5577)   |  Perform a manual conversion\.  | 

## UDT collection\-type arguments<a name="sct-reference-Oracle-PostgreSQL-udt-collection-type-arguments-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  := collection\_type\(\.\.\.\)  |   [Issue 5120: PostgreSQL doesn't support constructors of the "collection" type](sct-reference-Oracle-PostgreSQL-UDTcollection-typearguments.md#sct-reference-5120)   |  Use the "array" type\.  | 
|  EXTEND\(n\[,i\]\)  |   [Issue 5587: PostgreSQL doesn't support EXTEND method with parameters](sct-reference-Oracle-PostgreSQL-UDTcollection-typearguments.md#sct-reference-5587)   |  Perform a manual conversion\.  | 
|  FORALL  |   [Issue 5121: PostgreSQL doesn't support the FORALL statement](sct-reference-Oracle-PostgreSQL-UDTcollection-typearguments.md#sct-reference-5121)   |  Use a FOR LOOP statement\.  | 
|  TYPE \.\. IS TABLE OF\.\.\.  |   [Issue 5118: PostgreSQL doesn't support table type variables](sct-reference-Oracle-PostgreSQL-UDTcollection-typearguments.md#sct-reference-5118)   |  Use the "array" type\.  | 

## Universal<a name="sct-reference-Oracle-PostgreSQL-universal-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  Universal action item  |   [Issue 5339: The %s object is invalid](sct-reference-Oracle-PostgreSQL-Universal.md#sct-reference-5339)   |  To correct this, update the original source code to make the specified object valid\.  | 
|  Universal action item  |   [Issue 5591: The %s synonym is system](sct-reference-Oracle-PostgreSQL-Universal.md#sct-reference-5591)   |  Perform a manual conversion\.  | 

## Unknown<a name="sct-reference-Oracle-PostgreSQL-unknown-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|   |   [Issue 5025: This syntactic element conversion is not supported yet](sct-reference-Oracle-PostgreSQL-Unknown.md#sct-reference-5025)   |  Perform a manual conversion\.  | 
|  Unknown object  |   [Issue 5351: Automatic conversion of %s object is not supported](sct-reference-Oracle-PostgreSQL-Unknown.md#sct-reference-5351)   |  Perform a manual conversion\.  | 
|  Unparsed SQL  |   [Issue 5576: Unparsed SQL](sct-reference-Oracle-PostgreSQL-Unknown.md#sct-reference-5576)   |  Perform a manual conversion\.  | 

## UPDATE<a name="sct-reference-Oracle-PostgreSQL-update-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  ERROR LOG  |   [Issue 5064: PostgreSQL doesn't support the UPDATE statement with the ERROR LOG option](sct-reference-Oracle-PostgreSQL-UPDATE.md#sct-reference-5064)   |  You can add error records by inserting them into the log in the exception block\. Iterate through the errors in the exception block, add them to the log, and use the EXIT command when finished\.  | 
|  PARTITION  |   [Issue 5558: PostgreSQL doesn't support the UPDATE statement for a PARTITION](sct-reference-Oracle-PostgreSQL-UPDATE.md#sct-reference-5558)   |  Either insert data into the overlying partition, or perform a manual transformation using the UPDATE statement\.  | 
|  QUERY  |   [Issue 5065: PostgreSQL doesn't support the UPDATE statement for a subquery](sct-reference-Oracle-PostgreSQL-UPDATE.md#sct-reference-5065)   |  Perform this operation on the underlying tables instead\.  | 

## VIEW<a name="sct-reference-Oracle-PostgreSQL-view-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  CAST \(MULTISET\(  |   [Issue 5245: PostgreSQL doesn't support views with nested table columns](sct-reference-Oracle-PostgreSQL-VIEW.md#sct-reference-5245)   |  Revise your code to replace nested table with another solution\.  | 
|  constraint  |   [Issue 5583: PostgreSQL doesn't support constraints for view](sct-reference-Oracle-PostgreSQL-VIEW.md#sct-reference-5583)   |  Perform a manual conversion\.  | 
|  OID\_TEXT IS NOT NULL  |   [Issue 5321: PostgreSQL doesn't support the object view](sct-reference-Oracle-PostgreSQL-VIEW.md#sct-reference-5321)   |  Perform a manual conversion\.  | 
|  PIVOT clause  |   [Issue 5077: PostgreSQL doesn't support the PIVOT clause for the SELECT statement](sct-reference-Oracle-PostgreSQL-VIEW.md#sct-reference-5077)   |  You can use a stored procedure to prepare data, and then return the data with a VIEW\.  | 
|  STATUS=INVALID  |   [Issue 5320: PostgreSQL doesn't support the view with invalid status](sct-reference-Oracle-PostgreSQL-VIEW.md#sct-reference-5320)   |  Perform a manual conversion\.  | 
|  VIEW\_TYPE\_OWNER IS NOT NULL  |   [Issue 5322: PostgreSQL doesn't support the typed view](sct-reference-Oracle-PostgreSQL-VIEW.md#sct-reference-5322)   |  Perform a manual conversion\.  | 
|  WITH READ ONLY  |   [Issue 5075: PostgreSQL doesn't support VIEW with the READ ONLY option](sct-reference-Oracle-PostgreSQL-VIEW.md#sct-reference-5075)   |  Use VIEW without this option instead\.  | 

## Related Topics<a name="sct-reference-Oracle-PostgreSQL-related"></a>

+  [AWS Schema Conversion Tool Reference](CHAP_SchemaConversionTool.Reference.md) 

+  [What Is the AWS Schema Conversion Tool?](Welcome.md) 