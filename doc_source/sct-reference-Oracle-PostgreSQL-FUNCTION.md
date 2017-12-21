# Conversion Issues with FUNCTION<a name="sct-reference-Oracle-PostgreSQL-FUNCTION"></a>

## Issue 5350: The function can't use statements that explicitly or implicitly begin or end a transaction, such as START TRANSACTION, COMMIT, or ROLLBACK<a name="sct-reference-5350"></a>

Revise your code to implement transaction control on the application side\. Some cases that use SAVEPOINT <name>… ROLLBACK TO <name> can be converted to BEGIN … EXCEPTION … END\.

## Related Topics<a name="sct-reference-Oracle-PostgreSQL-FUNCTION-related"></a>

+  [Oracle to PostgreSQL Conversion Reference](sct-reference-Oracle-PostgreSQL.md) 

+  [AWS Schema Conversion Tool Reference](CHAP_SchemaConversionTool.Reference.md) 

+  [What Is the AWS Schema Conversion Tool?](Welcome.md) 