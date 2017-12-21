# Conversion Issues with CURSORS<a name="sct-reference-Microsoft-SQL-Server-PostgreSQL-CURSORS"></a>

## Issue 7637: PostgreSQL doesn't support GLOBAL CURSORS\. Requires manual conversion\.<a name="sct-reference-7637"></a>

Change the global cursor to a local cursor, or revise your code so it doesn't require global cursors\.

## Issue 7639: PostgreSQL doesn't support DYNAMIC cursors<a name="sct-reference-7639"></a>

Revise your code to remove the DYNAMIC option from any cursors\.

## Issue 7701: Setting this option corresponds to the typical behavior of cursors in PostgreSQL, so this option is skipped<a name="sct-reference-7701"></a>

The FAST\_FORWARD option is skipped during conversion, because PostgreSQL cursors provide the same behavior as the FAST\_FORWARD option by default\. Review your transformed code and modify it if necessary\. 

## Issue 7803: PostgreSQL doesn't support the option FOR UPDATE, so this option is skipped<a name="sct-reference-7803"></a>

The FOR\_UPDATE option is skipped during conversion because PostgreSQL doesn't support it\. Review your transformed code and modify it if necessary\.

## Issue 7700: The membership and order of rows never changes for cursors in PostgreSQL, so this option is skipped<a name="sct-reference-7700"></a>

Use cursors without this option\.

## Issue 7704: PostgreSQL doesn't support the option OPTIMISTIC, so this option is skipped<a name="sct-reference-7704"></a>

Use cursors without this option\.

## Issue 7702: All PostgreSQL cursors are read\-only, so this option is skipped<a name="sct-reference-7702"></a>

Use cursors without this option\.

## Issue 7705: PostgreSQL doesn't support the option TYPE\_WARNING, so this option is skipped<a name="sct-reference-7705"></a>

Use cursors without this option\.

## Related Topics<a name="sct-reference-Microsoft-SQL-Server-PostgreSQL-CURSORS-related"></a>

+  [Microsoft SQL Server to PostgreSQL Conversion Issue Reference](sct-reference-Microsoft-SQL-Server-PostgreSQL.md) 

+  [AWS Schema Conversion Tool Reference](CHAP_SchemaConversionTool.Reference.md) 

+  [What Is the AWS Schema Conversion Tool?](Welcome.md) 