# Using virtual targets<a name="CHAP_Mapping.VirtualTargets"></a>

You can see how AWS SCT converts your source database schema to any supported target database platform\. To do so, you don't need to connect to an existing target database\. Instead, you can choose a virtual target database platform in the right panel when you create a mapping rule\. For more information, see [Adding a new mapping rule](CHAP_Mapping.New.md)\. Make sure that you expand the **Servers**, **NoSQL clusters**, and **ETL** nodes in the right panel to see the list of virtual target database platforms\. 

 AWS SCT supports the following virtual target database platforms: 
+ Amazon Aurora MySQL\-Compatible Edition
+ Amazon Aurora PostgreSQL\-Compatible Edition
+ Amazon DynamoDB
+ Amazon Redshift
+ Amazon Redshift and AWS Glue
+ AWS Glue
+ AWS Glue Studio
+ Babelfish for Aurora PostgreSQL
+ MariaDB
+ Microsoft SQL Server
+ MySQL
+ Oracle
+ PostgreSQL

 If you use Babelfish for Aurora PostgreSQL as a target database platform, you can only create a database migration assessment report\. For more information, see [Creating migration assessment reports with AWS SCT](CHAP_AssessmentReport.md)\. 

 If you use a virtual target database platform, you can save converted code to a file\. For more information, see [Saving your converted schema to a file](CHAP_Converting.md#CHAP_Converting.Saving)\. 