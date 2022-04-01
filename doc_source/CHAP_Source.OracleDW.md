# Using Oracle Data Warehouse as a source for AWS SCT<a name="CHAP_Source.OracleDW"></a>

You can use AWS SCT to convert schemas, code objects, and application code from Oracle Data Warehouse to Amazon Redshift or Amazon Redshift and AWS Glue used in combination\. 

## Privileges for Oracle Data Warehouse as a source<a name="CHAP_Source.OracleDW.Permissions"></a>

The privileges required for Oracle Data Warehouse as a source are listed following: 
+ connect 
+ select\_catalog\_role 
+ select any dictionary 

## Connecting to Oracle Data Warehouse as a source<a name="CHAP_Source.OracleDW.Connecting"></a>

Use the following procedure to connect to your Oracle data warehouse source database with the AWS Schema Conversion Tool\. 

**To connect to an Oracle Data Warehouse source database**

1. In the AWS Schema Conversion Tool, choose **Add source**\. 

1. Choose **Oracle**, then choose **Next**\. 

   The **Add source** dialog box appears\.

1. For **Connection name**, enter a name for your database\. AWS SCT displays this name in the tree in the left panel\. 

1. Use database credentials from AWS Secrets Manager or enter them manually:
   + To use database credentials from Secrets Manager, use the following instructions:

     1. For **AWS Secret**, choose the name of the secret\.

     1. Choose **Populate** to automatically fill in all values in the database connection dialog box from Secrets Manager\.

     For information about using database credentials from Secrets Manager, see [Using AWS Secrets Manager](CHAP_UserInterface.md#CHAP_UserInterface.SecretsManager)\.
   + To enter the Oracle source data warehouse connection information manually, use the instructions in the following table\.  
****    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/CHAP_Source.OracleDW.html)

1. Choose **Test Connection** to verify that AWS SCT can connect to your source database\. 

1. Choose **Connect** to connect to your source database\.