# Conversion Issues with LIMIT<a name="sct-reference-PostgreSQL-MySQL-LIMIT"></a>

## Issue 6611: LIMIT/OFFSET option was omitted<a name="sct-reference-6611"></a>

MySQL doesn't support use of the LIMIT or OFFSET options with the SELECT statement\. These options are dropped during conversion\. For example, take the following PostgreSQL statement\.

```
SELECT * FROM customers c offset 3;
```

This statement is converted to the following MySQL statement:

```
SELECT * FROM customers c;
```

Review the converted code, and revise it as necessary\.

## Related Topics<a name="w3ab1c37c17c11d137b5"></a>

+  [PostgreSQL to MySQL Conversion Reference](sct-reference-PostgreSQL-MySQL-overview.md) 

+  [AWS Schema Conversion Tool Reference](CHAP_SchemaConversionTool.Reference.md) 

+  [What Is the AWS Schema Conversion Tool?](Welcome.md) 