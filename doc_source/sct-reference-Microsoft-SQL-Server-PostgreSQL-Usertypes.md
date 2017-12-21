# Conversion Issues with User Types<a name="sct-reference-Microsoft-SQL-Server-PostgreSQL-Usertypes"></a>

## Issue 7794: PostgreSQL doesn't support user\-defined data types<a name="sct-reference-7794"></a>

To correct this issue, perform a manual conversion of each sp\_ addtype or CREATE TYPE statement in Microsoft SQL Server to a CREATE TYPE statement in PostgreSQL\. For more information about creating a user\-defined data type in PostgreSQL, see [CREATE TYPE](http://www.postgresql.org/docs/9.5/static/sql-createtype.html) in the PostgreSQL documentation\.

## Related Topics<a name="sct-reference-Microsoft-SQL-Server-PostgreSQL-Usertypes-related"></a>

+  [Microsoft SQL Server to PostgreSQL Conversion Issue Reference](sct-reference-Microsoft-SQL-Server-PostgreSQL.md) 

+  [AWS Schema Conversion Tool Reference](CHAP_SchemaConversionTool.Reference.md) 

+  [What Is the AWS Schema Conversion Tool?](Welcome.md) 