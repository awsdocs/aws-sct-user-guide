# Using Oracle Database as a source for AWS SCT<a name="CHAP_Source.Oracle"></a>

You can use AWS SCT to convert schemas, database code objects, and application code from Oracle Database to the following targets: 
+ Amazon RDS for MySQL
+ Amazon Aurora MySQL\-Compatible Edition
+ Amazon RDS for PostgreSQL
+ Amazon Aurora PostgreSQL\-Compatible Edition
+ Amazon RDS for Oracle
+ Amazon RDS for MariaDB

When the source is an Oracle database, comments can be converted to the appropriate format in, for example, a PostgreSQL database\. AWS SCT can convert comments on tables, views, and columns\. Comments can include apostrophes; AWS SCT doubles the apostrophes when converting SQL statements, just as it does for string literals\.

For more information, see the following\.

**Topics**
+ [Privileges for Oracle as a source](#CHAP_Source.Oracle.Permissions)
+ [Connecting to Oracle as a source](#CHAP_Source.Oracle.Connecting)
+ [Converting Oracle to Amazon RDS for PostgreSQL or Amazon Aurora PostgreSQL](CHAP_Source.Oracle.ToPostgreSQL.md)
+ [Converting Oracle to Amazon RDS for MySQL or Amazon Aurora MySQL](CHAP_Source.Oracle.ToMySQL.md)
+ [Converting Oracle to Amazon RDS for Oracle](CHAP_Source.Oracle.ToRDSOracle.md)

## Privileges for Oracle as a source<a name="CHAP_Source.Oracle.Permissions"></a>

The privileges required for Oracle as a source are listed following: 
+ CONNECT 
+ SELECT\_CATALOG\_ROLE 
+ SELECT ANY DICTIONARY 
+ SELECT on SYS\.USER$

## Connecting to Oracle as a source<a name="CHAP_Source.Oracle.Connecting"></a>

Use the following procedure to connect to your Oracle source database with the AWS Schema Conversion Tool\. 

**To connect to an Oracle source database**

1. In the AWS Schema Conversion Tool, choose **Add source**\. 

1. Choose **Oracle**, then choose **Next**\. 

   The **Add source** dialog box appears\.

1. For **Connection name**, enter a name for your database\. AWS SCT displays this name in the tree in the left panel\. 

1. Use database credentials from AWS Secrets Manager or enter them manually:
   + To use database credentials from Secrets Manager, use the following instructions:

     1. For **AWS Secret**, choose the name of the secret\.

     1. Choose **Populate** to automatically fill in all values in the database connection dialog box from Secrets Manager\.

     For information about using database credentials from Secrets Manager, see [Using AWS Secrets Manager](CHAP_UserInterface.md#CHAP_UserInterface.SecretsManager)\.
   + To enter the Oracle source database connection information manually, use the instructions in the following table\.    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/CHAP_Source.Oracle.html)

1. Choose **Test Connection** to verify that AWS SCT can connect to your source database\. 

1. Choose **Connect** to connect to your source database\.