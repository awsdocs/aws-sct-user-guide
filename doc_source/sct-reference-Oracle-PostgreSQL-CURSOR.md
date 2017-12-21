# Conversion Issues with CURSOR<a name="sct-reference-Oracle-PostgreSQL-CURSOR"></a>

## Issue 5084: PostgreSQL doesn't support the cursor attribute %ISOPEN<a name="sct-reference-5084"></a>

Revise how you are using this attribute in your code\.

## Issue 5226: PostgreSQL doesn't support TYPE \.\.\. IS REF CURSOR<a name="sct-reference-5226"></a>

PostgreSQL doesn't support the TYPE <type\_name> IS REF CURSOR statement\. Change the function to a stored procedure and try using a table to store results instead\.

## Related Topics<a name="sct-reference-Oracle-PostgreSQL-CURSOR-related"></a>

+  [Oracle to PostgreSQL Conversion Reference](sct-reference-Oracle-PostgreSQL.md) 

+  [AWS Schema Conversion Tool Reference](CHAP_SchemaConversionTool.Reference.md) 

+  [What Is the AWS Schema Conversion Tool?](Welcome.md) 