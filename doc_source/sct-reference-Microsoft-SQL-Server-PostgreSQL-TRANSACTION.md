# Conversion Issues with TRANSACTION<a name="sct-reference-Microsoft-SQL-Server-PostgreSQL-TRANSACTION"></a>

## Issue 7807: Transactions in functions PostgreSQL doesn't support<a name="sct-reference-7807"></a>

Perform a manual conversion to correct this issue\.

PostgreSQL supports local transactions within a given client session\. You must manually convert Microsoft SQL Server transactions to use the PostgreSQL transaction management statements instead\. PostgreSQL doesn't support named or distributed transactions, marking transactions, or transaction management within functions\. For more information about using transactions in PostgreSQL, see [TRANSACTIONS](http://www.postgresql.org/docs/9.5/static/tutorial-transactions.html) in the PostgreSQL documentation\.

## Related Topics<a name="sct-reference-Microsoft-SQL-Server-PostgreSQL-TRANSACTION-related"></a>

+  [Microsoft SQL Server to PostgreSQL Conversion Issue Reference](sct-reference-Microsoft-SQL-Server-PostgreSQL.md) 

+  [AWS Schema Conversion Tool Reference](CHAP_SchemaConversionTool.Reference.md) 

+  [What Is the AWS Schema Conversion Tool?](Welcome.md) 