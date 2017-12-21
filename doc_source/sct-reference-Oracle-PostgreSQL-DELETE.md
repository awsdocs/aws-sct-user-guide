# Conversion Issues with DELETE<a name="sct-reference-Oracle-PostgreSQL-DELETE"></a>

## Issue 5067: PostgreSQL doesn't support the DELETE statement with the ERROR LOG option<a name="sct-reference-5067"></a>

You can add error records by inserting them into the log in the exception block\. Iterate through the errors in the exception block, add them to the log, and use the EXIT command when finished\.

## Issue 5098: PostgreSQL doesn't support the DELETE statement for a PARTITION<a name="sct-reference-5098"></a>

Either insert data into the overlying partition, or perform a manual conversion using the DELETE statement\.

## Issue 5068: PostgreSQL doesn't support the DELETE statement for a subquery<a name="sct-reference-5068"></a>

Perform this operation on the underlying tables instead\.

## Related Topics<a name="sct-reference-Oracle-PostgreSQL-DELETE-related"></a>

+  [Oracle to PostgreSQL Conversion Reference](sct-reference-Oracle-PostgreSQL.md) 

+  [AWS Schema Conversion Tool Reference](CHAP_SchemaConversionTool.Reference.md) 

+  [What Is the AWS Schema Conversion Tool?](Welcome.md) 