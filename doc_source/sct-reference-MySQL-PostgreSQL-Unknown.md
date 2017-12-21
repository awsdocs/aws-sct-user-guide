# Conversion Issues with Unknown<a name="sct-reference-MySQL-PostgreSQL-Unknown"></a>

## Issue 8655: This syntactic element conversion is not supported yet<a name="sct-reference-8655"></a>

Perform a manual conversion\.

## Issue 8674: Automatic conversion of %s clause of %s statement is not supported<a name="sct-reference-8674"></a>

This error is typically raised by code that sets transaction options or replication\-related variables that aren't supported in PostgreSQL\. Such code must be manually converted\. Statements that raise this error include the following:

+ SET TRANSACTION ISOLATION LEVEL SERIALIZABLE;

+ SET TRANSACTION READ ONLY;

+ SET SESSION TRANSACTION READ WRITE;

+ SET SESSION TRANSACTION ISOLATION LEVEL REPEATABLE READ;

+ SET TRANSACTION ISOLATION LEVEL READ COMMITTED;

+ SET TRANSACTION ISOLATION LEVEL READ UNCOMMITTED;

+ SET GLOBAL TRANSACTION READ WRITE;

+ SET GLOBAL tx\_isolation=<isolation\_level>;

+ SET SQL\_LOG\_BIN=<value>;

+ SET GLOBAL sql\_slave\_skip\_counter=<value>;

## Related Topics<a name="sct-reference-MySQL-PostgreSQL-Unknown-related"></a>

+  [MySQL to PostgreSQL Conversion Reference](sct-reference-MySQL-PostgreSQL.md) 

+  [AWS Schema Conversion Tool Reference](CHAP_SchemaConversionTool.Reference.md) 

+  [What Is the AWS Schema Conversion Tool?](Welcome.md) 