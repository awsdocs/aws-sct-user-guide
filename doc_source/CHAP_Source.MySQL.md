# Using MySQL as a Source for AWS Schema Conversion Tool \(AWS SCT\)<a name="CHAP_Source.MySQL"></a>

You can use AWS SCT to convert schemas and application code from MySQL to the following targets: 
+ Amazon RDS for PostgreSQL
+ Amazon Aurora \(PostgreSQL\)
+ Amazon RDS for MySQL
+ Amazon Aurora \(MySQL\)

For more information, see the following sections:

**Topics**
+ [Privileges for MySQL as a Source Database](#CHAP_Source.MySQL.Permissions)
+ [Connecting to MySQL as a Source Database](#CHAP_Source.MySQL.Connecting)

## Privileges for MySQL as a Source Database<a name="CHAP_Source.MySQL.Permissions"></a>

The privileges required for MySQL as a source are listed following: 
+ SELECT ON \*\.\* 
+ SELECT ON mysql\.proc 
+ SHOW VIEW ON \*\.\* 

## Connecting to MySQL as a Source Database<a name="CHAP_Source.MySQL.Connecting"></a>

Use the following procedure to connect to your MySQL source database with the AWS Schema Conversion Tool \(AWS SCT\)\. 

**To connect to a MySQL source database**

1. In the AWS Schema Conversion Tool, choose **Connect to MySQL**\.   
![\[Connect to source database\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/file_connect_to_mysql.png)

   The **Connect to MySQL** dialog box appears\.  
![\[MySQL connection information\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/source-mysql.png)

1. Provide the MySQL source database connection information\. Use the instructions in the following table\.   
****    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/CHAP_Source.MySQL.html)

1. Choose **Test Connection** to verify that you can successfully connect to your source database\. 

1. Choose **OK** to connect to your source database\.