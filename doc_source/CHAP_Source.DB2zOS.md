# Using IBM Db2 for z/OS as a source for AWS SCT<a name="CHAP_Source.DB2zOS"></a>

You can use AWS SCT to convert schemas, code objects, and application code from IBM Db2 for z/OS to the following targets\.
+ Amazon RDS for MySQL
+ Amazon Aurora MySQL\-Compatible Edition
+ Amazon RDS for PostgreSQL
+ Amazon Aurora PostgreSQL\-Compatible Edition

## Privileges for Db2 for z/OS as a source<a name="CHAP_Source.DB2zOS.Permissions"></a>

The privileges needed to connect to a Db2 for z/OS database and read system catalogs and tables are listed following:
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
   + To enter the IBM Db2 for z/OS source database connection information manually, use the instructions in the following table\.  
****    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/CHAP_Source.DB2zOS.html)

1. Choose **Test Connection** to verify that AWS SCT can connect to your source database\.

1. Choose **Connect** to connect to your source database\.

## Privileges for MySQL as a target<a name="CHAP_Source.DB2zOS.ConfigureMySQL"></a>

The privileges required for MySQL as a target are listed following:
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

In the example preceding, replace *user\_name* with the name of your user\. Then, replace *your\_password* with a secure password\.

To use Amazon RDS for MySQL as a target, set the `log_bin_trust_function_creators` parameter to true, and the `character_set_server` to `latin1`\. To configure these parameters, create a new DB parameter group or modify an existing DB parameter group\.

To use Aurora MySQL as a target, set the `log_bin_trust_function_creators` parameter to true, and the `character_set_server` to `latin1`\. Also, set the `lower_case_table_names` parameter to true\. To configure these parameters, create a new DB parameter group or modify an existing DB parameter group\.

## Privileges for PostgreSQL as a target<a name="CHAP_Source.DB2zOS.ConfigurePostgreSQL"></a>

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

In the example preceding, replace *user\_name* with the name of your user\. Then, replace *db\_name* with the name of your target Amazon Redshift database\. Finally, replace *your\_password* with a secure password\.

In PostgreSQL, only the schema owner or a `superuser` can drop a schema\. The owner can drop a schema and all objects that this schema includes even if the owner of the schema doesn't own some of its objects\.

When you use different users to convert and apply different schemas to your target database, you can get an error message when AWS SCT can't drop a schema\. To avoid this error message, use the `superuser` role\. 