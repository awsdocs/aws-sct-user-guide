# What is the AWS Schema Conversion Tool?<a name="CHAP_Welcome"></a>

You can use the AWS Schema Conversion Tool \(AWS SCT\) to convert your existing database schema from one database engine to another\. You can convert relational OLTP schema, or data warehouse schema\. Your converted schema is suitable for an Amazon Relational Database Service \(Amazon RDS\) MySQL, MariaDB, Oracle, SQL Server, PostgreSQL DB, an Amazon Aurora DB cluster, or an Amazon Redshift cluster\. The converted schema can also be used with a database on an Amazon EC2 instance or stored as data on an Amazon S3 bucket\.

AWS SCT supports several industry standards, including Federal Information Processing Standards \(FIPS\), for connections to an Amazon S3 bucket or another AWS resource\. AWS SCT is also compliant with Federal Risk and Authorization Management Program \(FedRAMP\)\. For details about AWS and compliance efforts, see [AWS services in scope by compliance program](https://aws.amazon.com/compliance/services-in-scope/)\.

AWS SCT supports the following OLTP conversions\. 


****  

| Source database | Target database | 
| --- | --- | 
| IBM Db2 for z/OS \(version 12\) |  Amazon Aurora MySQL\-Compatible Edition \(Aurora MySQL\), Amazon Aurora PostgreSQL\-Compatible Edition \(Aurora PostgreSQL\), MySQL, PostgreSQL  For more information, see [Using IBM Db2 for z/OS as a source](CHAP_Source.DB2zOS.md)\.   | 
|  IBM Db2 LUW \(versions 9\.1, 9\.5, 9\.7, 10\.5, 11\.1, and 11\.5\)  |  Aurora MySQL, Aurora PostgreSQL, MariaDB, MySQL, PostgreSQL  For more information, see [Using IBM Db2 LUW as a source](CHAP_Source.DB2LUW.md)\.   | 
| Microsoft Azure SQL Database |  Aurora MySQL, Aurora PostgreSQL, MySQL, PostgreSQL  For more information, see [Using Azure SQL Database as a source](CHAP_Source.AzureSQL.md)\.   | 
|  Microsoft SQL Server \(version 2008 R2 and later\)  |  Aurora MySQL, Aurora PostgreSQL, Babelfish for Aurora PostgreSQL \(only for assessment reports\), MariaDB, Microsoft SQL Server, MySQL, PostgreSQL   For more information, see [Using SQL Server as a source](CHAP_Source.SQLServer.md)\.   | 
|  MySQL \(version 5\.5 and later\)  |  Aurora PostgreSQL, MySQL, PostgreSQL  For more information, see [Using MySQL as a source](CHAP_Source.MySQL.md)\.  You can migrate schema and data from MySQL to an Aurora MySQL DB cluster without using AWS SCT\. For more information, see [Migrating data to an Amazon Aurora DB cluster](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Aurora.Migrate.html)\.   | 
|  Oracle \(version 10\.1 and later\)  |   Aurora MySQL, Aurora PostgreSQL, MariaDB, MySQL, Oracle, PostgreSQL   For more information, see [Using Oracle Database as a source](CHAP_Source.Oracle.md)\.   | 
|  PostgreSQL \(version 9\.1 and later\)  |  Aurora MySQL, Aurora PostgreSQL, MySQL, PostgreSQL  For more information, see [Using PostgreSQL as a source](CHAP_Source.PostgreSQL.md)\.   | 
| SAP ASE \(versions 12\.5\.4, 15\.0\.2, 15\.5, 15\.7, and 16\.0\) |   Aurora MySQL, Aurora PostgreSQL, MariaDB, MySQL, PostgreSQL   For more information, see [Using SAP ASE \(Sybase ASE\) as a source](CHAP_Source.SAP.md)\.   | 

AWS SCT supports the following data warehouse conversions\. 


****  

| Source data warehouse | Target data warehouse | 
| --- | --- | 
|  Amazon Redshift  |  Amazon Redshift  For more information, see [Using Amazon Redshift as a source](CHAP_Source.Redshift.md)\.   | 
|  Azure Synapse Analytics \(version 10\)  |  Amazon Redshift  For more information, see [Using Azure Synapse Analytics as a source](CHAP_Source.AzureSynapse.md)\.   | 
|  BigQuery  |  Amazon Redshift  For more information, see [Using BigQuery as a source](CHAP_Source.BigQuery.md)\.   | 
|  Greenplum Database \(versions 4\.3 and 6\.21\)  |  Amazon Redshift  For more information, see [Using Greenplum Database as a source](CHAP_Source.Greenplum.md)\.   | 
|  Microsoft SQL Server \(version 2008 and later\)  |  Amazon Redshift  For more information, see [Using SQL Server Data Warehouse as a source](CHAP_Source.SQLServerDW.md)\.   | 
|  Netezza \(version 7\.0\.3 and later\)  |  Amazon Redshift  For more information, see [Using Netezza as a source](CHAP_Source.Netezza.md)\.   | 
|  Oracle \(version 10\.1 and later\)  |  Amazon Redshift  For more information, see [Using Oracle Data Warehouse as a source](CHAP_Source.OracleDW.md)\.   | 
|  Teradata \(version 13 and later\)  |  Amazon Redshift  For more information, see [Using Teradata as a source](CHAP_Source.Teradata.md)\.   | 
|  Vertica \(version 9\.1 and 11\.0\)  |  Amazon Redshift  For more information, see [Using Vertica as a source](CHAP_Source.Vertica.md)\.   | 
|  Snowflake \(version 3\)  |  Amazon Redshift  For more information, see [Using Snowflake as a source](CHAP_Source.Snowflake.md)\.   | 

AWS SCT supports the following data NoSQL database conversions\. 


****  

| Source database | Target database | 
| --- | --- | 
|  Apache Cassandra \(versions 2\.1\.x, 2\.2\.16, and 3\.11\.x\)  |  Amazon DynamoDB  For more information, see [Using Apache Cassandra as a source](CHAP_Source.Cassandra.md)\.   | 

AWS SCT supports conversions of the following extract, transform, and load \(ETL\) processes\. For more information, see [Converting ETL processes](CHAP-converting-etl.md)\. 


****  

| Source | Target | 
| --- | --- | 
| Informatica ETL scripts | Informatica | 
| Microsoft SQL Server Integration Services \(SSIS\) ETL packages | AWS Glue or AWS Glue Studio | 
| Shell scripts with embedded commands from Teradata Basic Teradata Query \(BTEQ\)  | Amazon Redshift RSQL | 
| Teradata BTEQ ETL scripts | AWS Glue or Amazon Redshift RSQL | 
| Teradata FastExport job scripts | Amazon Redshift RSQL | 
| Teradata FastLoad job scripts | Amazon Redshift RSQL | 
| Teradata MultiLoad job scripts | Amazon Redshift RSQL | 

AWS SCT supports the following big data framework migrations\. For more information, see [Using Apache Hadoop as a source](CHAP_Source.Hadoop.md)\. 


****  

| Source | Target | 
| --- | --- | 
|  Apache Hive \(version 0\.13\.0 and later\)  |  Hive on Amazon EMR  | 
|  Apache HDFS  |  Amazon S3 or HDFS on Amazon EMR  | 

## Schema conversion overview<a name="CHAP_Welcome.Overview"></a>

AWS SCT provides a project\-based user interface to automatically convert the database schema of your source database into a format compatible with your target Amazon RDS instance\. If schema from your source database can't be converted automatically, AWS SCT provides guidance on how you can create equivalent schema in your target Amazon RDS database\. 

For information about how to install AWS SCT, see [Installing, verifying, and updating AWS SCT](CHAP_Installing.md)\. 

For an introduction to the AWS SCT user interface, see [Using the AWS SCT user interface](CHAP_UserInterface.md)\. 

For information on the conversion process, see [Converting database schemas using AWS SCT](CHAP_Converting.md)\. 

In addition to converting your existing database schema from one database engine to another, AWS SCT has some additional features that help you move your data and applications to the AWS Cloud: 
+ You can use data extraction agents to extract data from your data warehouse to prepare to migrate it to Amazon Redshift\. To manage the data extraction agents, you can use AWS SCT\. For more information, see [Using data extraction agents](agents.md)\. 
+ You can use AWS SCT to create AWS DMS endpoints and tasks\. You can run and monitor these tasks from AWS SCT\. For more information, see [Using AWS SCT with AWS DMS](CHAP_DMSIntegration.md)\. 
+ In some cases, database features can't be converted to equivalent Amazon RDS or Amazon Redshift features\. The AWS SCT extension pack wizard can help you install AWS Lambda functions and Python libraries to emulate the features that can't be converted\. For more information, see [Using AWS SCT extension packs](CHAP_ExtensionPack.md)\. 
+ You can use AWS SCT to optimize your existing Amazon Redshift database\. AWS SCT recommends sort keys and distribution keys to optimize your database\. For more information, see [Optimizing Amazon Redshift by using AWS SCT](CHAP_Converting.DW.RedshiftOpt.md)\. 
+ You can use AWS SCT to copy your existing on\-premises database schema to an Amazon RDS DB instance running the same engine\. You can use this feature to analyze potential cost savings of moving to the cloud and of changing your license type\. 
+ You can use AWS SCT to convert SQL in your C\+\+, C\#, Java, or other application code\. You can view, analyze, edit, and save the converted SQL code\. For more information, see [Converting application SQL using AWS SCT](CHAP_Converting.App.md)\. 
+ You can use AWS SCT to migrate extraction, transformation, and load \(ETL\) processes\. For more information, see [Converting extract, transform, and load \(ETL\) processes with AWS Schema Conversion Tool](CHAP-converting-etl.md)\. 

## Providing feedback<a name="CHAP_Welcome.Feedback"></a>

You can provide feedback about AWS SCT\. You can file a bug report, submit a feature request, or provide general information\.

**To provide feedback about AWS SCT**

1. Start the AWS Schema Conversion Tool\.

1. Open the **Help** menu and then choose **Leave Feedback**\. The **Leave Feedback** dialog box appears\. 

1. For **Area**, choose **Information**, **Bug report**, or **Feature request**\. 

1. For **Source database**, choose your source database\. Choose **Any** if your feedback is not specific to a particular database\. 

1. For **Target database**, choose your target database\. Choose **Any** if your feedback is not specific to a particular database\. 

1. For **Title**, type a title for your feedback\. 

1. For **Message**, type your feedback\. 

1. Choose **Send** to submit your feedback\. 