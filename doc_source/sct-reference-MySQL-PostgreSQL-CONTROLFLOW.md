# Conversion Issues with CONTROL FLOW<a name="sct-reference-MySQL-PostgreSQL-CONTROLFLOW"></a>

## Issue 8845: Rows count functionality is not supported behind the "open cursor" statement<a name="sct-reference-8845"></a>

In PostgreSQL, the FOUND\_ROWS\(\) function can't be called within a cursor\. Perform a manual conversion instead\.

## Issue 8826: Check the default value for a Date or DateTime variable<a name="sct-reference-8826"></a>

When converting default values for Date, Time, or DateTime variables, they are explicitly cast to the data type of the target variable\. For example, the following MySQL code:

```
DECLARE ValueDate1 DATE DEFAULT '2000-01-01';
```

Is converted to the following PostgreSQL code:

```
ValueDate1 DATE DEFAULT '2000-01-01'::DATE;
```

If the default value is of the form '0000\-00\-00' or similar \('0000\-00\-00', '0000\-00\-00 00:00:00', '0000\-00\-00 00:00:00\.000000'\), it is converted to the literal 'epoch'\. For example, the following MySQL code:

```
DECLARE ValueDate2 DATE DEFAULT '0000-00-00';
```

Is converted to the following PostgreSQL code:

```
ValueDate2 DATE DEFAULT 'epoch'::DATE; 
```

In these cases, the default value must be manually updated\. Review the generated code and modify it if necessary\.

## Issue 8828: User\-defined variables are not supported in PostgreSQL<a name="sct-reference-8828"></a>

Perform a manual conversion\.

## Issue 8844: Error codes are not the same<a name="sct-reference-8844"></a>

Some exit handler conditions require manual conversion\. MySQL code with any of the following exit handler statements must be converted to use PostgreSQL error handling with OTHERS or SQLSTATE conditions instead:

```
DECLARE EXIT HANDLER FOR SQLWARNING, SQLEXCEPTION, NOT FOUND
DECLARE EXIT HANDLER FOR SQLWARNING
DECLARE EXIT HANDLER FOR SQLEXCEPTION
DECLARE EXIT HANDLER FOR NOT FOUND
DECLARE EXIT HANDLER FOR SQLWARNING, NOT FOUND
DECLARE EXIT HANDLER FOR <mysql_error_code>
DECLARE EXIT HANDLER FOR SQLSTATE <sqlstate_value>
```

Review the transformed code, and correct it if necessary\.

## Issue 8846: PostgreSQL doesn't support the statement option %s<a name="sct-reference-8846"></a>

Some of the condition information items that are used with the DECLARE CONDITION and GET DIAGNOSTICS CONDITION statements in MySQL are not supported by PostgreSQL\. These include:

+ CLASS\_ORIGIN

+ SUBCLASS\_ORIGIN

+ MYSQL\_ERRNO

+ CONSTRAINT\_CATALOG

+ CONSTRAINT\_SCHEMA

+ CATALOG\_NAME

+ CURSOR\_NAME

Manually convert the code wherever you use these condition information items\.

## Issue 8847: PostgreSQL isn't able to return to a call point after error handling<a name="sct-reference-8847"></a>

If an error occurs in a BEGIN\.\.\.END block, PostgreSQL exits the block without executing any further statements in that block\. Check your error handling logic and perform a manual conversion instead\.

## Issue 8827: Statement Label Syntax for BEGIN\.\.\.END blocks is not supported in PostgreSQL<a name="sct-reference-8827"></a>

Perform a manual conversion\.

## Issue 8856: The information of the server processes is different on different servers<a name="sct-reference-8856"></a>

Check your conversion result\.

## Issue 8857: Automatic conversion for replication commands is not supported<a name="sct-reference-8857"></a>

Perform a manual conversion for all replication\-related code\.

## Issue 8853: Perform a manual conversion if using SLEEP\(\) with other expressions<a name="sct-reference-8853"></a>

If you are using SLEEP\(\) in a SELECT statement along with other expressions, for example `SELECT NOW(), SLEEP(2), AccountNo FROM Account`, you must manually convert that code\.

## Related Topics<a name="sct-reference-MySQL-PostgreSQL-CONTROLFLOW-related"></a>

+  [MySQL to PostgreSQL Conversion Reference](sct-reference-MySQL-PostgreSQL.md) 

+  [AWS Schema Conversion Tool Reference](CHAP_SchemaConversionTool.Reference.md) 

+  [What Is the AWS Schema Conversion Tool?](Welcome.md) 