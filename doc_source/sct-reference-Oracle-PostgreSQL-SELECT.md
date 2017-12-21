# Conversion Issues with SELECT<a name="sct-reference-Oracle-PostgreSQL-SELECT"></a>

## Issue 5140: PostgreSQL doesn't support BULK COLLECT INTO<a name="sct-reference-5140"></a>

Include all of the fields from your table in an INTO clause instead\.

## Issue 5139: PostgreSQL doesn't support FOR UPDATE SKIP LOCKED<a name="sct-reference-5139"></a>

Try using FOR UPDATE without SKIP LOCKED\.

## Issue 5144: PostgreSQL doesn't support FOR UPDATE WAIT clauses<a name="sct-reference-5144"></a>

Try using FOR UPDATE without WAIT\.

## Issue 5586: Automatic conversion for queries with NOCYCLE clause not supported<a name="sct-reference-5586"></a>

Perform a manual conversion\.

## Issue 5126: PostgreSQL doesn't support the MODEL statement<a name="sct-reference-5126"></a>

Revise your code\. Try using user procedures and temporary tables instead\.

## Issue 5585: Automatic conversion of an outer join into a correlation query is not supported<a name="sct-reference-5585"></a>

Perform a manual conversion\.

## Issue 5557: PostgreSQL doesn't support GROUPING SETS, CUBE, and ROLLUP functions<a name="sct-reference-5557"></a>

These functions can be emulated using CTE expressions instead\. GROUPING SETS, CUBE, and ROLLUP functionality is available in PostgreSQL v\.9\.5 or higher\.

## Issue 5578: Unable to automatically transform the SELECT statement<a name="sct-reference-5578"></a>

The indicated SELECT statement contains language that can't be converted, for example an unsupported function\. Try rewriting the statement\.

## Related Topics<a name="sct-reference-Oracle-PostgreSQL-SELECT-related"></a>

+  [Oracle to PostgreSQL Conversion Reference](sct-reference-Oracle-PostgreSQL.md) 

+  [AWS Schema Conversion Tool Reference](CHAP_SchemaConversionTool.Reference.md) 

+  [What Is the AWS Schema Conversion Tool?](Welcome.md) 