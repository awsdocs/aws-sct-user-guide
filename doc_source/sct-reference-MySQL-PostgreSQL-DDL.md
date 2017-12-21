# Conversion Issues with DDL<a name="sct-reference-MySQL-PostgreSQL-DDL"></a>

## Issue 8825: Check the default value for a Date or DateTime column<a name="sct-reference-8825"></a>

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

## Issue 8801: The table can be locked open cursor<a name="sct-reference-8801"></a>

The conversion uses the DROP TABLE IF EXISTS statement to remove a temporary table before the end of the function in which it was created\. In some cases though, this statement might fail because the temporary table is locked due to an open cursor\. In this case, the DROP TABLE statement must be commented out\. Review your transformed code and modify it if necessary\.

## Related Topics<a name="sct-reference-MySQL-PostgreSQL-DDL-related"></a>

+  [MySQL to PostgreSQL Conversion Reference](sct-reference-MySQL-PostgreSQL.md) 

+  [AWS Schema Conversion Tool Reference](CHAP_SchemaConversionTool.Reference.md) 

+  [What Is the AWS Schema Conversion Tool?](Welcome.md) 