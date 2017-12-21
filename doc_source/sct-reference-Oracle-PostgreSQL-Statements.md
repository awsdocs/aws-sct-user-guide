# Conversion Issues with Statements<a name="sct-reference-Oracle-PostgreSQL-Statements"></a>

## Issue 5335: PostgreSQL doesn't support the GOTO operator<a name="sct-reference-5335"></a>

 PostgreSQL doesn't support the GOTO operator in stored procedures\. Try one of the following alternatives instead:

+ Set a flag and test for it\.

+ Return from the procedure if updates should be made, and add the updates after the return\.

+ Put the updates in another stored procedure, and call it in your IF statements\.

## Related Topics<a name="sct-reference-Oracle-PostgreSQL-Statements-related"></a>

+  [Oracle to PostgreSQL Conversion Reference](sct-reference-Oracle-PostgreSQL.md) 

+  [AWS Schema Conversion Tool Reference](CHAP_SchemaConversionTool.Reference.md) 

+  [What Is the AWS Schema Conversion Tool?](Welcome.md) 