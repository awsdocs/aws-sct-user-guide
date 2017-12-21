# Conversion Issues with INSERT<a name="sct-reference-Oracle-PostgreSQL-INSERT"></a>

## Issue 5070: PostgreSQL doesn't support the INSERT statement with the ERROR LOG option<a name="sct-reference-5070"></a>

You can add error records by inserting them into the log in the exception block\. Iterate through the errors in the exception block, add them to the log, and use the EXIT command when finished\.

## Issue 5024: PostgreSQL doesn't support the INSERT statement with partition\_extension\_clause<a name="sct-reference-5024"></a>

Perform a manual conversion for the partition types that aren't supported\.

## Issue 5071: PostgreSQL doesn't support the INSERT statement for a subquery<a name="sct-reference-5071"></a>

Perform this operation on the underlying tables instead\.

## Issue 5090: PostgreSQL doesn't support the INSERT statement for a SUBPARTITION<a name="sct-reference-5090"></a>

Either insert data into the overlying partition, or perform a manual conversion using the INSERT statement\.

## Related Topics<a name="sct-reference-Oracle-PostgreSQL-INSERT-related"></a>

+  [Oracle to PostgreSQL Conversion Reference](sct-reference-Oracle-PostgreSQL.md) 

+  [AWS Schema Conversion Tool Reference](CHAP_SchemaConversionTool.Reference.md) 

+  [What Is the AWS Schema Conversion Tool?](Welcome.md) 