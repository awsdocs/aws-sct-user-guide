# Conversion Issues with Operators and Date Functions<a name="sct-reference-PostgreSQL-MySQL-OperatorsandDateFunctions"></a>

## Issue 6660: Unable to convert the %s operation with the interval value as one or more arguments<a name="sct-reference-6660"></a>

Some operations with arguments that use an interval data type can't be converted, for example `SELECT INTERVAL '1-1' YEAR TO MONTH * 2;`\. Perform a manual conversion in this case\.

## Issue 6661: The operation will return the number of days instead of the interval value<a name="sct-reference-6661"></a>

After conversion, some calculations that use date or time data types return the number of days rather than an interval value as they did previously, for example `SELECT TIMESTAMP '2012-01-01 09:30:15.01' - DATE '2010-01-01';`\. Check to see if the new return type meets your requirements, and revise the code if necessary\.

## Issue 6662: Unsupported format for the interval's value<a name="sct-reference-6662"></a>

Currently, the only supported format for a literal value assigned to an interval data type is SQL ANSI\. Perform a manual conversion in the case of an unsupported format\.

## Related Topics<a name="w3ab1c37c17c11d143b9"></a>

+  [PostgreSQL to MySQL Conversion Reference](sct-reference-PostgreSQL-MySQL-overview.md) 

+  [AWS Schema Conversion Tool Reference](CHAP_SchemaConversionTool.Reference.md) 

+  [What Is the AWS Schema Conversion Tool?](Welcome.md) 