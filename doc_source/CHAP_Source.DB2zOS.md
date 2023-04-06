# Using IBM Db2 for z/OS as a source for AWS SCT<a name="CHAP_Source.DB2zOS"></a>

You can use AWS SCT to convert schemas, code objects, and application code from IBM Db2 for z/OS to the following targets\.
+ Amazon RDS for MySQL
+ Amazon Aurora MySQL\-Compatible Edition
+ Amazon RDS for PostgreSQL
+ Amazon Aurora PostgreSQL\-Compatible Edition

## Privileges for Db2 for z/OS as a source database<a name="CHAP_Source.DB2zOS.Permissions"></a>

The privileges needed to connect to a Db2 for z/OS database and read system catalogs and tables are as follows:
+ SELECT ON SYSIBM\.LOCATIONS
+ SELECT ON SYSIBM\.SYSCHECKS
+ SELECT ON SYSIBM\.SYSCOLUMNS
+ SELECT ON SYSIBM\.SYSDATABASE
+ SELECT ON SYSIBM\.SYSDATATYPES
+ SELECT ON SYSIBM\.SYSDUMMY1
+ SELECT ON SYSIBM\.SYSFOREIGNKEYS
+ SELECT ON SYSIBM\.SYSINDEXES
+ SELECT ON SYSIBM\.SYSKEYCOLUSE
+ SELECT ON SYSIBM\.SYSKEYS
+ SELECT ON SYSIBM\.SYSKEYTARGETS
+ SELECT ON SYSIBM\.SYSJAROBJECTS
+ SELECT ON SYSIBM\.SYSPACKAGE
+ SELECT ON SYSIBM\.SYSPARMS
+ SELECT ON SYSIBM\.SYSRELS
+ SELECT ON SYSIBM\.SYSROUTINES
+ SELECT ON SYSIBM\.SYSSEQUENCES
+ SELECT ON SYSIBM\.SYSSEQUENCESDEP
+ SELECT ON SYSIBM\.SYSSYNONYMS
+ SELECT ON SYSIBM\.SYSTABCONST
+ SELECT ON SYSIBM\.SYSTABLES
+ SELECT ON SYSIBM\.SYSTABLESPACE
+ SELECT ON SYSIBM\.SYSTRIGGERS
+ SELECT ON SYSIBM\.SYSVARIABLES
+ SELECT ON SYSIBM\.SYSVIEWS

To convert Db2 for z/OS tables to PostgreSQL partitioned tables, gather statistics on tablespaces and tables in your database using the `RUNSTATS` utility as shown following\.

```
LISTDEF YOURLIST INCLUDE TABLESPACES DATABASE YOURDB 
RUNSTATS TABLESPACE
LIST YOURLIST
TABLE (ALL) INDEX (ALL KEYCARD)
UPDATE ALL
REPORT YES
SHRLEVEL REFERENCE
```

In the preceding example, replace the `YOURDB` placeholder with the name of the source database\.

## Connecting to Db2 for z/OS as a source<a name="CHAP_Source.DB2zOS.Connecting"></a>

Use the following procedure to connect to your Db2 for z/OS source database with AWS SCT\.

**To connect to an IBM Db2 for z/OS source database**

1. In the AWS Schema Conversion Tool, choose **Add source**\.

1. Choose **Db2 for z/OS**, then choose **Next**\.

   The **Add source** dialog box appears\.

1. For **Connection name**, enter a name for your database\. AWS SCT displays this name in the tree in the left panel\. 

1. Use database credentials from AWS Secrets Manager or enter them manually:
   + To use database credentials from Secrets Manager, use the following instructions:

     1. For **AWS Secret**, choose the name of the secret\.

     1. Choose **Populate** to automatically fill in all values in the database connection dialog box from Secrets Manager\.

     For information about using database credentials from Secrets Manager, see [Using AWS Secrets Manager](CHAP_UserInterface.md#CHAP_UserInterface.SecretsManager)\.
   + To enter the IBM Db2 for z/OS source database connection information manually, use the following instructions:  
****    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/CHAP_Source.DB2zOS.html)

1. Choose **Test Connection** to verify that AWS SCT can connect to your source database\.

1. Choose **Connect** to connect to your source database\.

## Privileges for MySQL as a target database<a name="CHAP_Source.DB2zOS.ConfigureMySQL"></a>

The privileges required for MySQL as a target are as follows:
+ CREATE ON \*\.\*
+ ALTER ON \*\.\*
+ DROP ON \*\.\*
+ INDEX ON \*\.\*
+ REFERENCES ON \*\.\*
+ SELECT ON \*\.\*
+ CREATE VIEW ON \*\.\*
+ SHOW VIEW ON \*\.\*
+ TRIGGER ON \*\.\*
+ CREATE ROUTINE ON \*\.\*
+ ALTER ROUTINE ON \*\.\*
+ EXECUTE ON \*\.\*
+ SELECT ON mysql\.proc
+ INSERT, UPDATE ON AWS\_DB2ZOS\_EXT\.\*
+ INSERT, UPDATE, DELETE ON AWS\_DB2ZOS\_EXT\_DATA\.\*
+ CREATE TEMPORARY TABLES ON AWS\_DB2ZOS\_EXT\_DATA\.\*

You can use the following code example to create a database user and grant the privileges\.

