# Conversion Issues with BUILT\-IN SQL FUNCTIONS<a name="sct-reference-MySQL-PostgreSQL-BUILT-INSQLFUNCTIONS"></a>

## Issue 8811: PostgreSQL doesn't support the %s function<a name="sct-reference-8811"></a>

Create a user\-defined function\.

## Issue 8849: PostgreSQL doesn't support the %s function with parameter values %s<a name="sct-reference-8849"></a>

Create a user\-defined function\.

## Issue 8850: Some parameter values for the function %s aren't supported<a name="sct-reference-8850"></a>

Review the transformed code, and correct it if necessary\.

## Issue 8851: PostgreSQL doesn't support using aggregate functions in the SELECT list without a GROUP BY clause<a name="sct-reference-8851"></a>

In MySQL, it is possible to use an aggregate function on a field in the SELECT list without adding the other fields in the SELECT list to a GROUP BY clause\. In PostgreSQL, adding these fields to a GROUP BY clause is required\. Perform a manual conversion in this case\.

## Issue 8854: PostgreSQL doesn't support the %s function with parameters<a name="sct-reference-8854"></a>

Perform a manual conversion\.

## Related Topics<a name="sct-reference-MySQL-PostgreSQL-BUILT-INSQLFUNCTIONS-related"></a>

+  [MySQL to PostgreSQL Conversion Reference](sct-reference-MySQL-PostgreSQL.md) 

+  [AWS Schema Conversion Tool Reference](CHAP_SchemaConversionTool.Reference.md) 

+  [What Is the AWS Schema Conversion Tool?](Welcome.md) 