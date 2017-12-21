# Conversion Issues with Unknown<a name="sct-reference-Microsoft-SQL-Server-PostgreSQL-Unknown"></a>

## Issue 7627: This syntactic element conversion is not supported yet<a name="sct-reference-7627"></a>

Perform a manual conversion\.

## Issue 7674: Automatic conversion of <clause name> clause of <statement name> statement is not supported<a name="sct-reference-7674"></a>

Perform a manual conversion to correct this issue\.

A common cause of this issue is SET statements in Microsoft SQL Server that affect current session handling \(a complete list of these SET statements is available at [SET Statements \(Transact\-SQL\)](http://msdn.microsoft.com/en-us/library/ms190356.aspx)\)\. These statements are not supported in PostgreSQL, so you need to perform a manual conversion to a PostgreSQL SET statement\. For more information about using a SET statement in PostgreSQL, see [SET](http://www.postgresql.org/docs/9.5/static/sql-set.html) in the PostgreSQL documentation\.

## Issue 7808: Unparsed SQL<a name="sct-reference-7808"></a>

Perform a manual conversion\.

## Related Topics<a name="sct-reference-Microsoft-SQL-Server-PostgreSQL-Unknown-related"></a>

+  [Microsoft SQL Server to PostgreSQL Conversion Issue Reference](sct-reference-Microsoft-SQL-Server-PostgreSQL.md) 

+  [AWS Schema Conversion Tool Reference](CHAP_SchemaConversionTool.Reference.md) 

+  [What Is the AWS Schema Conversion Tool?](Welcome.md) 