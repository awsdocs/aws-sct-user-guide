# Conversion Issues with CONTROL FLOW<a name="sct-reference-Microsoft-SQL-Server-PostgreSQL-CONTROLFLOW"></a>

## Issue 7800: PostgreSQL doesn't support result sets in the style of MSSQL<a name="sct-reference-7800"></a>

Review your transformed code and modify it if necessary\.

## Issue 7801: The table can be locked open cursor<a name="sct-reference-7801"></a>

In Microsoft SQL Server, a local temporary table created in a stored procedure is dropped automatically when the stored procedure completes\. Temporary tables in PostgreSQL are automatically dropped at the end of a session\. The conversion uses the DROP TABLE IF EXISTS statement to emulate this behavior and remove the temporary table before the end of the function that created it\. In some cases though, this statement might fail because the temporary table is locked due to an open cursor\. In this case, the DROP TABLE statement must be commented out\. Review your transformed code and modify it if necessary\.

## Issue 7802: A table that is created within the procedure, must be deleted before the end of the procedure<a name="sct-reference-7802"></a>

Review your transformed code and modify it if necessary\.

## Issue 7826: Check the default value for a DateTime variable<a name="sct-reference-7826"></a>

Check the default value for a DateTime variable\.

## Issue 7628: PostgreSQL doesn't support the GOTO option\. Automatic conversion can't be performed\.<a name="sct-reference-7628"></a>

Revise your code to eliminate GOTO operators, using BEGIN\.\.\.END blocks in combination with EXIT, REPEAT, UNTIL, and WHILE operators\.

## Issue 7821: Automatic conversion operator WAITFOR with a variable is not supported<a name="sct-reference-7821"></a>

You must perform a manual conversion in cases where you have a WAITFOR DELAY statement that uses a variable, for example `WAITFOR DELAY @time;`, instead of a literal value, for example `WAITFOR DELAY '00:00:05';`\. 

## Issue 7691: PostgreSQL doesn't support WAITFOR TIME feature<a name="sct-reference-7691"></a>

Perform a manual conversion\.

## Related Topics<a name="sct-reference-Microsoft-SQL-Server-PostgreSQL-CONTROLFLOW-related"></a>

+  [Microsoft SQL Server to PostgreSQL Conversion Issue Reference](sct-reference-Microsoft-SQL-Server-PostgreSQL.md) 

+  [AWS Schema Conversion Tool Reference](CHAP_SchemaConversionTool.Reference.md) 

+  [What Is the AWS Schema Conversion Tool?](Welcome.md) 