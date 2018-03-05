# Converting Database Schemas Using the AWS Schema Conversion Tool<a name="CHAP_SchemaConversionTool.Converting"></a>

You can use the AWS Schema Conversion Tool \(AWS SCT\) to convert your existing database schemas from one database engine to another\. You can use the AWS SCT to do the following: 

+ You can also use AWS SCT to copy an existing on\-premises database schema to an Amazon RDS DB instance running the same engine\. You can use this feature to analyze potential cost savings of moving to the cloud and of changing your license type\. 

+ In some cases, database features can't be converted to equivalent Amazon RDS features\. If you host and self\-manage a database on the Amazon Elastic Compute Cloud \(Amazon EC2\) platform, you can emulate these features by substituting AWS services for them\. 

+ You can also use AWS SCT to copy your existing on\-premises database schema to an Amazon RDS DB instance running the same engine\. You can use this feature to analyze potential cost savings of moving to the cloud\.

+ AWS SCT automates much of the process of converting your online transaction processing \(OLTP\) database schema to an Amazon Relational Database Service \(Amazon RDS\) MySQL DB instance, an Amazon Aurora DB cluster, or a PostgreSQL DB instance\. The source and target database engines contain many different features and capabilities, and AWS SCT attempts to create an equivalent schema in your Amazon RDS DB instance wherever possible\. If no direct conversion is possible, AWS SCT provides a list of possible actions for you to take\. 

This section includes the following topics:


+ [Creating Mapping Rules in the AWS Schema Conversion Tool](CHAP_SchemaConversionTool.Mapping.md)
+ [Converting Your Schema by Using the AWS Schema Conversion Tool](CHAP_SchemaConversionTool.Convert.md)
+ [Creating and Using the Assessment Report in the AWS Schema Conversion Tool](CHAP_SchemaConversionTool.AssessmentReport.md)
+ [Handling Manual Conversions in the AWS Schema Conversion Tool](CHAP_SchemaConversionTool.Manual.md)
+ [Updating and Refreshing Your Converted Schema in the AWS Schema Conversion Tool](CHAP_SchemaConversionTool.UpdateRefresh.md)
+ [Saving and Applying Your Converted Schema in the AWS Schema Conversion Tool](CHAP_SchemaConversionTool.SaveAndApply.md)
+ [Comparing Database Schemas](CHAP_Converting.SchemaCompare.md)
+ [Finding Related Transformed Objects](CHAP_Converting.RelatedObjects.md)
+ [Converting Dynamic SQL for Oracle to PostgreSQL Migrations](CHAP_Converting.DynamicSQL.md)

AWS SCT supports the following OLTP conversions\. 


****  

| Source Database | Target Database on Amazon RDS | 
| --- | --- | 
|  Microsoft SQL Server \(version 2008 and later\)  | Amazon Aurora \(MySQL or PostgreSQL\), Microsoft SQL Server, MySQL, PostgreSQL | 
|  MySQL \(version 5\.5 and later\)  |  Amazon Aurora \(PostgreSQL\), MySQL, PostgreSQL  You can migrate schema and data from MySQL to an Amazon Aurora \(MySQL\) DB cluster without using AWS SCT\. For more information, see [ Migrating Data to an Amazon Aurora DB Cluster](http://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Aurora.Migrate.html)\.   | 
|  Oracle \(version 10\.2 and later\)  | Amazon Aurora \(MySQL or PostgreSQL\), MySQL, Oracle, PostgreSQL | 
|  PostgreSQL \(version 9\.1 and later\)  | Amazon Aurora \(MySQL\), MySQL, PostgreSQL | 

If you want to convert a data warehouse schema, see [ Converting Data Warehouse Schemas to Amazon Redshift by Using the AWS Schema Conversion Tool](CHAP_SchemaConversionTool.Converting.DW.md)\. 

Almost all work you do with AWS SCT starts with the following three steps: 

1. Create an AWS SCT project\.

1. Connect to your source database\.

1. Connect to your target database\.

If you have not created an AWS SCT project yet, see [Getting Started with the AWS Schema Conversion Tool](CHAP_SchemaConversionTool.GettingStarted.md)\. 

To convert your database schema to Amazon RDS, you take the following high\-level steps: 

+ **Create mapping rules** – Before you convert your schema with AWS SCT, you can set up rules that change the data type of columns, move objects from one schema to another, and change the names of objects\. 

  For more information, see [Creating Mapping Rules in the AWS Schema Conversion Tool](CHAP_SchemaConversionTool.Mapping.md)\. 

+ **Convert your schema** – AWS SCT creates a local version of the converted schema for you to review, but it doesn't apply it to your target DB instance until you are ready\. 

  For more information, see [Converting Your Schema by Using the AWS Schema Conversion Tool](CHAP_SchemaConversionTool.Convert.md)\. 

+ **Create a database migration assessment report** – AWS SCT creates a database migration assessment report that details the schema elements that can't be converted automatically\. You can use this report to identify where you need to create a schema in your Amazon RDS DB instance that is compatible with your source database\. 

  For more information, see [Creating and Using the Assessment Report in the AWS Schema Conversion Tool](CHAP_SchemaConversionTool.AssessmentReport.md)\. 

+ **Decide how to handle manual conversions** – If you have schema elements that can't be converted automatically, you have two choices: update the source schema and then convert again, or create equivalent schema elements in your target Amazon RDS DB instance\. 

  For more information, see [Handling Manual Conversions in the AWS Schema Conversion Tool](CHAP_SchemaConversionTool.Manual.md)\. 

+ **Update and refresh the schema in your AWS SCT project** – You can update your AWS SCT project with the most recent schema from your source database\. 

  For more information, see [Updating and Refreshing Your Converted Schema in the AWS Schema Conversion Tool](CHAP_SchemaConversionTool.UpdateRefresh.md)\. 

+ **Apply the converted schema to your target database** – When you are ready, have AWS SCT apply the converted schema in your local project to your target Amazon RDS DB instance\. 

  For more information, see [Saving and Applying Your Converted Schema in the AWS Schema Conversion Tool](CHAP_SchemaConversionTool.SaveAndApply.md)\. 