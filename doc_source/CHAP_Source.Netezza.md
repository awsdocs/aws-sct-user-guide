# Using Netezza as a source for AWS SCT<a name="CHAP_Source.Netezza"></a>

You can use AWS SCT to convert schemas, code objects, and application code from Netezza to Amazon Redshift\. 

## Privileges for Netezza as a source<a name="CHAP_Source.Netezza.Permissions"></a>

The privileges required for Netezza as a source are listed following: 
+ select on system\.definition\_schema\.system view
+ select on system\.definition\_schema\.system table
+ select on system\.definition\_schema\.management table
+ list on *<database\_name>*
+ list on *<schema\_name>*
+ list on *<database\_name>*\.all\.table
+ list on *<database\_name>*\.all\.external table
+ list on *<database\_name>*\.all\.view
+ list on *<database\_name>*\.all\.materialized view
+ list on *<database\_name>*\.all\.procedure
+ list on *<database\_name>*\.all\.sequence
+ list on *<database\_name>*\.all\.function
+ list on *<database\_name>*\.all\.aggregate

In the example preceding, replace placeholders as following:
+ Replace *database\_name* with the name of the source database\.
+ Replace *schema\_name* with the name of the source schema\.

AWS SCT requires access to the following system tables and views\. You can grant access to these objects instead of granting access to `system.definition_schema.system view` and `system.definition_schema.system tables` in the preceding list\.
+ select on system\.definition\_schema\.\_t\_aggregate
+ select on system\.definition\_schema\.\_t\_class
+ select on system\.definition\_schema\.\_t\_constraint
+ select on system\.definition\_schema\.\_t\_const\_relattr
+ select on system\.definition\_schema\.\_t\_database
+ select on system\.definition\_schema\.\_t\_grpobj\_priv
+ select on system\.definition\_schema\.\_t\_grpusr
+ select on system\.definition\_schema\.\_t\_hist\_config
+ select on system\.definition\_schema\.\_t\_object
+ select on system\.definition\_schema\.\_t\_object\_classes
+ select on system\.definition\_schema\.\_t\_proc
+ select on system\.definition\_schema\.\_t\_type
+ select on system\.definition\_schema\.\_t\_user
+ select on system\.definition\_schema\.\_t\_usrobj\_priv
+ select on system\.definition\_schema\.\_vt\_sequence
+ select on system\.definition\_schema\.\_v\_aggregate
+ select on system\.definition\_schema\.\_v\_constraint\_depends
+ select on system\.definition\_schema\.\_v\_database
+ select on system\.definition\_schema\.\_v\_datatype
+ select on system\.definition\_schema\.\_v\_dslice
+ select on system\.definition\_schema\.\_v\_function
+ select on system\.definition\_schema\.\_v\_group
+ select on system\.definition\_schema\.\_v\_obj\_relation
+ select on system\.definition\_schema\.\_v\_obj\_relation\_xdb
+ select on system\.definition\_schema\.\_v\_procedure
+ select on system\.definition\_schema\.\_v\_relation\_column
+ select on system\.definition\_schema\.\_v\_relation\_keydata
+ select on system\.definition\_schema\.\_v\_relobjclasses
+ select on system\.definition\_schema\.\_v\_schema\_xdb
+ select on system\.definition\_schema\.\_v\_sequence
+ select on system\.definition\_schema\.\_v\_synonym
+ select on system\.definition\_schema\.\_v\_system\_info
+ select on system\.definition\_schema\.\_v\_sys\_constraint
+ select on system\.definition\_schema\.\_v\_sys\_object\_dslice\_info
+ select on system\.definition\_schema\.\_v\_sys\_user
+ select on system\.definition\_schema\.\_v\_table
+ select on system\.definition\_schema\.\_v\_table\_constraint
+ select on system\.definition\_schema\.\_v\_table\_dist\_map
+ select on system\.definition\_schema\.\_v\_table\_organize\_column
+ select on system\.definition\_schema\.\_v\_table\_storage\_stat
+ select on system\.definition\_schema\.\_v\_user
+ select on system\.definition\_schema\.\_v\_view
+ select on system\.information\_schema\.\_v\_relation\_column
+ select on system\.information\_schema\.\_v\_table
+ select on $hist\_column\_access\_\*

## Connecting to Netezza as a source<a name="CHAP_Source.Netezza.Connecting"></a>

Use the following procedure to connect to your Netezza source database with the AWS Schema Conversion Tool\. 

**To connect to a Netezza source database**

1. In the AWS Schema Conversion Tool, choose **Add source**\. 

1. Choose **Netezza**, then choose **Next**\. 

   The **Add source** dialog box appears\.

1. For **Connection name**, enter a name for your database\. AWS SCT displays this name in the tree in the left panel\. 

1. Use database credentials from AWS Secrets Manager or enter them manually:
   + To use database credentials from Secrets Manager, use the following instructions:

     1. For **AWS Secret**, choose the name of the secret\.

     1. Choose **Populate** to automatically fill in all values in the database connection dialog box from Secrets Manager\.

     For information about using database credentials from Secrets Manager, see [Using AWS Secrets Manager](CHAP_UserInterface.md#CHAP_UserInterface.SecretsManager)\.
   + To enter the Netezza source database connection information manually, use the instructions in the following table\.  
****    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/CHAP_Source.Netezza.html)

1. Choose **Test Connection** to verify that AWS SCT can connect to your source database\. 

1. Choose **Connect** to connect to your source database\.