# Getting Started with the AWS Schema Conversion Tool<a name="CHAP_GettingStarted"></a>

You can use the AWS Schema Conversion Tool \(AWS SCT\) to convert your source database schema to a schema for databases hosted on Amazon Web Services \(AWS\)\. The AWS SCT application provides a project\-based user interface\. Almost all work you do with AWS SCT starts with the following steps:

1. Install AWS SCT\. For more information, see [Installing, Verifying, and Updating the AWS Schema Conversion Tool \(AWS SCT\)](CHAP_Installing.md)\.

1. Install a data extractor agent if you want to migrate data from a data warehouse to Amazon Redshift\. For more information, see [Using Data Extraction Agents](CHAP_Agents.DW.md)\.

   Install a replication agent if you want to migrate data to AWS using Amazon Snowball or Amazon S3, or if you are using AWS Database Migration Service \(AWS DMS\)\. For more information, see [ Using the AWS Schema Conversion Tool with the AWS Database Migration Service ](CHAP_DMSIntegration.md)\.

1. Familiarize yourself with the user interface of AWS SCT\. For more information, see [ Using the AWS Schema Conversion Tool \(AWS SCT\) User Interface](CHAP_UserInterface.md)\.

1. Create an AWS SCT project\. Connect to your source and target databases\. For more information about connecting to your source database, see [Source Databases for the AWS Schema Conversion Tool](CHAP_Source.md)\.

1. Run and then review the Database Migration Assessment Report\. For more information about the assessment report, see [ Creating and Reviewing the Database Migration Assessment Report](CHAP_UserInterface.md#CHAP_UserInterface.AssessmentReport)\.

1. Convert the source database schemas\. There are several aspects of the conversion you need to keep in mind, such as what to do with items that don't convert, and how to map items that should be converted a particular way\. For more information about converting a source schema, see [Converting Database Schemas Using the AWS Schema Conversion Tool](CHAP_Converting.md)\.

   If you are converting a data warehouse schema, there are also aspects you need to consider before doing the conversion\. For more information, see [ Converting Data Warehouse Schemas to Amazon Redshift Using the AWS Schema Conversion Tool](CHAP_Converting.DW.md)\.

1. Applying the schema conversion to your target\. For more information about applying a source schema conversion, see [ Using the AWS Schema Conversion Tool \(AWS SCT\) User Interface](CHAP_UserInterface.md)\.

1. The AWS SCT can also be used to convert SQL stored procedures and other application code\. For more information, see [Converting Application SQL Using the AWS Schema Conversion Tool](CHAP_Converting.App.md)

You can also use AWS SCT to migrate your data from a source database to an Amazon\-managed database\. For more information, see 