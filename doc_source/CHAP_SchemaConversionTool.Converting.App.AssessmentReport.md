# Creating and Using the Assessment Report<a name="CHAP_SchemaConversionTool.Converting.App.AssessmentReport"></a>

The *application assessment report* provides important information about converting the application SQL code from your source database schema to your target database schema\. The report details all of the SQL extracted from the application, all of the SQL converted, and action items for SQL that can't be converted\. The report also includes estimates of the amount of effort that it will take to manually convert the SQL code that can't be converted automatically\. 

## Creating an Application Assessment Report<a name="CHAP_SchemaConversionTool.Converting.App.AssessmentReport.Create"></a>

Use the following procedure to create an application assessment report\.

**To create an application assessment report**

1. In the application conversion project window, choose **Create Report** from the **Actions** menu\. 

   The report is created and opens in the application conversion project window\. 

1. Review the **Summary** tab\. 

   The **Summary** tab shown following, displays the summary information from the application assessment report\. It shows the SQL code items that were converted automatically, and items that were not converted automatically\.   
![\[Application Assessment Report summary tab\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/applications-summary.png)

1. Choose the **SQL Conversion Actions** tab and review the information\. 

   The **SQL Conversion Actions** tab contains a list of SQL code items that can't be converted automatically\. There are also recommendations for how to manually convert the SQL code\. You edit your converted SQL code in a later step\. For more information, see [Editing and Saving Your Converted SQL Code with the AWS Schema Conversion Tool](CHAP_SchemaConversionTool.Converting.App.Edit.md)\.   
![\[SQL Conversion Actions tab\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/applications-actions.png)

1. You can save a local copy of the application assessment report as either a PDF file or a comma\-separated values \(CSV\) file\. The PDF file contains both the summary and action item information\. The CSV file contains only action item information\. 