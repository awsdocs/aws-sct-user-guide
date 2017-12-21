# Conversion Issues with ROW, RECORD type<a name="sct-reference-PostgreSQL-MySQL-ROW-RECORDtype"></a>

## Issue 6606: MySQL doesn't support ROW\(\) function with any, some, or all predicates<a name="sct-reference-6606"></a>

MySQL doesn't support the ROW\(\) function with the any, some, or all predicates, for example `SELECT * FROM customers c where ROW(c.id, c.postcode) <= all (select id, order_sum from orders where id = c.id);`\. Perform a manual conversion instead\.

## Issue 6668: MySQL doesn't support ROW/RECORD type<a name="sct-reference-6668"></a>

Perform a manual conversion\.

## Related Topics<a name="w3ab1c37c17c11d151b7"></a>

+  [PostgreSQL to MySQL Conversion Reference](sct-reference-PostgreSQL-MySQL-overview.md) 

+  [AWS Schema Conversion Tool Reference](CHAP_SchemaConversionTool.Reference.md) 

+  [What Is the AWS Schema Conversion Tool?](Welcome.md) 