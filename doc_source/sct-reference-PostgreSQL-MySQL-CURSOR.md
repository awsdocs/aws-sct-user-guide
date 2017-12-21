# Conversion Issues with CURSOR<a name="sct-reference-PostgreSQL-MySQL-CURSOR"></a>

## Issue 6639: MySQL doesn't support the direction clause<a name="sct-reference-6639"></a>

MySQL doesn't support the following direction clauses when using FETCH with cursors:

+ ABSOLUTE 2

+ BACKWARD

+ FIRST FROM

+ FORWARD

+ LAST FROM

+ PRIOR FROM

+ RELATIVE 2

+ RELATIVE 3

Perform a manual conversion in these cases\.

## Issue 6640: MySQL doesn't support the MOVE option<a name="sct-reference-6640"></a>

Revise your code to eliminate cursors with the MOVE option\.

## Issue 6638: MySQL doesn't support the SCROLL option in cursors<a name="sct-reference-6638"></a>

Revise your code to eliminate cursors with the SCROLL option\.

## Issue 6337: MySQL doesn't support a variable of REFCURSOR type<a name="sct-reference-6337"></a>

Try revising the code to use temporary tables instead\.

## Related Topics<a name="w3ab1c37c17c11d107c11"></a>

+  [PostgreSQL to MySQL Conversion Reference](sct-reference-PostgreSQL-MySQL-overview.md) 

+  [AWS Schema Conversion Tool Reference](CHAP_SchemaConversionTool.Reference.md) 

+  [What Is the AWS Schema Conversion Tool?](Welcome.md) 