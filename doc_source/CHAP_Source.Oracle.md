# Using Oracle as a Source for AWS Schema Conversion Tool \(AWS SCT\)<a name="CHAP_Source.Oracle"></a>

You can use AWS SCT to convert data from Oracle to the following targets: 
+ Amazon RDS for MySQL
+  Amazon Aurora \(MySQL\)
+ Amazon RDS for PostgreSQL
+ Amazon Aurora \(PostgreSQL\)
+ Amazon RDS for Oracle

When the source is an Oracle database, comments can be converted to the appropriate format in, for example, a PostgreSQL database\. AWS SCT can convert comments on tables, views, and columns\. Comments can include apostrophes; AWS SCT doubles the apostrophes when converting SQL statements, just as it does for string literals\.

For more information, see the following sections:

**Topics**
+ [Permissions Required When Using Oracle as a Source Database](#CHAP_Source.Oracle.Permissions)
+ [Connecting to Oracle as a Source Database](#CHAP_Source.Oracle.Connecting)
+ [Converting Oracle to Amazon RDS for PostgreSQL or Amazon Aurora \(PostgreSQL\)](CHAP_Source.Oracle.ToPostgreSQL.md)
+ [Converting Oracle to Amazon RDS for MySQL or Amazon Aurora \(MySQL\)](CHAP_Source.Oracle.ToMySQL.md)
+ [Converting Oracle to Amazon RDS for Oracle](CHAP_Source.Oracle.ToRDSOracle.md)

## Permissions Required When Using Oracle as a Source Database<a name="CHAP_Source.Oracle.Permissions"></a>

The privileges required for Oracle as a source are listed following: 
+ CONNECT 
+ SELECT\_CATALOG\_ROLE 
+ SELECT ANY DICTIONARY 

## Connecting to Oracle as a Source Database<a name="CHAP_Source.Oracle.Connecting"></a>

Use the following procedure to connect to your Oracle source database with the AWS Schema Conversion Tool \(AWS SCT\)\. 

**To connect to an Oracle source database**

1. In the AWS Schema Conversion Tool, choose **Connect to Oracle**\.   
![\[Connect to source database\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/file_connect_to_oracle.png)

   The **Connect to Oracle** dialog box appears\.  
![\[Oracle connection information\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/source-oracle.png)

1. Provide the Oracle source database connection information\. Use the instructions in the following table\.   
****    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/CHAP_Source.Oracle.html)

1. Choose **Test Connection** to verify that you can successfully connect to your source database\. 

1. Choose **OK** to connect to your source database\.