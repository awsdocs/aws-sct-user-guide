# Conversion Issues with DDL<a name="sct-reference-Microsoft-SQL-Server-PostgreSQL-DDL"></a>

## Issue 7675: PostgreSQL doesn't support sorting options \(ASC | DESC\) for constraints<a name="sct-reference-7675"></a>

Remove these options from indexes and constraints\.

## Issue 7681: PostgreSQL doesn't support clustered indexes<a name="sct-reference-7681"></a>

Use nonclustered indexes\.

## Issue 7682: PostgreSQL doesn't support the INCLUDE option in indexes<a name="sct-reference-7682"></a>

Use the index without this option\.

## Issue 7781: PostgreSQL doesn't support the PAD\_INDEX option in indexes<a name="sct-reference-7781"></a>

Use the index without this option\.

## Issue 7782: PostgreSQL doesn't support the SORT\_IN\_TEMPDB option in indexes<a name="sct-reference-7782"></a>

Use the index without this option\.

## Issue 7783: PostgreSQL doesn't support the IGNORE\_DUP\_KEY option in indexes<a name="sct-reference-7783"></a>

Use the index without this option\.

## Issue 7784: PostgreSQL doesn't support the STATISTICS\_NORECOMPUTE option in indexes<a name="sct-reference-7784"></a>

Use the index without this option\.

## Issue 7785: PostgreSQL doesn't support the STATISTICS\_INCREMENTAL option in indexes<a name="sct-reference-7785"></a>

Use the index without this option\.

## Issue 7786: PostgreSQL doesn't support the DROP\_EXISTING option in indexes<a name="sct-reference-7786"></a>

Use the index without this option\.

## Issue 7787: PostgreSQL doesn't support the ONLINE option in indexes<a name="sct-reference-7787"></a>

Use the index without this option\.

## Issue 7788: PostgreSQL doesn't support the ALLOW\_ROW\_LOCKS option in indexes<a name="sct-reference-7788"></a>

Use index without this option\.

## Issue 7789: PostgreSQL doesn't support the ALLOW\_PAGE\_LOCKS option in indexes<a name="sct-reference-7789"></a>

Use index without this option\.

## Issue 7790: PostgreSQL doesn't support the MAXDOP option in indexes<a name="sct-reference-7790"></a>

Use index without this option\.

## Issue 7791: PostgreSQL doesn't support the DATA\_COMPRESSION option in indexes<a name="sct-reference-7791"></a>

Use index without this option\.

## Issue 7679: PostgreSQL doesn't support computed columns<a name="sct-reference-7679"></a>

Try using a trigger instead\.

## Issue 7680: PostgreSQL doesn't support global temporary tables<a name="sct-reference-7680"></a>

Use local temporary or regular tables\.

## Issue 7812: Temporary table must be removed before the end of the function<a name="sct-reference-7812"></a>

Review your transformed code and modify it if necessary\.

## Issue 7825: The default value for a DateTime column removed<a name="sct-reference-7825"></a>

Review generated code and modify it if necessary\.

## Issue 7776: Automatic migration of inline functions not supported<a name="sct-reference-7776"></a>

Perform a manual conversion\.

## Related Topics<a name="sct-reference-Microsoft-SQL-Server-PostgreSQL-DDL-related"></a>

+  [Microsoft SQL Server to PostgreSQL Conversion Issue Reference](sct-reference-Microsoft-SQL-Server-PostgreSQL.md) 

+  [AWS Schema Conversion Tool Reference](CHAP_SchemaConversionTool.Reference.md) 

+  [What Is the AWS Schema Conversion Tool?](Welcome.md) 