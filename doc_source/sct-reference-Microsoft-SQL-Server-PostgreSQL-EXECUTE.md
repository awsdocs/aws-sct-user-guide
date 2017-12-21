# Conversion Issues with EXECUTE<a name="sct-reference-Microsoft-SQL-Server-PostgreSQL-EXECUTE"></a>

## Issue 7695: PostgreSQL doesn't support the execution of a procedure as a variable<a name="sct-reference-7695"></a>

Perform a manual conversion \(one possibility is to use dynamic SQL\)\. This issue occurs when you pass in the name of a procedure to an EXECUTE statement by using a variable, as in the example following\.

```
ALTER PROCEDURE [dbo].[PROC_EXECUTE_009]
AS
 SET NOCOUNT ON
BEGIN
  declare @v_ID int;
  declare @v_ProcName varchar(20) = '[dbo].[PROC_DML_015]';
  exec @v_ProcName 
    @v_ID output
```

## Issue 7672: Automatic conversion of this command is not supported<a name="sct-reference-7672"></a>

This issue is often caused by an EXECUTE statement that executes a string or variable, for example `EXEC('select * from Customer');` or `EXEC(@variable);`\. Convert each of these statements to a pair of [PREPARE](http://www.postgresql.org/docs/9.5/static/sql-prepare.html) and [EXECUTE](http://www.postgresql.org/docs/9.5/static/sql-execute.html) statements in PostgreSQL\.

## Issue 7645: PostgreSQL doesn't support executing a pass\-through command on a linked server<a name="sct-reference-7645"></a>

Use other methods to execute statements on a remote server\.

## Issue 7640: The EXECUTE with RECOMPILE option is ignored<a name="sct-reference-7640"></a>

Use the EXECUTE command without this option\.

## Issue 7643: The EXECUTE with RESULT SETS <result set definition> option is ignored<a name="sct-reference-7643"></a>

Use the EXECUTE command without this option\.

## Issue 7642: The EXECUTE with RESULT SETS NONE option is ignored<a name="sct-reference-7642"></a>

Use the EXECUTE command without this option\.

## Issue 7641: The EXECUTE with RESULT SETS UNDEFINED option is ignored<a name="sct-reference-7641"></a>

Use the EXECUTE command without this option\.

## Related Topics<a name="sct-reference-Microsoft-SQL-Server-PostgreSQL-EXECUTE-related"></a>

+  [Microsoft SQL Server to PostgreSQL Conversion Issue Reference](sct-reference-Microsoft-SQL-Server-PostgreSQL.md) 

+  [AWS Schema Conversion Tool Reference](CHAP_SchemaConversionTool.Reference.md) 

+  [What Is the AWS Schema Conversion Tool?](Welcome.md) 