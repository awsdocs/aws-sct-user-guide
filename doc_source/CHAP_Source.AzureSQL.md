# Using Azure SQL Database as a source for AWS SCT<a name="CHAP_Source.AzureSQL"></a>

You can use AWS SCT to convert schemas, code objects, and application code from Azure SQL Database to the following targets: 
+ Amazon RDS for MySQL
+ Amazon Aurora MySQL\-Compatible Edition
+ Amazon RDS for PostgreSQL
+ Amazon Aurora PostgreSQL\-Compatible Edition

**Topics**
+ [Privileges for Azure SQL Database as a source](#CHAP_Source.AzureSQL.Permissions)
+ [Connecting to Azure SQL Database as a source](#CHAP_Source.AzureSQL.Connecting)

## Privileges for Azure SQL Database as a source<a name="CHAP_Source.AzureSQL.Permissions"></a>

The privileges required for Azure SQL Database as a source are listed following: 
+ VIEW DEFINITION 
+ VIEW DATABASE STATE 

Repeat the grant for each database whose schema you are converting\. 

## Connecting to Azure SQL Database as a source<a name="CHAP_Source.AzureSQL.Connecting"></a>

Use the following procedure to connect to your Azure SQL Database source database with the AWS Schema Conversion Tool\. 

**To connect to an Azure SQL Database source database**

1. In the AWS Schema Conversion Tool, choose **Add source**\. 

1. Choose **Azure SQL Database**, then choose **Next**\. 

   The **Add source** dialog box appears\.

1. For **Connection name**, enter a name for your database\. AWS SCT displays this name in the tree in the left panel\. 

1. Use database credentials from AWS Secrets Manager or enter them manually:
   + To use database credentials from Secrets Manager, use the following insructions:

     1. For **AWS Secret**, choose the name of the secret\.

     1. Choose **Populate** to automatically fill in all values in the database connection dialog box from Secrets Manager\.

     For information about using database credentials from Secrets Manager, see [Using AWS Secrets Manager](CHAP_UserInterface.md#CHAP_UserInterface.SecretsManager)\.
   + To enter the Azure SQL Database source database connection information manually, use the instructions in the following table\.  
****    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/CHAP_Source.AzureSQL.html)

1. Choose **Test Connection** to verify that AWS SCT can connect to your source database\. 

1. Choose **Connect** to connect to your source database\.