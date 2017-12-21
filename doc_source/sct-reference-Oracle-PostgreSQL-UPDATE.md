# Conversion Issues with UPDATE<a name="sct-reference-Oracle-PostgreSQL-UPDATE"></a>

## Issue 5064: PostgreSQL doesn't support the UPDATE statement with the ERROR LOG option<a name="sct-reference-5064"></a>

You can add error records by inserting them into the log in the exception block\. Iterate through the errors in the exception block, add them to the log, and use the EXIT command when finished\.

## Issue 5558: PostgreSQL doesn't support the UPDATE statement for a PARTITION<a name="sct-reference-5558"></a>

Either insert data into the overlying partition, or perform a manual transformation using the UPDATE statement\.

## Issue 5065: PostgreSQL doesn't support the UPDATE statement for a subquery<a name="sct-reference-5065"></a>

Perform this operation on the underlying tables instead\.

## Related Topics<a name="sct-reference-Oracle-PostgreSQL-UPDATE-related"></a>

+  [Oracle to PostgreSQL Conversion Reference](sct-reference-Oracle-PostgreSQL.md) 

+  [AWS Schema Conversion Tool Reference](CHAP_SchemaConversionTool.Reference.md) 

+  [What Is the AWS Schema Conversion Tool?](Welcome.md) 