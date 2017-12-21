# MySQL to PostgreSQL Conversion Reference<a name="sct-reference-MySQL-PostgreSQL"></a>

## BUILT\-IN SQL FUNCTIONS<a name="sct-reference-MySQL-PostgreSQL-built-in-sql-functions-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  Function  |   [Issue 8811: PostgreSQL doesn't support the %s function](sct-reference-MySQL-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-8811)   |  Create a user\-defined function\.  | 
|  Function  |   [Issue 8849: PostgreSQL doesn't support the %s function with parameter values %s](sct-reference-MySQL-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-8849)   |  Create a user\-defined function\.  | 
|  Function  |   [Issue 8850: Some parameter values for the function %s aren't supported](sct-reference-MySQL-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-8850)   |  You need to check the result of the conversion  | 
|  Function  |   [Issue 8851: PostgreSQL doesn't support using aggregate functions in the SELECT list without a GROUP BY clause](sct-reference-MySQL-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-8851)   |  Perform a manual conversion\.  | 
|  Function  |   [Issue 8854: PostgreSQL doesn't support the %s function with parameters](sct-reference-MySQL-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-8854)   |  Perform a manual conversion\.  | 

## CONTROL FLOW<a name="sct-reference-MySQL-PostgreSQL-control-flow-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  CURSORS  |   [Issue 8845: Rows count functionality is not supported behind the "open cursor" statement](sct-reference-MySQL-PostgreSQL-CONTROLFLOW.md#sct-reference-8845)   |  Perform a manual conversion\.  | 
|  DECLARE / DEFAULT VALUE  |   [Issue 8826: Check the default value for a Date or DateTime variable](sct-reference-MySQL-PostgreSQL-CONTROLFLOW.md#sct-reference-8826)   |  Review generated code and modify it if necessary\.  | 
|  DECLARE / DEFAULT VALUE  |   [Issue 8828: User\-defined variables are not supported in PostgreSQL](sct-reference-MySQL-PostgreSQL-CONTROLFLOW.md#sct-reference-8828)   |  Perform a manual conversion\.  | 
|  error handling  |   [Issue 8844: Error codes are not the same](sct-reference-MySQL-PostgreSQL-CONTROLFLOW.md#sct-reference-8844)   |  You need to check the result of the conversion  | 
|  error handling  |   [Issue 8846: PostgreSQL doesn't support the statement option %s](sct-reference-MySQL-PostgreSQL-CONTROLFLOW.md#sct-reference-8846)   |  Perform a manual conversion\.  | 
|  error handling  |   [Issue 8847: PostgreSQL isn't able to return to a call point after error handling](sct-reference-MySQL-PostgreSQL-CONTROLFLOW.md#sct-reference-8847)   |  Perform a manual conversion\.  | 
|  LABEL  |   [Issue 8827: Statement Label Syntax for BEGIN\.\.\.END blocks is not supported in PostgreSQL](sct-reference-MySQL-PostgreSQL-CONTROLFLOW.md#sct-reference-8827)   |  Perform a manual conversion\.  | 
|  PROCESS\_LIST  |   [Issue 8856: The information of the server processes is different on different servers](sct-reference-MySQL-PostgreSQL-CONTROLFLOW.md#sct-reference-8856)   |  Check your conversion result\.  | 
|  REPLICATION  |   [Issue 8857: Automatic conversion for replication commands is not supported](sct-reference-MySQL-PostgreSQL-CONTROLFLOW.md#sct-reference-8857)   |  Perform a manual conversion\.  | 
|  SLEEP  |   [Issue 8853: Perform a manual conversion if using SLEEP\(\) with other expressions](sct-reference-MySQL-PostgreSQL-CONTROLFLOW.md#sct-reference-8853)   |  Perform a manual conversion\.  | 

## CREATE<a name="sct-reference-MySQL-PostgreSQL-create-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|   |   [Issue 8654: Unable to convert object due to %s not created](sct-reference-MySQL-PostgreSQL-CREATE.md#sct-reference-8654)   |  Review the %s object\.  | 

## DATATYPES<a name="sct-reference-MySQL-PostgreSQL-datatypes-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  BOOLEAN  |   [Issue 8848: In MySQL the BOOLEAN type is a synonym for TINYINT](sct-reference-MySQL-PostgreSQL-DATATYPES.md#sct-reference-8848)   |  Check it when you insert data from a BOOLEAN variables into the database\.  | 
|  DATATYPES  |   [Issue 8706: PostgreSQL doesn't support %s type](sct-reference-MySQL-PostgreSQL-DATATYPES.md#sct-reference-8706)   |  To store data of this type in PostgreSQL, use a PostgreSQL\-compatible type or use a composite type\.  | 

## DDL<a name="sct-reference-MySQL-PostgreSQL-ddl-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  CREATE TABLE  |   [Issue 8825: Check the default value for a Date or DateTime column](sct-reference-MySQL-PostgreSQL-DDL.md#sct-reference-8825)   |  Review generated code and modify it if necessary\.  | 
|  DROP TABLE  |   [Issue 8801: The table can be locked open cursor](sct-reference-MySQL-PostgreSQL-DDL.md#sct-reference-8801)   |  Review your transformed code and modify it if necessary\.  | 

## DML<a name="sct-reference-MySQL-PostgreSQL-dml-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  DML  |   [Issue 8829: PostgreSQL doesn't have an analog of clause ON DUPLICATE KEY UPDATE](sct-reference-MySQL-PostgreSQL-DML.md#sct-reference-8829)   |  Perform a manual conversion\.  | 
|  DML  |   [Issue 8830: PostgreSQL doesn't have an option similar to LOW\_PRIORITY for DML statements](sct-reference-MySQL-PostgreSQL-DML.md#sct-reference-8830)   |  Use DML statement without this option\.  | 
|  DML  |   [Issue 8831: PostgreSQL doesn't have an option similar to IGNORE for DML statements](sct-reference-MySQL-PostgreSQL-DML.md#sct-reference-8831)   |  Use DML statement without this option\.  | 
|  DML  |   [Issue 8832: PostgreSQL doesn't have an option similar to QUICK for DML statements](sct-reference-MySQL-PostgreSQL-DML.md#sct-reference-8832)   |  Use DML statement without this option\.  | 
|  DML  |   [Issue 8833: PostgreSQL can't make updates to several tables at the same time](sct-reference-MySQL-PostgreSQL-DML.md#sct-reference-8833)   |  Perform a manual conversion\.  | 
|  DML  |   [Issue 8834: PostgreSQL can't delete from several tables at the same time](sct-reference-MySQL-PostgreSQL-DML.md#sct-reference-8834)   |  Perform a manual conversion\.  | 
|  SELECT  |   [Issue 8835: PostgreSQL doesn't have an option similar to DELAYED for DML statements](sct-reference-MySQL-PostgreSQL-DML.md#sct-reference-8835)   |  Use DML statement without this option\.  | 
|  SELECT  |   [Issue 8836: PostgreSQL doesn't have an option similar to %s for DML statements](sct-reference-MySQL-PostgreSQL-DML.md#sct-reference-8836)   |  Use DML statement without this option\.  | 
|  SELECT  |   [Issue 8837: PostgreSQL doesn't support clause STRAIGHT\_JOIN](sct-reference-MySQL-PostgreSQL-DML.md#sct-reference-8837)   |  Use DML statement without this option  | 
|  SELECT  |   [Issue 8838: PostgreSQL doesn't support clause SQL\_SMALL\_RESULT](sct-reference-MySQL-PostgreSQL-DML.md#sct-reference-8838)   |  Use DML statement without this option  | 
|  SELECT  |   [Issue 8839: PostgreSQL doesn't support clause SQL\_BIG\_RESULT](sct-reference-MySQL-PostgreSQL-DML.md#sct-reference-8839)   |  Use DML statement without this option  | 
|  SELECT  |   [Issue 8840: PostgreSQL doesn't support clause SQL\_BUFFER\_RESULT](sct-reference-MySQL-PostgreSQL-DML.md#sct-reference-8840)   |  Use DML statement without this option  | 
|  SELECT  |   [Issue 8841: PostgreSQL doesn't support clause SQL\_CACHE](sct-reference-MySQL-PostgreSQL-DML.md#sct-reference-8841)   |  Use DML statement without this option  | 
|  SELECT  |   [Issue 8842: PostgreSQL doesn't support clause SQL\_NO\_CACHE](sct-reference-MySQL-PostgreSQL-DML.md#sct-reference-8842)   |  Use DML statement without this option  | 
|  SELECT  |   [Issue 8843: PostgreSQL doesn't support clause SQL\_CALC\_FOUND\_ROWS](sct-reference-MySQL-PostgreSQL-DML.md#sct-reference-8843)   |  Use DML statement without this option  | 
|  WHERE  |   [Issue 8795: PostgreSQL is case sensitive\. Check the string comparison\.](sct-reference-MySQL-PostgreSQL-DML.md#sct-reference-8795)   |  Check the string comparison\.  | 

## EVENTS<a name="sct-reference-MySQL-PostgreSQL-events-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  EVENTS  |   [Issue 8855: Automatic conversion of EVENT syntax is not supported](sct-reference-MySQL-PostgreSQL-EVENTS.md#sct-reference-8855)   |  Perform a manual conversion\.  | 

## EXECUTE<a name="sct-reference-MySQL-PostgreSQL-execute-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  EXECUTE a character string  |   [Issue 8672: Automatic conversion of this command is not supported](sct-reference-MySQL-PostgreSQL-EXECUTE.md#sct-reference-8672)   |  Perform a manual conversion\.  | 

## Operators<a name="sct-reference-MySQL-PostgreSQL-operators-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  Arithmetic operators  |   [Issue 8773: The tool can not currently perform automated migration of arithmetic operations with dates](sct-reference-MySQL-PostgreSQL-Operators.md#sct-reference-8773)   |  Perform a manual conversion\.  | 
|  Arithmetic operators  |   [Issue 8774: The tool can not currently perform automated migration of arithmetic operations with mixed types of operands](sct-reference-MySQL-PostgreSQL-Operators.md#sct-reference-8774)   |  Perform a manual conversion\.  | 

## Parser Error<a name="sct-reference-MySQL-PostgreSQL-parser-error-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  Parser Error  |   [Issue 8663: Unable to resolve the object](sct-reference-MySQL-PostgreSQL-ParserError.md#sct-reference-8663)   |  Verify if object %s is present in the database\. If it isn't, check the object name or add the object\. If the object is present, transform the code manually\.  | 

## SELECT<a name="sct-reference-MySQL-PostgreSQL-select-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  GROUP BY  |   [Issue 8653: PostgreSQL doesn't support the option GROUP BY ROLLUP](sct-reference-MySQL-PostgreSQL-SELECT.md#sct-reference-8653)   |  Perform a manual conversion\.  | 

## TRANSACTION<a name="sct-reference-MySQL-PostgreSQL-transaction-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  TRANSACTION  |   [Issue 8807: PostgreSQL doesn't support transactions in functions](sct-reference-MySQL-PostgreSQL-TRANSACTION.md#sct-reference-8807)   |  Perform a manual conversion\.  | 

## Unknown<a name="sct-reference-MySQL-PostgreSQL-unknown-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|   |   [Issue 8655: This syntactic element conversion is not supported yet](sct-reference-MySQL-PostgreSQL-Unknown.md#sct-reference-8655)   |  Perform a manual conversion\.  | 
|  Unknown Clause  |   [Issue 8674: Automatic conversion of %s clause of %s statement is not supported](sct-reference-MySQL-PostgreSQL-Unknown.md#sct-reference-8674)   |  Perform a manual conversion\.  | 

## VIEW<a name="sct-reference-MySQL-PostgreSQL-view-overview"></a>


| Item | Issue | Resolution | 
| --- | --- | --- | 
|  CREATE VIEV  |   [Issue 8824: ALGORITHM option is not supported](sct-reference-MySQL-PostgreSQL-VIEW.md#sct-reference-8824)   |  Perform a manual conversion\.  | 

## Related Topics<a name="sct-reference-MySQL-PostgreSQL-related"></a>

+  [AWS Schema Conversion Tool Reference](CHAP_SchemaConversionTool.Reference.md) 

+  [What Is the AWS Schema Conversion Tool?](Welcome.md) 