# Conversion Issues with Patterns<a name="sct-reference-PostgreSQL-MySQL-Patterns"></a>

## Issue 6607: Could not convert pattern to MySQL version; check pattern manually<a name="sct-reference-6607"></a>

MySQL doesn't support some pattern matching syntax, for example `SELECT * FROM customers where name similar to 'name';`\. Perform a manual conversion in this case\.

## Related Topics<a name="w3ab1c37c17c11d149b5"></a>

+  [PostgreSQL to MySQL Conversion Reference](sct-reference-PostgreSQL-MySQL-overview.md) 

+  [AWS Schema Conversion Tool Reference](CHAP_SchemaConversionTool.Reference.md) 

+  [What Is the AWS Schema Conversion Tool?](Welcome.md) 