# Conversion Issues with TRANSACTION<a name="sct-reference-MySQL-PostgreSQL-TRANSACTION"></a>

## Issue 8807: PostgreSQL doesn't support transactions in functions<a name="sct-reference-8807"></a>

Code that uses transaction management statements such as START TRANSACTION or COMMIT within a function or stored procedure can't be automatically converted\. Perform a manual conversion instead\.

## Related Topics<a name="sct-reference-MySQL-PostgreSQL-TRANSACTION-related"></a>

+  [MySQL to PostgreSQL Conversion Reference](sct-reference-MySQL-PostgreSQL.md) 

+  [AWS Schema Conversion Tool Reference](CHAP_SchemaConversionTool.Reference.md) 

+  [What Is the AWS Schema Conversion Tool?](Welcome.md) 