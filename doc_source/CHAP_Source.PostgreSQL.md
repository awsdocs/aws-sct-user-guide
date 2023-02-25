# Using PostgreSQL as a source for AWS SCT<a name="CHAP_Source.PostgreSQL"></a>

You can use AWS SCT to convert schemas, database code objects, and application code from PostgreSQL to the following targets: 
+ Amazon RDS for MySQL
+ Amazon Aurora MySQL\-Compatible Edition
+ Amazon RDS for PostgreSQL
+ Amazon Aurora PostgreSQL\-Compatible Edition

For more information, see the following sections:

**Topics**
+ [Privileges for PostgreSQL as a source database](#CHAP_Source.PostgreSQL.Permissions)
+ [Connecting to PostgreSQL as a source](#CHAP_Source.PostgreSQL.Connecting)
+ [Privileges for MySQL as a target database](#CHAP_Source.PostgreSQL.ConfigureMySQL)

## Privileges for PostgreSQL as a source database<a name="CHAP_Source.PostgreSQL.Permissions"></a>

The privileges required for PostgreSQL as a source are listed following: 
+ CONNECT ON DATABASE *<database\_name>* 
+ USAGE ON SCHEMA *<database\_name>* 
+ SELECT ON ALL TABLES IN SCHEMA *<database\_name>* 
+ SELECT ON ALL SEQUENCES IN SCHEMA *<database\_name>* 

## Connecting to PostgreSQL as a source<a name="CHAP_Source.PostgreSQL.Connecting"></a>

Use the following procedure to connect to your PostgreSQL source database with the AWS Schema Conversion Tool\. 

**To connect to a PostgreSQL source database**

1. In the AWS Schema Conversion Tool, choose **Add source**\. 

1. Choose **PostgreSQL**, then choose **Next**\.

   The **Add source** dialog box appears\.

1. For **Connection name**, enter a name for your database\. AWS SCT displays this name in the tree in the left panel\. 

1. Use database credentials from AWS Secrets Manager or enter them manually:
   + To use database credentials from Secrets Manager, use the following instructions:

     1. For **AWS Secret**, choose the name of the secret\.

     1. Choose **Populate** to automatically fill in all values in the database connection dialog box from Secrets Manager\.

     For information about using database credentials from Secrets Manager, see [Using AWS Secrets Manager](CHAP_UserInterface.md#CHAP_UserInterface.SecretsManager)\.
   + To enter the PostgreSQL source database connection information manually, use the following instructions:  
****    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/CHAP_Source.PostgreSQL.html)

1. Choose **Test Connection** to verify that AWS SCT can connect to your source database\. 

1. Choose **Connect** to connect to your source database\.

## Privileges for MySQL as a target database<a name="CHAP_Source.PostgreSQL.ConfigureMySQL"></a>

The privileges required for MySQL as a target when you migrate from PostgreSQL are listed following:
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
+ INSERT, UPDATE ON AWS\_POSTGRESQL\_EXT\.\*
+ INSERT, UPDATE, DELETE ON AWS\_POSTGRESQL\_EXT\_DATA\.\*
+ CREATE TEMPORARY TABLES ON AWS\_POSTGRESQL\_EXT\_DATA\.\*

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
GRANT INSERT, UPDATE ON AWS_POSTGRESQL_EXT.* TO 'user_name';
GRANT INSERT, UPDATE, DELETE ON AWS_POSTGRESQL_EXT_DATA.* TO 'user_name';
GRANT CREATE TEMPORARY TABLES ON AWS_POSTGRESQL_EXT_DATA.* TO 'user_name';
```

In the preceding example, replace *user\_name* with the name of your user\. Then, replace *your\_password* with a secure password\.

To use Amazon RDS for MySQL as a target, set the `log_bin_trust_function_creators` parameter to true, and the `character_set_server` to `latin1`\. To configure these parameters, create a new DB parameter group or modify an existing DB parameter group\.

To use Aurora MySQL as a target, set the `log_bin_trust_function_creators` parameter to true, and the `character_set_server` to `latin1`\. Also, set the `lower_case_table_names` parameter to true\. To configure these parameters, create a new DB parameter group or modify an existing DB parameter group\.