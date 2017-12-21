# Conversion Issues with SELECT<a name="sct-reference-Microsoft-SQL-Server-PostgreSQL-SELECT"></a>

## Issue 7653: PostgreSQL doesn't support the option GROUP BY ROLLUP\. Automatic conversion can't be performed\.<a name="sct-reference-7653"></a>

Try creating a stored procedure to replace the query\.

## Issue 7654: PostgreSQL doesn't support the option GROUP BY CUBE\. Automatic conversion can't be performed\.<a name="sct-reference-7654"></a>

Try creating a stored procedure to replace the query\.

## Issue 7655: PostgreSQL doesn't support the option GROUP BY GROUPING SETS\. Automatic conversion can't be performed\.<a name="sct-reference-7655"></a>

Try creating a stored procedure to replace the query\.

## Issue 7646: PostgreSQL doesn't support the COLLATE option in the ORDER BY clause\. Automatic conversion can't be performed\.<a name="sct-reference-7646"></a>

You must use the collation settings that were assigned when the database was created\.

## Issue 7687: PostgreSQL doesn't support the CONTAINS predicate<a name="sct-reference-7687"></a>

Perform a manual conversion by re\-writing the SELECT statement to use PostgreSQL full\-text search functionality instead\. For more information about full\-text search in PostgreSQL, see [Tables and Indexes](http://www.postgresql.org/docs/current/static/textsearch-tables.html) in the PostgreSQL documentation\.

## Issue 7688: PostgreSQL doesn't support the FREETEXT predicate<a name="sct-reference-7688"></a>

Perform a manual conversion by re\-writing the SELECT statement to use PostgreSQL full\-text search functionality instead\. For more information about full\-text search in PostgreSQL, see [Tables and Indexes](http://www.postgresql.org/docs/current/static/textsearch-tables.html) in the PostgreSQL documentation\.

## Issue 7795: PostgreSQL is case sensitive\. Check the string comparison\.<a name="sct-reference-7795"></a>

Check string comparisons in the WHERE clauses of statements, for example `WHERE [Name] LIKE '%BLOCKED%';`\. All strings used in comparisons must be lowercase\.

## Issue 7605: PostgreSQL doesn't support the WITH TIES option<a name="sct-reference-7605"></a>

Perform a manual conversion of any TOP statements that use the WITH TIES clause\. You can use the rank\(\) [window function](http://www.postgresql.org/docs/9.5/static/functions-window.html) in PostgreSQL to provide similar results\.

## Related Topics<a name="sct-reference-Microsoft-SQL-Server-PostgreSQL-SELECT-related"></a>

+  [Microsoft SQL Server to PostgreSQL Conversion Issue Reference](sct-reference-Microsoft-SQL-Server-PostgreSQL.md) 

+  [AWS Schema Conversion Tool Reference](CHAP_SchemaConversionTool.Reference.md) 

+  [What Is the AWS Schema Conversion Tool?](Welcome.md) 