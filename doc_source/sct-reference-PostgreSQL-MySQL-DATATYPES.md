# Conversion Issues with DATA TYPES<a name="sct-reference-PostgreSQL-MySQL-DATATYPES"></a>

## Issue 6673: MySQL doesn't support %s type in the CAST function, and a loss of precision or accuracy of data is possible<a name="sct-reference-6673"></a>

Statements that cast values to any of the following data types are converted to statements that cast values to CHAR:

+ BYTEA

+ CIDR

+ JSON

+ int4range

 For example, take the following PostgreSQL statements\.

```
select '1'::BYTEA
select CAST('1' AS BYTEA)
```

These are both converted to the following MySQL statement\.

```
select CAST('1' AS CHAR)
```

Review the converted code and revise it if necessary\.

## Issue 6674: MySQL doesn't support %s type in the CAST function<a name="sct-reference-6674"></a>

Statements that cast a value to the TXID\_SNAPSHOT data type are converted to statements that cast a value to CHAR\. For example, take the following PostgreSQL statements\.

```
select '2628:2628:'::TXID_SNAPSHOT
select CAST('2628:2628:' AS TXID_SNAPSHOT)
```

These are both converted to the following MySQL statement:

```
select CAST('2628:2628:' AS CHAR)
```

Review the converted code and revise it if necessary\.

## Related Topics<a name="w3ab1c37c17c11d111b7"></a>

+  [PostgreSQL to MySQL Conversion Reference](sct-reference-PostgreSQL-MySQL-overview.md) 

+  [AWS Schema Conversion Tool Reference](CHAP_SchemaConversionTool.Reference.md) 

+  [What Is the AWS Schema Conversion Tool?](Welcome.md) 