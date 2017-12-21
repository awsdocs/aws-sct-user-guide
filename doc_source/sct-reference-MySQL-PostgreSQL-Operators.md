# Conversion Issues with Operators<a name="sct-reference-MySQL-PostgreSQL-Operators"></a>

## Issue 8773: The tool can not currently perform automated migration of arithmetic operations with dates<a name="sct-reference-8773"></a>

Perform a manual conversion\.

## Issue 8774: The tool can not currently perform automated migration of arithmetic operations with mixed types of operands<a name="sct-reference-8774"></a>

Code that uses an arithmetic operator and has one operand that has a DATE, TIME or TIMESTAMP data type can't be automatically converted\. For example, `set d = now() + 1;`\. Perform a manual conversion instead\.

## Related Topics<a name="sct-reference-MySQL-PostgreSQL-Operators-related"></a>

+  [MySQL to PostgreSQL Conversion Reference](sct-reference-MySQL-PostgreSQL.md) 

+  [AWS Schema Conversion Tool Reference](CHAP_SchemaConversionTool.Reference.md) 

+  [What Is the AWS Schema Conversion Tool?](Welcome.md) 