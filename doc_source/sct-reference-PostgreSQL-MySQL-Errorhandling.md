# Conversion Issues with Error Handling<a name="sct-reference-PostgreSQL-MySQL-Errorhandling"></a>

## Issue 6665: MySQL doesn't support the GET \[ CURRENT \] DIAGNOSTICS command<a name="sct-reference-6665"></a>

Perform a manual conversion\.

## Issue 6664: MySQL doesn't support the condition information %s<a name="sct-reference-6664"></a>

Some of the condition information items that are used with the GET STACKED DIAGNOSTICS statement in PostgreSQL are not supported by MySQL\. These include the following:

+ PG\_DATATYPE\_NAME

+ TABLE\_NAME

+ SCHEMA\_NAME

+ PG\_EXCEPTION\_DETAIL

+ PG\_EXCEPTION\_HINT

+ PG\_EXCEPTION\_CONTEXT

Manually convert the code wherever you use these condition information items\.

## Issue 6329: MySQL doesn't support the RAISE exception<a name="sct-reference-6329"></a>

Review the RAISE exception used, and if possible convert it to an exception using the SIGNAL or RESIGNAL statement\.

## Related Topics<a name="w3ab1c37c17c11d119b9"></a>

+  [PostgreSQL to MySQL Conversion Reference](sct-reference-PostgreSQL-MySQL-overview.md) 

+  [AWS Schema Conversion Tool Reference](CHAP_SchemaConversionTool.Reference.md) 

+  [What Is the AWS Schema Conversion Tool?](Welcome.md) 