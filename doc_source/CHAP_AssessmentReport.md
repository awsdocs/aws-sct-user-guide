# AWS Schema Conversion Tool Assessment Report<a name="CHAP_AssessmentReport"></a>

An important part of the AWS Schema Conversion Tool \(AWS SCT\) is the *database migration assessment report* that it generates to help you convert your schema\. The report summarizes all of the schema conversion tasks and details the action items for schema that can't be converted to the DB engine of your target DB instance\. You can view the report in the application\. To do so, export it as a comma\-separated value \(CSV\) or PDF file\.

The migration assessment report includes the following:
+ Executive summary
+ License evaluation
+ Cloud support, indicating any features in the source database not available on the target\.
+ Current source hardware configuration
+ Recommendations, including conversion of server objects, backup suggestions, and linked server changes

The report includes information about an Amazon RDS DB instance if you selected Amazon RDS as your target, including the following:
+ The currently used storage size and maximum storage size for the DB instance\. 
+ The current number of databases on the DB instance and the maximum number of databases allowed on the DB instance\.
+ A list of database services and server objects that are not available on the DB instance\. 
+ A list of databases that are currently participating in replication\. Amazon RDS doesn't support replication\.

The report also includes estimates of the amount of effort that it will take to write the equivalent code for your target DB instance that can't be converted automatically\. This Estimated Complexity field is exported in the PDF version of the assessment report, but it's not included in the CSV version\. 

If you use AWS SCT to migrate your existing schema to an Amazon RDS DB instance, the report can help you analyze requirements for moving to the AWS Cloud and for changing your license type\. 

You can find more details in the following topics:

**Topics**
+ [Creating a Database Migration Assessment Report](#CHAP_AssessmentReport.Create)
+ [Assessment Report Summary](#CHAP_AssessmentReport.Summary)
+ [Assessment Report Action Items](#CHAP_AssessmentReport.ActionItems)
+ [Saving the Assessment Report](#CHAP_AssessmentReport.Save)

## Creating a Database Migration Assessment Report<a name="CHAP_AssessmentReport.Create"></a>

Use the following procedure to create a database migration assessment report\.

**To create a database migration assessment report**

1. In the left panel that displays the schema from your source database, choose a schema object to create an assessment report for\. 

1. Open the context \(right\-click\) menu for the object, and then choose **Create Report**\.   
![\[Create database migration assessment report\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/create_assessment_report.png)

## Assessment Report Summary<a name="CHAP_AssessmentReport.Summary"></a>

After you create an assessment report, the assessment report view opens, showing the **Summary** tab\. The **Summary** tab displays the summary information from the database migration assessment report\. It shows items that were converted automatically, and items that were not converted automatically\. 

![\[Assessment report summary\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/summary_tab.png)

For schema items that can't be converted automatically to the target database engine, the summary includes an estimate of the effort required to create schema items in your target DB instance that are equivalent to those in your source\. 

The report categorizes the estimated time to convert these schema items as follows: 
+ **Simple** – Actions that can be completed in less than one hour\. 
+ **Medium** – Actions that are more complex and can be completed in one to four hours\. 
+ **Significant** – Actions that are very complex and take more than four hours to complete\. 

The section **License Evaluation and Cloud Support** contains information about moving your existing on\-premises database schema to an Amazon RDS DB instance running the same engine\. For example, if you want to change license types, this section of the report tells you which features from your current database should be removed\. 

## Assessment Report Action Items<a name="CHAP_AssessmentReport.ActionItems"></a>

The assessment report view also includes an **Action Items** tab\. This tab contains a list of items that can't be converted automatically to the database engine of your target Amazon RDS DB instance\. If you select an action item from the list, AWS SCT highlights the item from your schema that the action item applies to\. 

The report also contains recommendations for how to manually convert the schema item\. For more information about deciding how to handle manual conversions, see [Handling Manual Conversions in the AWS Schema Conversion Tool](CHAP_Converting.md#CHAP_Converting.Manual)\. 

![\[Action items tab\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/action_items_tab.png)

## Saving the Assessment Report<a name="CHAP_AssessmentReport.Save"></a>

You can save a local copy of the database migration assessment report as either a PDF file or a comma\-separated values \(CSV\) file\. The CSV file contains only action item information\. The PDF file contains both the summary and action item information, as shown in the following example\. 

![\[Database migration assessment report\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/assessment_report.png)