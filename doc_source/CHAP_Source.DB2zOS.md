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