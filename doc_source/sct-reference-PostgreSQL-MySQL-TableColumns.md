# Conversion Issues with Table Columns<a name="sct-reference-PostgreSQL-MySQL-TableColumns"></a>

## Issue 6006: MySQL doesn't support %s type<a name="sct-reference-6006"></a>

Check the target data type and correct it if necessary\.

## Issue 6008: MySQL doesn't support array types for table column definition<a name="sct-reference-6008"></a>

MySQL doesn't support using an array data type for either a table column or a function variable, so this code isn't automatically converted from PostgreSQL\. Perform a manual conversion instead\.

## Issue 6011: MySQL doesn't support CIRCLE as a spatial type; the approximated results of BUFFER function of POLYGON data type is used to perform a conversion<a name="sct-reference-6011"></a>

Check the converted code, and revise it if the approximated representation doesn't meet your needs\.

## Issue 6002: MySQL doesn't support %s with precision more than 65 digits and scale more than 30 digits; the loss of precision or accuracy of data is possible<a name="sct-reference-6002"></a>

Check to see if you are converting columns whose numeric data types violate these restrictions\. If so, perform a manual migration instead\.

## Issue 6005: MySQL doesn't support INTERVAL type<a name="sct-reference-6005"></a>

Perform a manual conversion of any code that uses this data type\.

## Issue 6010: MySQL doesn't support infinite lines; a LINESTRING with two points on the line is used for conversion<a name="sct-reference-6010"></a>

Any instance of the LINE data type is converted to a LINESTRING data type\. If the two\-pointed representation is not suitable for your purposes, revise this code\.

## Issue 6009: MySQL doesn't support range types<a name="sct-reference-6009"></a>

MySQL doesn't support range data types like LONGTEXT or VARCHAR\(*length*\)\. Manually convert code that uses these data types instead\.

## Issue 6001: Unable to provide full migration for auto\-increment table columns<a name="sct-reference-6001"></a>

The PostgreSQL auto\-increment data types SMALLSERIAL, SERIAL and BIGSERIAL are converted to the MySQL SMALLINT, INT, and BIGINT data types, respectively\. If you want to enable auto\-incrementing, MySQL supports only one auto\-increment column per table and it must be a key\. Choose an appropriate column and manually update it to meet these requirements\.

## Issue 6003: MySQL doesn't support time zone information for %s type<a name="sct-reference-6003"></a>

Perform a manual conversion\.

## Issue 6004: MySQL doesn't support time zone information for %s type<a name="sct-reference-6004"></a>

Perform a manual conversion instead\. If the time zone information isn't important, you can choose DATETIME\(6\) as a target data type\. Otherwise, try to convert the data into TIMESTAMP\(6\), taking into account the value of time\_zone server setting\.

## Related Topics<a name="w3ab1c37c17c11d163c23"></a>

+  [PostgreSQL to MySQL Conversion Reference](sct-reference-PostgreSQL-MySQL-overview.md) 

+  [AWS Schema Conversion Tool Reference](CHAP_SchemaConversionTool.Reference.md) 

+  [What Is the AWS Schema Conversion Tool?](Welcome.md) 