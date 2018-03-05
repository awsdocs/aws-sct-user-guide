# Creating and Using the Assessment Report in the AWS Schema Conversion Tool<a name="CHAP_SchemaConversionTool.AssessmentReport"></a>

The AWS Schema Conversion Tool \(AWS SCT\) creates a *database migration assessment report* to help you convert your schema\. The database migration assessment report provides important information about the conversion of the schema from your source database to your target Amazon RDS DB instance\. The report summarizes all of the schema conversion tasks and details the action items for schema that can't be converted to the DB engine of your target DB instance\. The report includes estimates of the amount of effort that it will take to write the equivalent code in your target DB instance that can't be converted automatically\. This Estimated Complexity field is exported in the PDF version of the assessment report, but it is not included in the CSV version\. 

If you are using AWS SCT to copy your existing on\-premises database schema to an Amazon RDS DB instance running the same engine, the report can help you analyze requirements for moving to the AWS Cloud and for changing your license type\. 

## Creating a Database Migration Assessment Report<a name="CHAP_SchemaConversionTool.AssessmentReport.Create"></a>

Use the following procedure to create a database migration assessment report\.

**To create a database migration assessment report**

1. In the left panel that displays the schema from your source database, choose a schema object to create an assessment report for\. 

1. Open the context \(right\-click\) menu for the object, and then choose **Create Report**\.   
![\[Create database migration assessment report\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/create_assessment_report.png)

## Assessment Report Summary<a name="CHAP_SchemaConversionTool.AssessmentReport.Summary"></a>

After you create an assessment report, the assessment report view opens, showing the **Summary** tab\. The **Summary** tab displays the summary information from the database migration assessment report\. It shows items that were converted automatically, and items that were not converted automatically\. 

![\[Assessment report summary\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/summary_tab.png)

For schema items that can't be converted automatically to the target database engine, the summary includes an estimate of the effort required to create schema items in your target DB instance that are equivalent to those in your source\. 

The report categorizes the estimated time to convert these schema items as follows: 

+ **Simple** – Actions that can be completed in less than one hour\. 

+ **Medium** – Actions that are more complex and can be completed in one to four hours\. 

+ **Significant** – Actions that are very complex and take more than four hours to complete\. 

The section **License Evaluation and Cloud Support** contains information about moving your existing on\-premises database schema to an Amazon RDS DB instance running the same engine\. For example, if you want to change license types, this section of the report tells you which features from your current database should be removed\. 

## Assessment Report Action Items<a name="CHAP_SchemaConversionTool.AssessmentReport.ActionItems"></a>

The assessment report view also includes an **Action Items** tab\. This tab contains a list of items that can't be converted automatically to the database engine of your target Amazon RDS DB instance\. If you select an action item from the list, AWS SCT highlights the item from your schema that the action item applies to\. 

The report also contains recommendations for how to manually convert the schema item\. For more information about deciding how to handle manual conversions, see [Handling Manual Conversions in the AWS Schema Conversion Tool](CHAP_SchemaConversionTool.Manual.md)\. 

![\[Action items tab\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/action_items_tab.png)

## Saving the Assessment Report<a name="CHAP_SchemaConversionTool.AssessmentReport.Save"></a>

You can save a local copy of the database migration assessment report as either a PDF file or a comma\-separated values \(CSV\) file\. The CSV file contains only action item information\. The PDF file contains both the summary and action item information, as shown in the following example\. 

![\[Database migration assessment report\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/assessment_report.png)