# Getting Started Converting Data Warehouse Schema with the AWS Schema Conversion Tool<a name="CHAP_SchemaConversionTool.GettingStarted.DW"></a>

Following, you can find information to help you convert your data warehouse schema from one database engine to another by using the AWS Schema Conversion Tool \(AWS SCT\)\. You can use the converted schema with an Amazon Redshift cluster\. 

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

If you want to convert an online transaction processing \(OLTP\) database schema, see [Getting Started Converting Database Schema with the AWS Schema Conversion Tool](CHAP_SchemaConversionTool.GettingStarted.Rel.md)\. 

## Before You Begin<a name="CHAP_SchemaConversionTool.GettingStarted.DW.Before"></a>

Before you complete the procedures in this topic, you must first do the following: 

1. Create an AWS SCT project\.

1. Connect to your source database\.

1. Connect to your target database\.

For more information, see [Getting Started with the AWS Schema Conversion Tool](CHAP_SchemaConversionTool.GettingStarted.md)\. 

## Choosing Optimization Strategies and Rules<a name="CHAP_SchemaConversionTool.GettingStarted.DW.Strategy"></a>

To optimize how AWS SCT converts your data warehouse schema, you can choose the strategies and rules you want the tool to use\. After converting your schema, and reviewing the suggested keys, you can adjust your rules or change your strategy to get the results you want\. 

**To choose your optimization strategies and rules**

1. Choose **Settings**, and then choose **Project Settings**\. The **Current project settings** dialog box appears\. 

1. In the left pane, choose **Optimization Strategies**\. The optimization strategies appear in the right pane with the defaults selected\. 

1. For **Strategy Sector**, choose the optimization strategy you want to use\. You can choose from the following: 

   + **Use metadata, ignore statistical information** – In this strategy, only information from the metadata is used for optimization decisions\. For example, if there is more than one index on a source table, the source database sort order is used, and the first index becomes a distribution key\. 

      

   + **Ignore metadata, use statistical information** – In this strategy, optimization decisions about derived from statistical information only\. This strategy applies only to tables and columns for which statistics are provided\. For more information, see [Collecting or Uploading Statistics for the AWS Schema Conversion Tool](CHAP_SchemaConversionTool.DW.Statistics.md)\. 

      

   + **Use metadata and use statistical information** – In this strategy, both metadata and statistics are used for optimization decisions\. 

      

1. After you choose your optimization strategy, you can choose the rules you want to use\. You can choose from the following: 

   + **Choose Distribution Key and Sort Keys using metadata**

   + **Choose fact table and appropriate dimension for collation**

   + **Analyze cardinality of indexes' columns**

   + **Find the most used tables and columns from QueryLog table**

   For each rule, you can enter a weight for the sort key and a weight for the distribution key\. AWS SCT uses the weights you choose when it converts your schema\. 

For more information, see [Choosing Optimization Strategies and Rules for Use with the AWS Schema Conversion Tool](CHAP_SchemaConversionTool.DW.Strategy.md)\. 

## Collecting or Uploading Statistics<a name="CHAP_SchemaConversionTool.GettingStarted.DW.Statistics"></a>

To optimize how AWS SCT converts your data warehouse schema, you can provide statistics from your source database that the tool can use\. You can either collect statistics directly from the database, or upload an existing statistics file\. 

**To provide and review statistics**

