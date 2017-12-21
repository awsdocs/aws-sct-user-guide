# Conversion Issues with SYNONYMS<a name="sct-reference-Microsoft-SQL-Server-PostgreSQL-SYNONYMS"></a>

## Issue 7792: PostgreSQL doesn't support synonyms<a name="sct-reference-7792"></a>

PostgreSQL doesn't support the CREATE SYNONYM statement\. To convert, replace the synonym in any statement with the original database object\. If the original object is a table or view, you can try to create a view in one database that relies on a table or view in another database\.

## Related Topics<a name="sct-reference-Microsoft-SQL-Server-PostgreSQL-SYNONYMS-related"></a>

+  [Microsoft SQL Server to PostgreSQL Conversion Issue Reference](sct-reference-Microsoft-SQL-Server-PostgreSQL.md) 

+  [AWS Schema Conversion Tool Reference](CHAP_SchemaConversionTool.Reference.md) 

+  [What Is the AWS Schema Conversion Tool?](Welcome.md) 