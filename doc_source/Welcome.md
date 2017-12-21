# What Is the AWS Schema Conversion Tool?<a name="Welcome"></a>

You can use the AWS Schema Conversion Tool \(AWS SCT\) to convert your existing database schema from one database engine to another\. You can convert relational OLTP schema, or data warehouse schema\. Your converted schema is suitable for an Amazon Relational Database Service \(Amazon RDS\) MySQL DB instance, an Amazon Aurora DB cluster, an Amazon RDS PostgreSQL DB instance, or an Amazon Redshift cluster\. 

AWS SCT supports several industry standards, including Federal Information Processing Standards \(FIPS\) when connecting to an Amazon S3 bucket or other AWS resource\. AWS SCT is also Federal Risk and Authorization Management Program \(FedRAMP\) compliant\. For more information on using FIPS when accessing AWS resources, see 

AWS SCT supports the following OLTP conversions\. 


****  

| Source Database | Target Database on Amazon RDS | 
| --- | --- | 
|  Microsoft SQL Server \(version 2008 and later\)  | Amazon Aurora \(MySQL or PostgreSQL\), Microsoft SQL Server, MySQL, PostgreSQL | 
|  MySQL \(version 5\.5 and later\)  |  Amazon Aurora \(PostgreSQL\), MySQL, PostgreSQL  You can migrate schema and data from MySQL to an Amazon Aurora \(MySQL\) DB cluster without using AWS SCT\. For more information, see [ Migrating Data to an Amazon Aurora DB Cluster](http://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Aurora.Migrate.html)\.   | 
|  Oracle \(version 10\.2 and later\)  | Amazon Aurora \(MySQL or PostgreSQL\), MySQL, Oracle, PostgreSQL | 
|  PostgreSQL \(version 9\.1 and later\)  |  Amazon Aurora \(MySQL\), MySQL, PostgreSQL  | 

AWS SCT supports the following data warehouse conversions\. 


****  

| Source Database | Target Database on Amazon Redshift | 
| --- | --- | 
|  Greenplum Database \(version 4\.3 and later\)  | Amazon Redshift | 
|  Microsoft SQL Server \(version 2008 and later\)  | Amazon Redshift | 
|  Netezza \(version 7\.0\.3 and later\)  | Amazon Redshift | 
|  Oracle \(version 10 and later\)  | Amazon Redshift | 
|  Teradata \(version 13 and later\)  | Amazon Redshift | 
|  Vertica \(version 7\.2\.2 and later\)  | Amazon Redshift | 

## Converting Your Schema<a name="CHAP_SchemaConversionTool.Overview.Converting"></a>

AWS SCT provides a project\-based user interface to automatically convert the database schema of your source database into a format compatible with your target Amazon RDS instance\. If schema from your source database can't be converted automatically, AWS SCT provides guidance on how you can create equivalent schema in your target Amazon RDS database\. 

For information about how to install AWS SCT, see [Installing and Updating the AWS Schema Conversion Tool](CHAP_SchemaConversionTool.Installing.md)\. 

To get started with AWS SCT, and create your first project, see [Getting Started with the AWS Schema Conversion Tool](CHAP_SchemaConversionTool.GettingStarted.md)\. 

To start converting your schema, see [Converting Database Schema to Amazon RDS by Using the AWS Schema Conversion Tool](CHAP_SchemaConversionTool.Converting.md) or [Converting Data Warehouse Schema to Amazon Redshift by Using the AWS Schema Conversion Tool](CHAP_SchemaConversionTool.Converting.DW.md)\. 

## Additional Features of the AWS Schema Conversion Tool<a name="CHAP_SchemaConversionTool.Overview.AdditionalFeatures"></a>

In addition to converting your existing database schema from one database engine to another, AWS SCT has some additional features that help you move your data and applications to the cloud: 

+ You can use data extraction agents to extract data from your data warehouse to prepare to migrate it to Amazon Redshift\. To manage the data extraction agents, you can use AWS SCT\. For more information, see [Using Data Extraction Agents](Agents.DW.md)\. 

+ You can use AWS SCT to create AWS DMS endpoints and tasks\. You can run and monitor these tasks from AWS SCT\. For more information, see [Working with the AWS Database Migration Service Using the AWS Schema Conversion Tool](CHAP_SchemaConversionTool.DMSIntegration.md)\. 

+ In some cases, database features can't be converted to equivalent Amazon RDS or Amazon Redshift features\. The AWS SCT extension pack wizard can help you install AWS Lambda functions and Python libraries to emulate the features that can't be converted\. For more information, see [Using the AWS Schema Conversion Tool Extension Pack AWS Lambda Functions](CHAP_SchemaConversionTool.ExtensionPack.OLTP.md) and [Using the AWS Schema Conversion Tool Extension Pack Custom Python Library](CHAP_SchemaConversionTool.ExtensionPack.DW.md)\. 

+ You can use AWS SCT to optimize your existing Amazon Redshift database\. AWS SCT recommends sort keys and distribution keys to optimize your database\. For more information, see [Optimizing Amazon Redshift by Using the AWS Schema Conversion Tool](CHAP_SchemaConversionTool.RedshiftOpt.md)\. 

+ You can use AWS SCT to copy your existing on\-premises database schema to an Amazon RDS DB instance running the same engine\. You can use this feature to analyze potential cost savings of moving to the cloud and of changing your license type\. 

+ You can use AWS SCT to convert SQL in your C\+\+, C\#, Java, or other application code\. You can view, analyze, edit, and save the converted SQL code\. For more information, see [Converting Application SQL by Using the AWS Schema Conversion Tool](CHAP_SchemaConversionTool.Converting.App.md)\. 

## Providing Customer Feedback<a name="CHAP_SchemaConversionTool.Overview.Feedback"></a>

You can provide feedback about the AWS Schema Conversion Tool\. You can file a bug report, you can submit a feature request, or you can provide general information\. 

**To provide feedback about AWS SCT\.**

1. Start the AWS Schema Conversion Tool\.

1. Open the **Help** menu and then choose **Leave Feedback**\. The **Leave Feedback** dialog box appears\. 

1. For **Area**, choose **Information**, **Bug report**, or **Feature request**\. 

1. For **Source database**, choose your source database\. Choose **Any** if your feedback is not specific to a particular database\. 

1. For **Target database**, choose your target database\. Choose **Any** if your feedback is not specific to a particular database\. 

1. For **Title**, type a title for your feedback\. 

1. For **Message**, type your feedback\. 

1. Choose **Send** to submit your feedback\. 