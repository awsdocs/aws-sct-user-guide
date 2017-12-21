# Microsoft SQL Server to PostgreSQL Conversion Issue Reference<a name="sct-reference-Microsoft-SQL-Server-PostgreSQL"></a>

Use the following sections to get information on the types of issues you might encounter during a Microsoft SQL Server to PostgreSQL conversion\. Choose the link in the **Issue** column to get more detailed resolution information about the issue if it is available\.

## Arithmetic Operators<a name="sct-reference-Microsoft-SQL-Server-PostgreSQL-arithmetic-operators-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  Arithmetic operators  |   [Issue 7775: Check the data type conversion for possible loss of accuracy](sct-reference-Microsoft-SQL-Server-PostgreSQL-Arithmeticoperators.md#sct-reference-7775)   |  Cast values as the intended type\.  | 
|  Arithmetic operators and date types  |   [Issue 7773: Unable to perform an automated migration of arithmetic operations with dates](sct-reference-Microsoft-SQL-Server-PostgreSQL-Arithmeticoperators.md#sct-reference-7773)   |  Cast values as the intended type\.  | 
|  Arithmetic operators and mixed types  |   [Issue 7774: Unable to perform an automated migration of the arithmetic operations with mixed types of operands](sct-reference-Microsoft-SQL-Server-PostgreSQL-Arithmeticoperators.md#sct-reference-7774)   |  Cast values as the intended type\.  | 

## Built\-In Services<a name="sct-reference-Microsoft-SQL-Server-PostgreSQL-built-in-services-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  Database Mail  |   [Issue 7900: PostgreSQL does not have functionality similar to SQL Server Database Mail](sct-reference-Microsoft-SQL-Server-PostgreSQL-BUILT-INSERVICES.md#sct-reference-7900)   |  Try using the Amazon Simple Notification Service \(Amazon SNS\)\.  | 
|  Service Broker  |   [Issue 7901: PostgreSQL does not have functionality similar to SQL Server Service Broker](sct-reference-Microsoft-SQL-Server-PostgreSQL-BUILT-INSERVICES.md#sct-reference-7901)   |  Try using the Amazon Simple Queue Service \(Amazon SQS\)\.  | 
|  SQL Server Agent  |   [Issue 7902: PostgreSQL does not have functionality similar to SQL Server Agent](sct-reference-Microsoft-SQL-Server-PostgreSQL-BUILT-INSERVICES.md#sct-reference-7902)   |  Try using the AWS Lambda service with Scheduled Events\.  | 
|  SQL Server Backup  |   [Issue 7903: PostgreSQL does not have functionality similar to SQL Server Backup](sct-reference-Microsoft-SQL-Server-PostgreSQL-BUILT-INSERVICES.md#sct-reference-7903)   |  Try using the Amazon Glacier storage service\.  | 

## Built\-In SQL Functions<a name="sct-reference-Microsoft-SQL-Server-PostgreSQL-built-in-sql-functions-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  SOUNDEX  |   [Issue 7811: PostgreSQL doesn't support the SOUNDEX function](sct-reference-Microsoft-SQL-Server-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-7811)   |  Create a user\-defined function\.  | 

## CONTROL FLOW<a name="sct-reference-Microsoft-SQL-Server-PostgreSQL-control-flow-overview-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
| Cursors |   [Issue 7801: The table can be locked open cursor](sct-reference-Microsoft-SQL-Server-PostgreSQL-CONTROLFLOW.md#sct-reference-7801)   |  Review your transformed code and modify it if necessary\.  | 
|  DECLARE / DEFAULT VALUE  |   [Issue 7826: Check the default value for a DateTime variable](sct-reference-Microsoft-SQL-Server-PostgreSQL-CONTROLFLOW.md#sct-reference-7826)   |  Check the default value for a DateTime variable\.  | 
|  GOTO  |   [Issue 7628: PostgreSQL doesn't support the GOTO option\. Automatic conversion can't be performed\.](sct-reference-Microsoft-SQL-Server-PostgreSQL-CONTROLFLOW.md#sct-reference-7628)   |  Revise your code to eliminate GOTO operators, using BEGIN\.\.\.END blocks in combination with EXIT, REPEAT, UNTIL, and WHILE operators\.  | 
| Procedures |   [Issue 7802: A table that is created within the procedure, must be deleted before the end of the procedure](sct-reference-Microsoft-SQL-Server-PostgreSQL-CONTROLFLOW.md#sct-reference-7802)   |  Review your transformed code and modify it if necessary\.  | 
| Result sets |   [Issue 7800: PostgreSQL doesn't support result sets in the style of MSSQL](sct-reference-Microsoft-SQL-Server-PostgreSQL-CONTROLFLOW.md#sct-reference-7800)   |  Review your transformed code and modify it if necessary\.  | 
|  WAITFOR DELAY  |   [Issue 7821: Automatic conversion operator WAITFOR with a variable is not supported](sct-reference-Microsoft-SQL-Server-PostgreSQL-CONTROLFLOW.md#sct-reference-7821)   |  Perform a manual conversion\.  | 
|  WAITFOR TIME  |   [Issue 7691: PostgreSQL doesn't support WAITFOR TIME feature](sct-reference-Microsoft-SQL-Server-PostgreSQL-CONTROLFLOW.md#sct-reference-7691)   |  Perform a manual conversion\.  | 

## CREATE<a name="sct-reference-Microsoft-SQL-Server-PostgreSQL-create-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|   |   [Issue 7696: Unable convert object due to %s not created](sct-reference-Microsoft-SQL-Server-PostgreSQL-CREATE.md#sct-reference-7696)   |  Review the %s object\.  | 
|  Encrypted objects  |   [Issue 7813: Encrypted objects](sct-reference-Microsoft-SQL-Server-PostgreSQL-CREATE.md#sct-reference-7813)   |  Decrypt the object before conversion\.  | 

## CURSORS<a name="sct-reference-Microsoft-SQL-Server-PostgreSQL-cursors-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  CURSOR with option GLOBAL  |   [Issue 7637: PostgreSQL doesn't support GLOBAL CURSORS\. Requires manual conversion\.](sct-reference-Microsoft-SQL-Server-PostgreSQL-CURSORS.md#sct-reference-7637)   |  Change the global cursor to a local cursor, or revise your code so it doesn't require global cursors\.  | 
|  CURSOR with options STATIC or KEYSET or DYNAMIC or FAST\_FORWARD  |   [Issue 7639: PostgreSQL doesn't support DYNAMIC cursors](sct-reference-Microsoft-SQL-Server-PostgreSQL-CURSORS.md#sct-reference-7639)   |  Revise your code to eliminate dynamic cursors\.  | 
|  FAST\_FORWARD option  |   [Issue 7701: Setting this option corresponds to the typical behavior of cursors in PostgreSQL, so this option is skipped](sct-reference-Microsoft-SQL-Server-PostgreSQL-CURSORS.md#sct-reference-7701)   |  Use cursors without this option\.  | 
|  FOR UPDATE  |   [Issue 7803: PostgreSQL doesn't support the option FOR UPDATE, so this option is skipped](sct-reference-Microsoft-SQL-Server-PostgreSQL-CURSORS.md#sct-reference-7803)   |  Review your transformed code and modify it if necessary\.  | 
|  KEYSET option  |   [Issue 7700: The membership and order of rows never changes for cursors in PostgreSQL, so this option is skipped](sct-reference-Microsoft-SQL-Server-PostgreSQL-CURSORS.md#sct-reference-7700)   |  Use cursors without this option\.  | 
|  OPTIMISTIC option  |   [Issue 7704: PostgreSQL doesn't support the option OPTIMISTIC, so this option is skipped](sct-reference-Microsoft-SQL-Server-PostgreSQL-CURSORS.md#sct-reference-7704)   |  Use cursors without this option\.  | 
|  READ\_ONLY option  |   [Issue 7702: All PostgreSQL cursors are read\-only, so this option is skipped](sct-reference-Microsoft-SQL-Server-PostgreSQL-CURSORS.md#sct-reference-7702)   |  Use cursors without this option\.  | 
|  TYPE\_WARNING option  |   [Issue 7705: PostgreSQL doesn't support the option TYPE\_WARNING, so this option is skipped](sct-reference-Microsoft-SQL-Server-PostgreSQL-CURSORS.md#sct-reference-7705)   |  Use cursors without this option\.  | 

## DATA TYPES<a name="sct-reference-Microsoft-SQL-Server-PostgreSQL-datatypes-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  BYTEA  |   [Issue 7818: PostgreSQL doesn't support arithmetic operations with binary data types](sct-reference-Microsoft-SQL-Server-PostgreSQL-DATATYPES.md#sct-reference-7818)   |  Perform a manual conversion\.  | 
|  geography  |   [Issue 7662: PostgreSQL doesn't support this type\. A manual conversion is required\.](sct-reference-Microsoft-SQL-Server-PostgreSQL-DATATYPES.md#sct-reference-7662)   |  To store data of this type in PostgreSQL, use a PostgreSQL\-compatible type or use a composite type\.  | 
|  geometry  |   [Issue 7664: PostgreSQL doesn't support this type\. A manual conversion is required\.](sct-reference-Microsoft-SQL-Server-PostgreSQL-DATATYPES.md#sct-reference-7664)   |  To store data of this type in PostgreSQL, use a PostgreSQL\-compatible type or use a composite type\.  | 
|  hierarchyid  |   [Issue 7657: PostgreSQL doesn't support this type\. A manual conversion is required\.](sct-reference-Microsoft-SQL-Server-PostgreSQL-DATATYPES.md#sct-reference-7657)   |  To store data of this type in PostgreSQL, use a PostgreSQL\-compatible type or use a composite type\.  | 
|  rowversion  |   [Issue 7706: PostgreSQL doesn't support this type](sct-reference-Microsoft-SQL-Server-PostgreSQL-DATATYPES.md#sct-reference-7706)   |  Perform a manual conversion\.  | 
|  sql\_variant  |   [Issue 7658: PostgreSQL doesn't support this type\. A manual conversion is required\.](sct-reference-Microsoft-SQL-Server-PostgreSQL-DATATYPES.md#sct-reference-7658)   |  To store data of this type in PostgreSQL, use a PostgreSQL\-compatible type or use a composite type\.  | 
|  table  |   [Issue 7659: The scope table\-variables and temporary tables is different\. You must apply manual conversion, if you are using recursion\.](sct-reference-Microsoft-SQL-Server-PostgreSQL-DATATYPES.md#sct-reference-7659)   |  Perform a manual conversion\.  | 
|  UDT  |   [Issue 7690: PostgreSQL doesn't support table types](sct-reference-Microsoft-SQL-Server-PostgreSQL-DATATYPES.md#sct-reference-7690)   |  Perform a manual conversion\.  | 
|  XML  |   [Issue 7816: PostgreSQL doesn't support any methods for data type XML](sct-reference-Microsoft-SQL-Server-PostgreSQL-DATATYPES.md#sct-reference-7816)   |  Perform a manual conversion\.  | 
|  XML  |   [Issue 7817: PostgreSQL doesn't support option \[for xml path\] in the SQL queries](sct-reference-Microsoft-SQL-Server-PostgreSQL-DATATYPES.md#sct-reference-7817)   |  Perform a manual conversion\.  | 

## DDL<a name="sct-reference-Microsoft-SQL-Server-PostgreSQL-ddl-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  CREATE INDEX  |   [Issue 7675: PostgreSQL doesn't support sorting options \(ASC | DESC\) for constraints](sct-reference-Microsoft-SQL-Server-PostgreSQL-DDL.md#sct-reference-7675)   |  Use indexes without this option\.  | 
|  CREATE INDEX  |   [Issue 7681: PostgreSQL doesn't support clustered indexes](sct-reference-Microsoft-SQL-Server-PostgreSQL-DDL.md#sct-reference-7681)   |  Use nonclustered indexes\.  | 
|  CREATE INDEX  |   [Issue 7682: PostgreSQL doesn't support the INCLUDE option in indexes](sct-reference-Microsoft-SQL-Server-PostgreSQL-DDL.md#sct-reference-7682)   |  Use index without this option\.  | 
|  CREATE INDEX  |   [Issue 7781: PostgreSQL doesn't support the PAD\_INDEX option in indexes](sct-reference-Microsoft-SQL-Server-PostgreSQL-DDL.md#sct-reference-7781)   |  Use index without this option\.  | 
|  CREATE INDEX  |   [Issue 7782: PostgreSQL doesn't support the SORT\_IN\_TEMPDB option in indexes](sct-reference-Microsoft-SQL-Server-PostgreSQL-DDL.md#sct-reference-7782)   |  Use index without this option\.  | 
|  CREATE INDEX  |   [Issue 7783: PostgreSQL doesn't support the IGNORE\_DUP\_KEY option in indexes](sct-reference-Microsoft-SQL-Server-PostgreSQL-DDL.md#sct-reference-7783)   |  Use index without this option\.  | 
|  CREATE INDEX  |   [Issue 7784: PostgreSQL doesn't support the STATISTICS\_NORECOMPUTE option in indexes](sct-reference-Microsoft-SQL-Server-PostgreSQL-DDL.md#sct-reference-7784)   |  Use index without this option\.  | 
|  CREATE INDEX  |   [Issue 7785: PostgreSQL doesn't support the STATISTICS\_INCREMENTAL option in indexes](sct-reference-Microsoft-SQL-Server-PostgreSQL-DDL.md#sct-reference-7785)   |  Use index without this option\.  | 
|  CREATE INDEX  |   [Issue 7786: PostgreSQL doesn't support the DROP\_EXISTING option in indexes](sct-reference-Microsoft-SQL-Server-PostgreSQL-DDL.md#sct-reference-7786)   |  Use index without this option\.  | 
|  CREATE INDEX  |   [Issue 7787: PostgreSQL doesn't support the ONLINE option in indexes](sct-reference-Microsoft-SQL-Server-PostgreSQL-DDL.md#sct-reference-7787)   |  Use index without this option\.  | 
|  CREATE INDEX  |   [Issue 7788: PostgreSQL doesn't support the ALLOW\_ROW\_LOCKS option in indexes](sct-reference-Microsoft-SQL-Server-PostgreSQL-DDL.md#sct-reference-7788)   |  Use index without this option\.  | 
|  CREATE INDEX  |   [Issue 7789: PostgreSQL doesn't support the ALLOW\_PAGE\_LOCKS option in indexes](sct-reference-Microsoft-SQL-Server-PostgreSQL-DDL.md#sct-reference-7789)   |  Use index without this option\.  | 
|  CREATE INDEX  |   [Issue 7790: PostgreSQL doesn't support the MAXDOP option in indexes](sct-reference-Microsoft-SQL-Server-PostgreSQL-DDL.md#sct-reference-7790)   |  Use index without this option\.  | 
|  CREATE INDEX  |   [Issue 7791: PostgreSQL doesn't support the DATA\_COMPRESSION option in indexes](sct-reference-Microsoft-SQL-Server-PostgreSQL-DDL.md#sct-reference-7791)   |  Use index without this option\.  | 
|  CREATE TABLE  |   [Issue 7679: PostgreSQL doesn't support computed columns](sct-reference-Microsoft-SQL-Server-PostgreSQL-DDL.md#sct-reference-7679)   |  Try using a trigger\.  | 
|  CREATE TABLE  |   [Issue 7680: PostgreSQL doesn't support global temporary tables](sct-reference-Microsoft-SQL-Server-PostgreSQL-DDL.md#sct-reference-7680)   |  Use local temporary or regular tables\.  | 
|  CREATE TABLE  |   [Issue 7812: Temporary table must be removed before the end of the function](sct-reference-Microsoft-SQL-Server-PostgreSQL-DDL.md#sct-reference-7812)   |  Review your transformed code and modify it if necessary\.  | 
|  CREATE TABLE  |   [Issue 7825: The default value for a DateTime column removed](sct-reference-Microsoft-SQL-Server-PostgreSQL-DDL.md#sct-reference-7825)   |  Review generated code and modify it if necessary\.  | 
|  Inline Function  |   [Issue 7776: Automatic migration of inline functions not supported](sct-reference-Microsoft-SQL-Server-PostgreSQL-DDL.md#sct-reference-7776)   |  Perform a manual conversion\.  | 

## DELETE<a name="sct-reference-Microsoft-SQL-Server-PostgreSQL-delete-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  DELETE with Table Hint Limited  |   [Issue 7623: PostgreSQL doesn't support hints in DELETE statements\. The conversion skips options in the format WITH\(Table\_Hint\_Limited\)\.](sct-reference-Microsoft-SQL-Server-PostgreSQL-DELETE.md#sct-reference-7623)   |  Use PostgreSQL methods for performance tuning\.  | 
|  TOP  |   [Issue 7798: PostgreSQL doesn't support TOP option in the operator DELETE](sct-reference-Microsoft-SQL-Server-PostgreSQL-DELETE.md#sct-reference-7798)   |  Perform a manual conversion\.  | 

## DML, FROM<a name="sct-reference-Microsoft-SQL-Server-PostgreSQL-dml-from-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  Table Hints  |   [Issue 7823: PostgreSQL doesn't support table hints in DML statements](sct-reference-Microsoft-SQL-Server-PostgreSQL-DML-FROM.md#sct-reference-7823)   |  Use PostgreSQL methods of performance tuning\.  | 

## EXECUTE<a name="sct-reference-Microsoft-SQL-Server-PostgreSQL-execute-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|   |   [Issue 7695: PostgreSQL doesn't support the execution of a procedure as a variable](sct-reference-Microsoft-SQL-Server-PostgreSQL-EXECUTE.md#sct-reference-7695)   |  Perform a manual conversion using dynamic SQL\.  | 
|  EXECUTE a character string  |   [Issue 7672: Automatic conversion of this command is not supported](sct-reference-Microsoft-SQL-Server-PostgreSQL-EXECUTE.md#sct-reference-7672)   |  Perform a manual conversion\.  | 
|  Execute a pass\-through command against a linked server  |   [Issue 7645: PostgreSQL doesn't support executing a pass\-through command on a linked server](sct-reference-Microsoft-SQL-Server-PostgreSQL-EXECUTE.md#sct-reference-7645)   |  Use other methods to execute statements on a remote server\.  | 
|  EXECUTE with execute options \[RECOMPILE\]  |   [Issue 7640: The EXECUTE with RECOMPILE option is ignored](sct-reference-Microsoft-SQL-Server-PostgreSQL-EXECUTE.md#sct-reference-7640)   |  Use EXECUTE command without this option\.  | 
|  EXECUTE with execute options \[RESULT SETS \(<result\_sets\_definition>\)\]  |   [Issue 7643: The EXECUTE with RESULT SETS <result set definition> option is ignored](sct-reference-Microsoft-SQL-Server-PostgreSQL-EXECUTE.md#sct-reference-7643)   |  Use EXECUTE command without this option\.  | 
|  EXECUTE with execute options \[RESULT SETS NONE\]  |   [Issue 7642: The EXECUTE with RESULT SETS NONE option is ignored](sct-reference-Microsoft-SQL-Server-PostgreSQL-EXECUTE.md#sct-reference-7642)   |  Use EXECUTE command without this option\.  | 
|  EXECUTE with execute options \[RESULT SETS UNDEFINED\]  |   [Issue 7641: The EXECUTE with RESULT SETS UNDEFINED option is ignored](sct-reference-Microsoft-SQL-Server-PostgreSQL-EXECUTE.md#sct-reference-7641)   |  Use EXECUTE command without this option\.  | 

## INSERT<a name="sct-reference-Microsoft-SQL-Server-PostgreSQL-insert-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  EXECUTE  |   [Issue 7819: PostgreSQL doesn't support INSERT\.\.\.EXECUTE statements](sct-reference-Microsoft-SQL-Server-PostgreSQL-INSERT.md#sct-reference-7819)   |  Perform a manual conversion\.  | 
|  TOP  |   [Issue 7799: PostgreSQL doesn't support TOP option in the operator INSERT](sct-reference-Microsoft-SQL-Server-PostgreSQL-INSERT.md#sct-reference-7799)   |  Perform a manual conversion\.  | 

## Operators<a name="sct-reference-Microsoft-SQL-Server-PostgreSQL-operators-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  Bitwise Operators  |   [Issue 7804: PostgreSQL doesn't support operator \[Bitwise exclusive OR\]](sct-reference-Microsoft-SQL-Server-PostgreSQL-Operators.md#sct-reference-7804)   |  Perform a manual conversion\.  | 
|  Comparison Operators  |   [Issue 7805: PostgreSQL doesn't support operator \[Not less than\]](sct-reference-Microsoft-SQL-Server-PostgreSQL-Operators.md#sct-reference-7805)   |  Perform a manual conversion\.  | 
|  Comparison Operators  |   [Issue 7806: PostgreSQL doesn't support operator \[Not greater than\]](sct-reference-Microsoft-SQL-Server-PostgreSQL-Operators.md#sct-reference-7806)   |  Perform a manual conversion\.  | 

## Parser Error<a name="sct-reference-Microsoft-SQL-Server-PostgreSQL-parser-error-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  Parser Error  |   [Issue 7663: Unable to resolve the object](sct-reference-Microsoft-SQL-Server-PostgreSQL-ParserError.md#sct-reference-7663)   |  Verify if object <object name> is present in the database\. If it isn't, check the object name or add the object\. If the object is present, transform the code manually\.  | 

## SELECT<a name="sct-reference-Microsoft-SQL-Server-PostgreSQL-select-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  GROUP BY CUBE  |   [Issue 7653: PostgreSQL doesn't support the option GROUP BY ROLLUP\. Automatic conversion can't be performed\.](sct-reference-Microsoft-SQL-Server-PostgreSQL-SELECT.md#sct-reference-7653)   |  Try creating a stored procedure to replace the query\.  | 
|  GROUP BY CUBE  |   [Issue 7654: PostgreSQL doesn't support the option GROUP BY CUBE\. Automatic conversion can't be performed\.](sct-reference-Microsoft-SQL-Server-PostgreSQL-SELECT.md#sct-reference-7654)   |  Try creating a stored procedure to replace the query\.  | 
|  Group By Grouping Sets  |   [Issue 7655: PostgreSQL doesn't support the option GROUP BY GROUPING SETS\. Automatic conversion can't be performed\.](sct-reference-Microsoft-SQL-Server-PostgreSQL-SELECT.md#sct-reference-7655)   |  Try creating a stored procedure to replace the query\.  | 
|  ORDER BY Specifying a collation  |   [Issue 7646: PostgreSQL doesn't support the COLLATE option in the ORDER BY clause\. Automatic conversion can't be performed\.](sct-reference-Microsoft-SQL-Server-PostgreSQL-SELECT.md#sct-reference-7646)   |  You must use the COLLATION settings that were assigned when the database was created\.  | 
|  search condition  |   [Issue 7687: PostgreSQL doesn't support the CONTAINS predicate](sct-reference-Microsoft-SQL-Server-PostgreSQL-SELECT.md#sct-reference-7687)   |  Perform a manual conversion\.  | 
|  search condition  |   [Issue 7688: PostgreSQL doesn't support the FREETEXT predicate](sct-reference-Microsoft-SQL-Server-PostgreSQL-SELECT.md#sct-reference-7688)   |  Perform a manual conversion\.  | 
|  search condition  |   [Issue 7795: PostgreSQL is case sensitive\. Check the string comparison\.](sct-reference-Microsoft-SQL-Server-PostgreSQL-SELECT.md#sct-reference-7795)   |  Check the string comparison\.  | 
|  TOP WITH TIES  |   [Issue 7605: PostgreSQL doesn't support the WITH TIES option](sct-reference-Microsoft-SQL-Server-PostgreSQL-SELECT.md#sct-reference-7605)   |  Perform a manual conversion\.  | 

## SEQUENCE<a name="sct-reference-Microsoft-SQL-Server-PostgreSQL-sequence-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  Specific data type  |   [Issue 7793: PostgreSQL doesn't support changing data type in sequences](sct-reference-Microsoft-SQL-Server-PostgreSQL-SEQUENCE.md#sct-reference-7793)   |  Review your transformed code and modify it if necessary\.  | 

## SYNONYMS<a name="sct-reference-Microsoft-SQL-Server-PostgreSQL-synonyms-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  CREATE  |   [Issue 7792: PostgreSQL doesn't support synonyms](sct-reference-Microsoft-SQL-Server-PostgreSQL-SYNONYMS.md#sct-reference-7792)   |  Replace a synonym with original database object\. If original object is table or view you can try to create a view in one database that relies on a table or view in another database\.  | 

## SYS objects<a name="sct-reference-Microsoft-SQL-Server-PostgreSQL-sys-objects-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  SYS objects  |   [Issue 7904: Unable to convert system object <object name>](sct-reference-Microsoft-SQL-Server-PostgreSQL-SYSobjects.md#sct-reference-7904)   |  Perform a manual conversion\.  | 

## TRANSACTION<a name="sct-reference-Microsoft-SQL-Server-PostgreSQL-transaction-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  Transaction  |   [Issue 7807: Transactions in functions PostgreSQL doesn't support](sct-reference-Microsoft-SQL-Server-PostgreSQL-TRANSACTION.md#sct-reference-7807)   |  Perform a manual conversion\.  | 

## TRIGGERS<a name="sct-reference-Microsoft-SQL-Server-PostgreSQL-triggers-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  Triggers  |   [Issue 7809: In PostgreSQL there are no analogues of the tables 'inserted' and 'deleted'](sct-reference-Microsoft-SQL-Server-PostgreSQL-TRIGGERS.md#sct-reference-7809)   |  Perform a manual conversion\.  | 

## Unknown<a name="sct-reference-Microsoft-SQL-Server-PostgreSQL-unknown-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|   |   [Issue 7627: This syntactic element conversion is not supported yet](sct-reference-Microsoft-SQL-Server-PostgreSQL-Unknown.md#sct-reference-7627)   |  Perform a manual conversion\.  | 
|  Unknown Clause  |   [Issue 7674: Automatic conversion of <clause name> clause of <statement name> statement is not supported](sct-reference-Microsoft-SQL-Server-PostgreSQL-Unknown.md#sct-reference-7674)   |  Perform a manual conversion\.  | 
|  Unparsed SQL  |   [Issue 7808: Unparsed SQL](sct-reference-Microsoft-SQL-Server-PostgreSQL-Unknown.md#sct-reference-7808)   |  Perform a manual conversion\.  | 

## UPDATE<a name="sct-reference-Microsoft-SQL-Server-PostgreSQL-update-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  TOP  |   [Issue 7796: PostgreSQL doesn't support TOP option in the operator UPDATE](sct-reference-Microsoft-SQL-Server-PostgreSQL-UPDATE.md#sct-reference-7796)   |  Perform a manual conversion\.  | 
|  UPDATE  |   [Issue 7797: PostgreSQL doesn't have analog for option "OUTPUT" with using the implicit table "deleted" in the operator for UPDATE](sct-reference-Microsoft-SQL-Server-PostgreSQL-UPDATE.md#sct-reference-7797)   |  This case requires manual conversion\.  | 
|  Variable assignment  |   [Issue 7829: Unable to convert variable assignment by UPDATE statement](sct-reference-Microsoft-SQL-Server-PostgreSQL-UPDATE.md#sct-reference-7829)   |  Perform a manual conversion\.  | 

## User Types<a name="sct-reference-Microsoft-SQL-Server-PostgreSQL-user-types-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  User\-Defined Data Types  |   [Issue 7794: PostgreSQL doesn't support user\-defined data types](sct-reference-Microsoft-SQL-Server-PostgreSQL-Usertypes.md#sct-reference-7794)   |  Perform a manual conversion\.  | 

## Related Topics<a name="sct-reference-Microsoft-SQL-Server-PostgreSQL-related"></a>

+  [AWS Schema Conversion Tool Reference](CHAP_SchemaConversionTool.Reference.md) 

+  [What Is the AWS Schema Conversion Tool?](Welcome.md) 