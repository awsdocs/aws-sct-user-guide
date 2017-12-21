# Conversion Issues with DELETE<a name="sct-reference-PostgreSQL-MySQL-DELETE"></a>

## Issue 6069: MySQL doesn't support the DELETE statement with the RETURNING option<a name="sct-reference-6069"></a>

To convert this operation, change the DELETE statement with the RETURNING clause into a DELETE statement with following INSERT statements, and use the same key conditions in each INSERT\. 

## Issue 6672: MySQL does not support delete by cursor<a name="sct-reference-6672"></a>

MySQL doesn't support using a DELETE statement within a cursor\. Perform a manual conversion in this case\.

## Related Topics<a name="w3ab1c37c17c11d113b7"></a>

+  [PostgreSQL to MySQL Conversion Reference](sct-reference-PostgreSQL-MySQL-overview.md) 

+  [AWS Schema Conversion Tool Reference](CHAP_SchemaConversionTool.Reference.md) 

+  [What Is the AWS Schema Conversion Tool?](Welcome.md) 