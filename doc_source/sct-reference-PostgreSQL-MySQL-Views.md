# Conversion Issues with Views<a name="sct-reference-PostgreSQL-MySQL-Views"></a>

## Issue 6072: MySQL doesn't support default values for the view's column<a name="sct-reference-6072"></a>

MySQL doesn't support specifying a default value when creating or altering a view, as shown in the following example\.

```
ALTER VIEW test_pg_mysql.v_default_values 
  ALTER n SET DEFAULT 10;
```

If you need this functionality, perform a manual conversion instead\.

## Issue 6071: MySQL doesn't support row\-level security<a name="sct-reference-6071"></a>

If the same functionality is necessary, perform a manual conversion instead\.

## Issue 6070: MySQL doesn't support temporary views or views on temporary tables<a name="sct-reference-6070"></a>

Perform a manual conversion instead\.

## Related Topics<a name="w3ab1c37c17c11d181b9"></a>

+  [PostgreSQL to MySQL Conversion Reference](sct-reference-PostgreSQL-MySQL-overview.md) 

+  [AWS Schema Conversion Tool Reference](CHAP_SchemaConversionTool.Reference.md) 

+  [What Is the AWS Schema Conversion Tool?](Welcome.md) 