# Using Microsoft SQL Server Data Warehouse as a source for AWS SCT<a name="CHAP_Source.SQLServerDW"></a>

You can use AWS SCT to convert schemas, code objects, and application code from Microsoft SQL Server DW to Amazon Redshift or Amazon Redshift and AWS Glue used in combination\. 

## Privileges for Microsoft SQL Server Data Warehouse as a source<a name="CHAP_Source.SQLServerDW.Permissions"></a>

The privileges required for Microsoft SQL Server data warehouse as a source are listed following: 
+ VIEW DEFINITION 
+ VIEW DATABASE STATE 
+ SELECT ON SCHEMA :: *<schema\_name>* 

In the example preceding, replace the *<source\_schema>* placeholder with the name of the source source\_schema\.

Repeat the grant for each database whose schema you are converting\. 

In addition, grant the following, and run the grant on the master database: 
+ VIEW SERVER STATE 

## Limitations for SQL Server Data Warehouse as a source<a name="CHAP_Source.SQLServerDW.Limitations"></a>

Using Microsoft SQL Server Parallel Data Warehouse \(PDW\) as a source isn't currently supported\.

## Connecting to SQL Server Data Warehouse as a source<a name="CHAP_Source.SQLServerDW.Connecting"></a>

Use the following procedure to connect to your SQL Server Data Warehouse source database with the AWS Schema Conversion Tool\. 

**To connect to a SQL Server Data Warehouse source database**

1. In the AWS Schema Conversion Tool, choose **Add source**\.

1. Choose **Microsoft SQL Server**, then choose **Next**\. 

   The **Add source** dialog box appears\.

1. For **Connection name**, enter a name for your database\. AWS SCT displays this name in the tree in the left panel\. 

1. Use database credentials from AWS Secrets Manager or enter them manually:
   + To use database credentials from Secrets Manager, use the following instructions:

     1. For **AWS Secret**, choose the name of the secret\.

     1. Choose **Populate** to automatically fill in all values in the database connection dialog box from Secrets Manager\.

     For information about using database credentials from Secrets Manager, see [Using AWS Secrets Manager](CHAP_UserInterface.md#CHAP_UserInterface.SecretsManager)\.
   + To enter the Microsoft SQL Server source data warehouse connection information manually, use the instructions in the following table\.  
****    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/CHAP_Source.SQLServerDW.html)

1. Choose **Test Connection** to verify that AWS SCT can connect to your source database\. 

1. Choose **Connect** to connect to your source database\.