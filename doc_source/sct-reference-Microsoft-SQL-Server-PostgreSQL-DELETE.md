# Conversion Issues with DELETE<a name="sct-reference-Microsoft-SQL-Server-PostgreSQL-DELETE"></a>

## Issue 7623: PostgreSQL doesn't support hints in DELETE statements\. The conversion skips options in the format WITH\(Table\_Hint\_Limited\)\.<a name="sct-reference-7623"></a>

PostgreSQL doesn't support usings hints \(for example, WITH FORCESCAN\) to override the default behavior of the query optimizer when executing Data Manipulation Language \(DML\) statements\. Use PostgreSQL methods for performance tuning instead\.

## Issue 7798: PostgreSQL doesn't support TOP option in the operator DELETE<a name="sct-reference-7798"></a>

Perform a manual conversion for any DELETE statements that contain a TOP argument, as in the example following\.

```
delete top (<expression >)[PERCENT] from <table-name>;
```

In PostgreSQL, you can use a subquery in the WHERE clause to identify the rows you want to delete\.

## Related Topics<a name="sct-reference-Microsoft-SQL-Server-PostgreSQL-DELETE-related"></a>

+  [Microsoft SQL Server to PostgreSQL Conversion Issue Reference](sct-reference-Microsoft-SQL-Server-PostgreSQL.md) 

+  [AWS Schema Conversion Tool Reference](CHAP_SchemaConversionTool.Reference.md) 

+  [What Is the AWS Schema Conversion Tool?](Welcome.md) 