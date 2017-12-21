# Conversion Issues with Messages from Stored Routines<a name="sct-reference-PostgreSQL-MySQL-Messagefromstoredroutines"></a>

## Issue 6332: MySQL doesn't support the RAISE statement to report messages<a name="sct-reference-6332"></a>

Try using INSERT to write a message to a log table instead\. To do this, you must add code in one of the following tables in the AWS\_POSTGRESQL\_EXT schema \(the temporary work schema used for PostgreSQL\):

+ RAISE\_DEBUG

+ RAISE\_LOG

+ RAISE\_INFO

+ RAISE\_NOTICE

+ RAISE\_WARNING

## Related Topics<a name="w3ab1c37c17c11d141b5"></a>

+  [PostgreSQL to MySQL Conversion Reference](sct-reference-PostgreSQL-MySQL-overview.md) 

+  [AWS Schema Conversion Tool Reference](CHAP_SchemaConversionTool.Reference.md) 

+  [What Is the AWS Schema Conversion Tool?](Welcome.md) 