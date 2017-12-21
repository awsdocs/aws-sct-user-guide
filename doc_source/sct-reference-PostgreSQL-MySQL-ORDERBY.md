# Conversion Issues with ORDER BY<a name="sct-reference-PostgreSQL-MySQL-ORDERBY"></a>

## Issue 6610: AI nulls first/last transformation was performed<a name="sct-reference-6610"></a>

MySQL doesn't support the NULLS FIRST or NULLS LAST options with the SELECT statement\. Instances of this language are converted to use the isnull\(\) function instead\. For example, take the following PostgreSQL statements\.

```
 SELECT * FROM customers c order by id nulls last;
 SELECT * FROM customers c order by id desc nulls first;
```

These statements are converted to the following MySQL statements\.

```
 SELECT * FROM customers c order by isnull(id), id;
 SELECT * FROM customers c order by isnull(id) desc, id desc;
```

Review the converted code, and revise it if necessary\.

## Issue 6609: ORDER option was omitted because MySQL doesn't support key word USING in order by clause<a name="sct-reference-6609"></a>

MySQL doesn't support the ORDER BY *field\_name* USING clause, for example `SELECT * FROM customers c order by id using >;`\. During conversion, the ORDER BY clause is dropped\. Review this code and revise it if necessary\.

## Related Topics<a name="w3ab1c37c17c11d145b7"></a>

+  [PostgreSQL to MySQL Conversion Reference](sct-reference-PostgreSQL-MySQL-overview.md) 

+  [AWS Schema Conversion Tool Reference](CHAP_SchemaConversionTool.Reference.md) 

+  [What Is the AWS Schema Conversion Tool?](Welcome.md) 