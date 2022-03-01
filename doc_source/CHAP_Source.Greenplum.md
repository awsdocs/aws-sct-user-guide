# Using Greenplum Database as a source for AWS SCT<a name="CHAP_Source.Greenplum"></a>

You can use AWS SCT to convert schemas, code objects, and application code from Greenplum Database to Amazon Redshift\. 

## Privileges for Greenplum Database as a source<a name="CHAP_Source.Greenplum.Permissions"></a>

The privileges required for Greenplum Database as a source are listed following: 
+ CONNECT ON DATABASE *<database\_name>* 
+ USAGE ON SCHEMA *<schema\_name>* 
+ SELECT ON *<schema\_name>\.<table\_name>* 
+ SELECT ON SEQUENCE *<schema\_name>\.<sequence\_name>* 

In the example preceding, replace placeholders as following:
+ Replace `database_name` with the name of the source database\.
+ Replace `schema_name` with the name of the source schema\.
+ Replace *`table_name`* with the name of the source table\.
+ Replace `sequence_name` with the name of the sequence name\.

## Connecting to Greenplum Database as a source<a name="CHAP_Source.Greenplum.Connecting"></a>

Use the following procedure to connect to your Greenplum source database with the AWS SCT\.

**To connect to a Greenplum source database**

1. In the AWS Schema Conversion Tool, choose **Add source**\. 

1. Choose **SAP ASE**, then choose **Next**\. 

   The **Add source** dialog box appears\.

1. For **Connection name**, enter a name for your database\. AWS SCT displays this name in the tree in the left panel\. 

1. Use database credentials from AWS Secrets Manager or enter them manually:
   + To use database credentials from Secrets Manager, use the following insructions:

     1. For **AWS Secret**, choose the name of the secret\.

     1. Choose **Populate** to automatically fill in all values in the database connection dialog box from Secrets Manager\.

     For information about using database credentials from Secrets Manager, see [Using AWS Secrets Manager](CHAP_UserInterface.md#CHAP_UserInterface.SecretsManager)\.
   + To enter the Greenplum source database connection information manually, use the instructions in the following table\.  
****    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/CHAP_Source.Greenplum.html)

1. Choose **Test Connection** to verify that AWS SCT can connect to your source database\. 

1. Choose **Connect** to connect to your source database\.