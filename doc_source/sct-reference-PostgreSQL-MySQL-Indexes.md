# Conversion Issues with Indexes<a name="sct-reference-PostgreSQL-MySQL-Indexes"></a>

## Issue 6091: MySQL doesn't support %s index method<a name="sct-reference-6091"></a>

The InnoDB engine in MySQL doesn't support HASH and ON *table\_name* indexes\. Perform a manual conversion in these cases\.

## Issue 6090: MySQL doesn't support indexes on expressions<a name="sct-reference-6090"></a>

Perform a manual conversion\.

## Issue 6092: MySQL doesn't support explicit sort ordering in the index definition<a name="sct-reference-6092"></a>

Indexes that use explicit sort ordering are converted to use the default \(ascending\) sort order instead\. If this conversion causes performance degradation, revise the converted code as necessary\.

## Issue 6093: MySQL doesn't support partial indexes<a name="sct-reference-6093"></a>

Partial indexes are converted to full indexes instead\. For example, take the following PostgreSQL statement\.

```
CREATE INDEX i_indexed_partial
  ON test_pg_mysql.indexed_partial USING btree
  ( n )
  WHERE ( n < 100 );
```

The preceding statement is converted to the following MySQL statement:

```
CREATE INDEX i_indexed_partial
  USING BTREE ON test_pg_mysql.indexed_partial
  ( n );
```

If this conversion causes performance degradation, revise the converted code as necessary\.

## Related Topics<a name="w3ab1c37c17c11d129c11"></a>

+  [PostgreSQL to MySQL Conversion Reference](sct-reference-PostgreSQL-MySQL-overview.md) 

+  [AWS Schema Conversion Tool Reference](CHAP_SchemaConversionTool.Reference.md) 

+  [What Is the AWS Schema Conversion Tool?](Welcome.md) 