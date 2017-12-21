# Getting Started Converting Database Schema with the AWS Schema Conversion Tool<a name="CHAP_SchemaConversionTool.GettingStarted.Rel"></a>

Following, you can find information to help you convert your online transaction processing \(OLTP\) database schema from one database engine to another by using the AWS Schema Conversion Tool \(AWS SCT\)\. You can use the converted schema with an Amazon Relational Database Service \(Amazon RDS\) DB instance\. 

AWS SCT supports the following OLTP database conversions\. 


****  

| Source Database | Target Database on Amazon RDS | 
| --- | --- | 
|  Microsoft SQL Server \(version 2008 and later\)  | Amazon Aurora \(MySQL or PostgreSQL\), Microsoft SQL Server, MySQL, PostgreSQL | 
|  MySQL \(version 5\.5 and later\)  |  Amazon Aurora \(PostgreSQL\), MySQL, PostgreSQL  You can migrate schema and data from MySQL to an Amazon Aurora \(MySQL\) DB cluster without using AWS SCT\. For more information, see [ Migrating Data to an Amazon Aurora DB Cluster](http://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Aurora.Migrate.html)\.   | 
|  Oracle \(version 10\.2 and later\)  | Amazon Aurora \(MySQL or PostgreSQL\), MySQL, Oracle, PostgreSQL | 
|  PostgreSQL \(version 9\.1 and later\)  | Amazon Aurora \(MySQL\), MySQL, PostgreSQL | 

If you want to convert a data warehouse schema, see [Getting Started Converting Data Warehouse Schema with the AWS Schema Conversion Tool](CHAP_SchemaConversionTool.GettingStarted.DW.md)\. 

## Before You Begin<a name="CHAP_SchemaConversionTool.GettingStarted.Rel.Before"></a>

Before you complete the procedures in this topic, you must first do the following: 

1. Create an AWS SCT project\.

1. Connect to your source database\.

1. Connect to your target database\.

For more information, see [Getting Started with the AWS Schema Conversion Tool](CHAP_SchemaConversionTool.GettingStarted.md)\. 

## Converting Your Schema<a name="CHAP_SchemaConversionTool.GettingStarted.Rel.Convert"></a>

Use the following procedure to convert schema\. 

**To convert schema**

1. Choose **View**, and then choose **Main View**\.   
![\[Select main view\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/select_main_view.png)

1. In the left panel that displays the schema from your source database, choose a schema object to convert\. Open the context \(right\-click\) menu for the object, and then choose **Convert schema**\.   
![\[Convert schema\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/transform_schema.png)

1. When AWS SCT finishes converting the schema, you can view the proposed schema in the panel on the right of your project\. 

   At this point, no schema is applied to your target Amazon RDS DB instance\. The planned schema is part of your project\. If you select a converted schema item, you can see the planned schema command in the panel at lower center for your target Amazon RDS DB instance\. 

   You can edit the schema in this window\. The edited schema is stored as part of your project and is written to the target DB instance when you choose to apply your converted schema\.   
![\[View the converted schema\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/view_transformed_schema.png)

For more information, see [Converting Your Schema by Using the AWS Schema Conversion Tool](CHAP_SchemaConversionTool.Convert.md)\. 

## Creating and Reviewing the Database Migration Assessment Report<a name="CHAP_SchemaConversionTool.GettingStarted.Rel.Report"></a>

The *database migration assessment report* summarizes all of the action items for schema that can't be converted automatically to the engine of your target Amazon RDS DB instance\. The report also includes estimates of the amount of effort that it will take to write the equivalent code for your target DB instance\. 

You can create \(or update\) a database migration assessment report in your project at any time by using the following procedure\. 

**To create and view the database migration assessment report**

1. In the left panel that displays the schema from your source database, choose a schema object to create an assessment report for\. Open the context \(right\-click\) menu for the object, and then choose **Create Report**\.   
![\[Create database migration assessment report\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/create_assessment_report.png)

   The assessment report view opens\.

1. Choose the **Action Items** tab\. 

   The **Action Items** tab displays a list of items that describe the schema that can't be converted automatically\. Select one of the action items from the list\. AWS SCT highlights the item from your schema that the action item applies to, as shown following\.   
![\[Action items tab\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/action_items_tab.png)

1. Choose the **Summary** tab\. 

   The **Summary** tab displays the summary information from the database migration assessment report\. It shows the number of items that were converted automatically, and the number of items that were not converted automatically\. The summary also includes an estimate of the time that it will take to create schema in your target DB instance that are equivalent to those in your source database\. 

   The section **License Evaluation and Cloud Support** contains information about moving your existing on\-premises database schema to an Amazon RDS DB instance running the same engine\. For example, if you want to change license types, this section of the report tells you which features from your current database should be removed\. 

   An example of an assessment report summary is shown following\.   
![\[Assessment report summary\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/summary_tab.png)

1. Choose the **Summary** tab, and then choose **Save to PDF**\. The database migration assessment report is saved as a PDF file\. The PDF file contains both the summary and action item information\. 

   You can also choose **Save to CSV** to save the report as a comma\-separated values \(CSV\) file\. The CSV file contains only action item information\.   
![\[Database migration assessment report\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/assessment_report.png)

For more information, see [Creating and Using the Assessment Report in the AWS Schema Conversion Tool](CHAP_SchemaConversionTool.AssessmentReport.md)\. 

## Applying the Converted Schema to Your Target DB Instance<a name="CHAP_SchemaConversionTool.GettingStarted.Rel.Apply"></a>

You can apply the converted database schema to your target Amazon RDS DB instance\. After the schema has been applied to your target DB instance, you can update the schema based on the action items in the database migration assessment report\. 

**Warning**  
This procedure overwrites the existing target schema\. Be careful not to overwrite schema unintentionally\. Be careful not to overwrite schema in your target DB instance that you have already modified, or you will overwrite those changes\. 

**To apply the converted database schema to your target Amazon RDS DB instance**

1. Choose the schema element in the right panel of your project that displays the planned schema for your target DB instance\. 

1. Open the context \(right\-click\) menu for the schema element, and then choose **Apply to database**\.   
![\[Apply to database\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/write_to_database.png)

   The converted schema is applied to the target DB instance\.

For more information, see [Saving and Applying Your Converted Schema in the AWS Schema Conversion Tool](CHAP_SchemaConversionTool.SaveAndApply.md)\. 

## Related Topics<a name="CHAP_SchemaConversionTool.GettingStarted.Rel.Related"></a>

+ [Converting Database Schema to Amazon RDS by Using the AWS Schema Conversion Tool](CHAP_SchemaConversionTool.Converting.md)