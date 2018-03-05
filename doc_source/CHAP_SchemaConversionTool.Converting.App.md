# Converting Application SQL by Using the AWS Schema Conversion Tool<a name="CHAP_SchemaConversionTool.Converting.App"></a>

When you convert your database schema from one engine to another, you also need to update the SQL code in your applications to interact with the new database engine instead of the old one\. You can use the AWS Schema Conversion Tool \(AWS SCT\) to convert the SQL code in your C\+\+, C\#, Java, or other application code\. You can view, analyze, edit, and save the converted SQL code\. 

## Before You Begin<a name="CHAP_SchemaConversionTool.Converting.App.Before"></a>

Almost all work you do with AWS SCT starts with the following three steps: 

1. Create an AWS SCT project\.

1. Connect to your source database\.

1. Connect to your target database\.

If you have not created an AWS SCT project yet, see [Getting Started with the AWS Schema Conversion Tool](CHAP_SchemaConversionTool.GettingStarted.md)\. 

Because the SQL code in your application interacts with your database schema, you need to convert your database schema before you can convert your application SQL\. To convert your database schema, use the procedures in one of the following topics: 

+ [Converting Database Schemas Using the AWS Schema Conversion Tool](CHAP_SchemaConversionTool.Converting.md)

+ [ Converting Data Warehouse Schemas to Amazon Redshift by Using the AWS Schema Conversion Tool](CHAP_SchemaConversionTool.Converting.DW.md)

## Overview of Converting Application SQL<a name="CHAP_SchemaConversionTool.Converting.App.Overview"></a>

To convert the SQL code in your application, you take the following high\-level steps: 

+ **Create an application conversion project** – The application conversion project is a child of the database schema conversion project\. Each database schema conversion project can have one or more child application conversion projects\. 

  For more information, see [Creating Application Conversion Projects in the AWS Schema Conversion Tool](CHAP_SchemaConversionTool.Converting.App.Project.md)\. 

   

+ **Analyze and convert your SQL code** – AWS SCT analyzes your application, extracts the SQL code, and creates a local version of the converted SQL for you to review and edit\. The tool doesn't change the code in your application until you are ready\. 

  For more information, see [Analyzing and Converting Your SQL Code by Using the AWS Schema Conversion Tool](CHAP_SchemaConversionTool.Converting.App.Convert.md)\. 

   

+ **Create an application assessment report** – The application assessment report provides important information about the conversion of the application SQL code from your source database schema to your target database schema\. 

  For more information, see [Creating and Using the Assessment Report](CHAP_SchemaConversionTool.Converting.App.AssessmentReport.md)\. 

   

+ **Edit, apply changes to, and save your converted SQL code** – The assessment report includes a list of SQL code items that can't be converted automatically\. For these items, you can edit the SQL code manually to perform the conversion\. 

  For more information, see [Editing and Saving Your Converted SQL Code with the AWS Schema Conversion Tool](CHAP_SchemaConversionTool.Converting.App.Edit.md)\. 

   