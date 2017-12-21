# Conversion Issues with FROM<a name="sct-reference-PostgreSQL-MySQL-FROM"></a>

## Issue 6603: Can't use function in from clause<a name="sct-reference-6603"></a>

Code that selects from a function, for example `SELECT * FROM function_name;`, isn't converted\. Perform a manual conversion in this case\.

## Issue 6682: Can't use the table\-value function in the from clause<a name="sct-reference-6682"></a>

MySQL does not support the table\-value function\. Perform a manual conversion in this case\.

## Related Topics<a name="w3ab1c37c17c11d123b7"></a>

+  [PostgreSQL to MySQL Conversion Reference](sct-reference-PostgreSQL-MySQL-overview.md) 

+  [AWS Schema Conversion Tool Reference](CHAP_SchemaConversionTool.Reference.md) 

+  [What Is the AWS Schema Conversion Tool?](Welcome.md) 