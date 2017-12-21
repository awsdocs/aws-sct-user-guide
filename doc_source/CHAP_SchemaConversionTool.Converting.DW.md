# Converting Data Warehouse Schema to Amazon Redshift by Using the AWS Schema Conversion Tool<a name="CHAP_SchemaConversionTool.Converting.DW"></a>

The AWS Schema Conversion Tool \(AWS SCT\) automates much of the process of converting your data warehouse schema to a Amazon Redshift database schema\. The source and target database engines contain many different features and capabilities, and AWS SCT attempts to create an equivalent schema in your target database wherever possible\. If no direct conversion is possible, AWS SCT provides a list of possible actions for you to take\. 

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

If you want to convert an online transaction processing \(OLTP\) database schema, see [Converting Database Schema to Amazon RDS by Using the AWS Schema Conversion Tool](CHAP_SchemaConversionTool.Converting.md)\. 

Almost all work you do with AWS SCT starts with the following three steps: 

1. Create an AWS SCT project\.

1. Connect to your source database\.

1. Connect to your target database\.

If you have not created an AWS SCT project yet, see [Getting Started with the AWS Schema Conversion Tool](CHAP_SchemaConversionTool.GettingStarted.md)\. 

To convert your data warehouse schema to Amazon RDS, you take the following high\-level steps: 

+ **Choose your optimization strategy** – To optimize how AWS SCT converts your data warehouse schema, you can choose the strategies and rules you want the tool to use\. 

  For more information, see [Choosing Optimization Strategies and Rules for Use with the AWS Schema Conversion Tool](CHAP_SchemaConversionTool.DW.Strategy.md)\. 

   

+ **Collect statistics** – To optimize how AWS SCT converts your data warehouse schema, you can provide statistics from your source database that the tool can use\. You can either collect statistics directly from the database, or upload an existing statistics file\. 

  For more information, see [Collecting or Uploading Statistics for the AWS Schema Conversion Tool](CHAP_SchemaConversionTool.DW.Statistics.md)\. 

   

+ **Create mapping rules** – Before you convert your schema with AWS SCT, you can set up rules that change the data type of columns, move objects from one schema to another, and change the names of objects\. 

  For more information, see [Creating Mapping Rules in the AWS Schema Conversion Tool](CHAP_SchemaConversionTool.DW.Mapping.md)\. 

   

+ **Convert your schema** – AWS SCT creates a local version of the converted schema for you to review, but it doesn't apply it to your target database until you are ready\. 

  For more information, see [Converting Your Schema by Using the AWS Schema Conversion Tool](CHAP_SchemaConversionTool.DW.Convert.md)\. 

   

+ **Manage and customize keys** – After you convert your schema, you can manage and edit your keys\. Key management is the heart of a data warehouse conversion\. 

  For more information, see [Managing and Customizing Keys in the AWS Schema Conversion Tool](CHAP_SchemaConversionTool.DW.Keys.md)\. 

   

+ **Create a database migration assessment report** – AWS SCT creates a database migration assessment report that details the schema elements that can't be converted automatically\. You can use this report to identify where you need to manually create a schema in your target database that is compatible with your source database\. 

  For more information, see [Creating and Using the Assessment Report in the AWS Schema Conversion Tool](CHAP_SchemaConversionTool.DW.AssessmentReport.md)\. 

   

+ **Decide how to handle manual conversions** – If you have schema elements that can't be converted automatically, you have two choices: update the source schema and then convert again, or create equivalent schema elements in your target database\. 

  For more information, see [Handling Manual Conversions in the AWS Schema Conversion Tool](CHAP_SchemaConversionTool.DW.Manual.md)\. 

   

+ **Update and refresh the schema in your AWS SCT project** – You can update your AWS SCT project with the most recent schema from your source database\. 

  For more information, see [Updating and Refreshing Your Converted Schema in the AWS Schema Conversion Tool](CHAP_SchemaConversionTool.DW.UpdateRefresh.md)\. 

   

+ **Apply the converted schema to your target database** – When you are ready, have AWS SCT apply the converted schema in your local project to your target database\. 

  For more information, see [Saving and Applying Your Converted Schema in the AWS Schema Conversion Tool](CHAP_SchemaConversionTool.DW.SaveAndApply.md)\. 

   