```
CREATE USER 'user_name' IDENTIFIED BY 'your_password';
GRANT CREATE ON *.* TO 'user_name';
GRANT ALTER ON *.* TO 'user_name';
GRANT DROP ON *.* TO 'user_name';
GRANT INDEX ON *.* TO 'user_name';
GRANT REFERENCES ON *.* TO 'user_name';
GRANT SELECT ON *.* TO 'user_name';
GRANT CREATE VIEW ON *.* TO 'user_name';
GRANT SHOW VIEW ON *.* TO 'user_name';
GRANT TRIGGER ON *.* TO 'user_name';
GRANT CREATE ROUTINE ON *.* TO 'user_name';
GRANT ALTER ROUTINE ON *.* TO 'user_name';
GRANT EXECUTE ON *.* TO 'user_name';
GRANT SELECT ON mysql.proc TO 'user_name';
GRANT INSERT, UPDATE ON AWS_DB2ZOS_EXT.* TO 'user_name';
GRANT INSERT, UPDATE, DELETE ON AWS_DB2ZOS_EXT_DATA.* TO 'user_name';
GRANT CREATE TEMPORARY TABLES ON AWS_DB2ZOS_EXT_DATA.* TO 'user_name';
```

In the preceding example, replace *user\_name* with the name of your user\. Then, replace *your\_password* with a secure password\.

To use Amazon RDS for MySQL as a target, set the `log_bin_trust_function_creators` parameter to true, and the `character_set_server` to `latin1`\. To configure these parameters, create a new DB parameter group or modify an existing DB parameter group\.

To use Aurora MySQL as a target, set the `log_bin_trust_function_creators` parameter to true, and the `character_set_server` to `latin1`\. Also, set the `lower_case_table_names` parameter to true\. To configure these parameters, create a new DB parameter group or modify an existing DB parameter group\.

## Privileges for PostgreSQL as a target database<a name="CHAP_Source.DB2zOS.ConfigurePostgreSQL"></a>

To use PostgreSQL as a target, AWS SCT requires the `CREATE ON DATABASE` privilege\. Make sure that you grant this privilege for each target PostgreSQL database\.

To use Amazon RDS for PostgreSQL as a target, AWS SCT requires the `rds_superuser` privilege\.

To use the converted public synonyms, change the database default search path to `"$user", public_synonyms, public`\.

You can use the following code example to create a database user and grant the privileges\.

```
CREATE ROLE user_name LOGIN PASSWORD 'your_password';
GRANT CREATE ON DATABASE db_name TO user_name;
GRANT rds_superuser TO user_name;
ALTER DATABASE db_name SET SEARCH_PATH = "$user", public_synonyms, public;
```

In the preceding example, replace *user\_name* with the name of your user\. Then, replace *db\_name* with the name of your target database\. Finally, replace *your\_password* with a secure password\.

In PostgreSQL, only the schema owner or a `superuser` can drop a schema\. The owner can drop a schema and all objects that this schema includes even if the owner of the schema doesn't own some of its objects\.

When you use different users to convert and apply different schemas to your target database, you can get an error message when AWS SCT can't drop a schema\. To avoid this error message, use the `superuser` role\. 

## Db2 for z/OS to PostgreSQL conversion settings<a name="CHAP_Source.DB2zOS.PostgreSQLConversionSettings"></a>

To edit Db2 for z/OS to PostgreSQL conversion settings, choose **Settings**, and then choose **Conversion settings**\. From the upper list, choose **Db2 for z/OS**, and then choose **Db2 for z/OS – PostgreSQL** or **Db2 for z/OS – Amazon Aurora \(PostgreSQL compatible\)**\. AWS SCT displays all available settings for IBM Db2 for z/OS to PostgreSQL conversion\.

Db2 for z/OS to PostgreSQL conversion settings in AWS SCT include options for the following:
+ To limit the number of comments with action items in the converted code\.

  For **Add comments in the converted code for the action items of selected severity and higher**, choose the severity of action items\. AWS SCT adds comments in the converted code for action items of the selected severity and higher\.

  For example, to minimize the number of comments in your converted code, choose **Errors only**\. To include comments for all action items in your converted code, choose **All messages**\.
+ To generate unique names for constraints in the target database\.

  In PostgreSQL, all constraint names that you use must be unique\. AWS SCT can generate unique names for constraints in the converted code by adding a prefix with the table name to the name of your constraint\. To make sure that AWS SCT generates unique names for your constraints, select **Generate unique names for constraints**\.
+ To keep the formatting of column names, expressions, and clauses in DML statements in the converted code\.

  AWS SCT can keep the layout of column names, expressions, and clauses in DML statements in the similar position and order as in the source code\. To do so, select **Yes** for **Keep the formatting of column names, expressions, and clauses in DML statements**\.
+ To exclude table partitions from the conversion scope\.

  AWS SCT can skip all partitions of a source table during the conversion\. To do so, select **Exclude table partitions from the conversion scope**\.
+ To use automatic partitioning for tables that are partitioned by growth\.

  For data migration, AWS SCT can automatically partition all tables that are larger than the specified size\. To use this option, select **Enforce partition of tables larger than**, and enter the tables size in gigabytes\. Next, enter the number of partitions\. AWS SCT considers the direct access storage device \(DASD\) size of your source database when you turn on this option\.

  AWS SCT can determine the number of partitions automatically\. To do so, select **Increase the number of partitions proportionally**, and enter the maximum number of partitions\.
+ To return dynamic result sets as an array of values of the refcursor data type\.

  AWS SCT can convert source procedures that return dynamic result sets into procedures which have an array of open refcursors as an additional output parameter\. To do so, select **Use an array of refcursors to return all dynamic result sets**\.
+ To specify the standard to use for the conversion of date and time values to string representations\.

  AWS SCT can convert date and time values to string representations using one of the supported industry formats\. To do so, select **Use string representations of date values** or **Use string representations of time values**\. Next, choose one of the following standards\.
  + International Standards Organization \(ISO\)
  + IBM European Standard \(EUR\)
  + IBM USA Standard \(USA\)
  + Japanese Industrial Standard Christian Era \(JIS\)