1. Connect to your source database\. For more information, see [Connecting to Your Source Database](CHAP_SchemaConversionTool.GettingStarted.md#CHAP_SchemaConversionTool.Converting.CreateProject)\. 

1. Choose a schema object from the left panel of your project, and open the context \(right\-click\) menu for the object\. Choose **Collect Statistics** or **Upload Statistics** as shown following\.   
![\[Context menu with collect statistics\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/collect-statistics.png)

1. Choose a schema object from the left panel of your project, and then choose the **Statistics** tab\. You can review the statistics for the object\.   
![\[Statistics tab\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/statistics.png)

For more information, see [Collecting or Uploading Statistics for the AWS Schema Conversion Tool](CHAP_SchemaConversionTool.DW.Statistics.md)\. 

## Converting Your Schema<a name="CHAP_SchemaConversionTool.GettingStarted.DW.Convert"></a>

Use the following procedure to converted schema\. 

**To convert schema**

1. Choose **View**, and then choose **Main View**\.   
![\[Select main view\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/select_main_view.png)

1. In the left panel that displays the schema from your source database, choose a schema object to convert\. Open the context \(right\-click\) menu for the object, and then choose **Convert schema**\.   
![\[Convert schema\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/transform_schema.png)

1. When AWS SCT finishes converting the schema, you can view the proposed schema in the panel on the right of your project\. 

   At this point, no schema is applied to your target database\. The planned schema is part of your project\. If you select a converted schema item, you can see the planned schema command in the panel at lower center for your target database\. 

   You can edit the schema in this window\. The edited schema is stored as part of your project and is written to the target database when you choose to apply your converted schema\.   
![\[View the converted schema\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/view_transformed_schema.png)

For more information, see [Converting Your Schema by Using the AWS Schema Conversion Tool](CHAP_SchemaConversionTool.DW.Convert.md)\. 

## Managing and Customizing Keys<a name="CHAP_SchemaConversionTool.GettingStarted.DW.Keys"></a>

After you convert your schema, you can manage and edit your keys\. Key management is the heart of a data warehouse conversion\. 

To manage keys, select a table in your target database, and then choose the **Key Management** tab as shown following\. 

![\[Key management tab\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/key-management.png)

The left pane contains key suggestions, and includes the confidence rating for each suggestion\. You can choose one of the suggestions, or you can customize the key by editing it in the right pane\. 

If the choices for the key don't look like what you expected, you can edit your edit your optimization strategies, and then retry the conversion\. For more information, see [Choosing Optimization Strategies and Rules](#CHAP_SchemaConversionTool.GettingStarted.DW.Strategy)\. 

For more information, see [Managing and Customizing Keys in the AWS Schema Conversion Tool](CHAP_SchemaConversionTool.DW.Keys.md)\. 

## Creating and Reviewing the Database Migration Assessment Report<a name="CHAP_SchemaConversionTool.GettingStarted.DW.Report"></a>

The *database migration assessment report* summarizes all of the action items for schema that can't be converted automatically to the engine of your target database\. The report also includes estimates of the amount of effort that it will take to write the equivalent code for your target database\. 

You can create \(or update\) a database migration assessment report in your project at any time by using the following procedure\. 

**To create and view the database migration assessment report**

1. In the left panel that displays the schema from your source database, choose a schema object to create an assessment report for\. Open the context \(right\-click\) menu for the object, and then choose **Create Report**\.   
![\[Create database migration assessment report\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/create_assessment_report.png)

   The assessment report view opens\.

1. Choose the **Action Items** tab\. 

   The **Action Items** tab displays a list of items that describe the schema that can't be converted automatically\. Select one of the action items from the list\. AWS SCT highlights the item from your schema that the action item applies to, as shown following\.   
![\[Action items tab\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/action_items_tab.png)

1. Choose the **Summary** tab\. 

   The **Summary** tab displays the summary information from the database migration assessment report\. It shows the number of items that were converted automatically, and the number of items that were not converted automatically\. The summary also includes an estimate of the time that it will take to create schema in your target database that are equivalent to those in your source database\. An example is shown following\.   
![\[Assessment report summary\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/summary_tab.png)

1. Choose the **Summary** tab, and then choose **Save to PDF**\. The database migration assessment report is saved as a PDF file\. The PDF file contains both the summary and action item information\. 

   You can also choose **Save to CSV** to save the report as a comma\-separated values \(CSV\) file\. The CSV file contains only action item information\.   
![\[Database migration assessment report\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/assessment_report.png)

For more information, see [Creating and Using the Assessment Report in the AWS Schema Conversion Tool](CHAP_SchemaConversionTool.DW.AssessmentReport.md)\. 

## Applying the Converted Schema to Your Target Database<a name="CHAP_SchemaConversionTool.GettingStarted.DW.Apply"></a>

You can apply the converted database schema to your target database\. After the schema has been applied to your target database, you can update the schema based on the action items in the database migration assessment report\. 

**Warning**  
This procedure overwrites the existing target schema\. Be careful not to overwrite schema unintentionally\. Be careful not to overwrite schema in your target database that you have already modified, or you will overwrite those changes\. 

**To apply the converted database schema to your target database**

1. Choose the schema element in the right panel of your project that displays the planned schema for your target database\. 

1. Open the context \(right\-click\) menu for the schema element, and then choose **Apply to database**\.   
![\[Apply to database\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/write_to_database.png)

   The converted schema is applied to the target database\.

For more information, see [Saving and Applying Your Converted Schema in the AWS Schema Conversion Tool](CHAP_SchemaConversionTool.DW.SaveAndApply.md)\. 

## Related Topics<a name="CHAP_SchemaConversionTool.GettingStarted.DW.Related"></a>

+ [Converting Data Warehouse Schema to Amazon Redshift by Using the AWS Schema Conversion Tool](CHAP_SchemaConversionTool.Converting.DW.md)