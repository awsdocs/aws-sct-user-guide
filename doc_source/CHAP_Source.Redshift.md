# Using Amazon Redshift as a source for AWS SCT<a name="CHAP_Source.Redshift"></a>

You can use AWS SCT to convert schemas, code objects, and application code from Amazon Redshift to the following targets: 
+ Amazon Redshift

## Privileges for Amazon Redshift as a source database<a name="CHAP_Source.Redshift.Permissions"></a>

The privileges required for using Amazon Redshift as a source are listed following: 
+ USAGE ON SCHEMA *<schema\_name>* 
+ SELECT ON ALL TABLES IN SCHEMA *<schema\_name>* 
+ SELECT ON PG\_CATALOG\.PG\_STATISTIC 
+ SELECT ON SVV\_TABLE\_INFO 
+ SELECT ON TABLE STV\_BLOCKLIST 
+ SELECT ON TABLE STV\_TBL\_PERM 
+ SELECT ON SYS\_SERVERLESS\_USAGE 
+ SELECT ON PG\_DATABASE\_INFO 
+ SELECT ON PG\_STATISTIC 

In the example preceding, replace the *<schema\_name>* placeholder with the name of the source schema\.

## Connecting to Amazon Redshift as a source<a name="CHAP_Source.Redshift.Connecting"></a>

Use the following procedure to connect to your Amazon Redshift source database with the AWS Schema Conversion Tool\. 

**To connect to an Amazon Redshift source database**

1. In the AWS Schema Conversion Tool, choose **Add source**\. 

1. Choose **Amazon Redshift**, then choose **Next**\. 

   The **Add source** dialog box appears\.

1. For **Connection name**, enter a name for your database\. AWS SCT displays this name in the tree in the left panel\. 

1. Use database credentials from AWS Secrets Manager or enter them manually:
   + To use database credentials from Secrets Manager, use the following instructions:

     1. For **AWS Secret**, choose the name of the secret\.

     1. Choose **Populate** to automatically fill in all values in the database connection dialog box from Secrets Manager\.

     For information about using database credentials from Secrets Manager, see [Using AWS Secrets Manager](CHAP_UserInterface.md#CHAP_UserInterface.SecretsManager)\.
   + To enter the Amazon Redshift source database connection information manually, use the instructions in the following table\.  
****    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/CHAP_Source.Redshift.html)

1. Choose **Test Connection** to verify that AWS SCT can connect to your source database\. 

1. Choose **Connect** to connect to your source database\.