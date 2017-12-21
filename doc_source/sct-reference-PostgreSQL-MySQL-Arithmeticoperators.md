# Conversion Issues with Arithmetic Operators<a name="sct-reference-PostgreSQL-MySQL-Arithmeticoperators"></a>

## Issue 6681: Unable to perform an automated migration of arithmetic operations with string and other types<a name="sct-reference-6681"></a>

Arithmetic operations that use a string type as one of the operands can't be automatically converted\. Modify the code to cast values as the intended type\.

## Related Topics<a name="w3ab1c37c17c11c97b5"></a>

+  [PostgreSQL to MySQL Conversion Reference](sct-reference-PostgreSQL-MySQL-overview.md) 

+  [AWS Schema Conversion Tool Reference](CHAP_SchemaConversionTool.Reference.md) 

+  [What Is the AWS Schema Conversion Tool?](Welcome.md) 