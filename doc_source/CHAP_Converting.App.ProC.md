# Converting SQL code in Pro\*C applications with the AWS SCT<a name="CHAP_Converting.App.ProC"></a>

For an Oracle to PostgreSQL conversion, you can use the AWS Schema Conversion Tool \(AWS SCT\) to convert SQL code embedded into your Pro\*C applications\. This specific Pro\*C application converter understands the application logic\. It collects statements that are located in different application objects, such as functions, parameters, local variables, and so on\. 

Because of this deep analysis, the Pro\*C application SQL code converter provides better conversion results compared the generic converter\. 

## Creating Pro\*C application conversion projects in the AWS SCT<a name="CHAP_Converting.App.ProC.Create"></a>

You can create a Pro\*C application conversion project only for converting Oracle database schemas to PostgreSQL database schemas\. Make sure that you add a mapping rule in your project that includes a source Oracle schema and a target PostgreSQL database\. For more information, see [Creating mapping rules in AWS SCT](CHAP_Mapping.md)\.

You can add multiple application conversion projects in a single AWS SCT project\. Use the following procedure to create a Pro\*C application conversion project\. 

**To create a Pro\*C application conversion project**

1. Create a database conversion project, and add a source Oracle database\. For more information, see [Creating an AWS SCT project](CHAP_UserInterface.md#CHAP_UserInterface.Project) and [Adding database servers to an AWS SCT project](CHAP_UserInterface.md#CHAP_UserInterface.AddServers)\. 

1. Add a mapping rule that includes your source Oracle database and a target PostgreSQL database\. You can add a target PostgreSQL database or use a virtual PostgreSQL target database platform in a mapping rule\. For more information, see [Creating mapping rules in AWS SCT](CHAP_Mapping.md) and [Using virtual targets](CHAP_Mapping.VirtualTargets.md)\. 

1. On the **Applications** menu, choose **New Pro\*C application**\. 

   The **Creating Pro\*C application conversion project** dialog box appears\.   
![\[The new Pro*C application conversion project dialog box\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/proc-application-new-project.png)

1. For **Name**, enter a name for your Pro\*C application conversion project\. Because each database schema conversion project can have one or more child application conversion projects, choose a name that makes sense if you add multiple projects\. 

1. For **Location**, enter the location of the source code for your application\. 

1. In the source tree, choose the schema that your application uses\. Make sure that this schema is part of a mapping rule\. AWS SCT highlights the schemas that are part of a mapping rule in bold\. 

1. Choose **OK** to create your Pro\*C application conversion project\.

1. On the **View** menu, choose **Main view**\.

1. Find your Pro\*C application conversion project in the **Applications** node in the left panel\.

## Managing Pro\*C application conversion projects in the AWS SCT<a name="CHAP_Converting.App.ProC.Manage"></a>

You can add multiple Pro\*C application conversion projects, update the application code in the AWS SCT project, or remove a Pro\*C conversion project from your AWS SCT project\.

**To add an additional Pro\*C application conversion project**

1. Expand the **Applications** node in the left panel\.

1. Choose the **Pro\*C** node, and open the context \(right\-click\) menu\.

1. Choose **New application**\.

1. Enter the information that is required to create a new Pro\*C application conversion project\. For more information, see [Creating Pro\*C application conversion projects](#CHAP_Converting.App.ProC.Create)\.

After you make changes in your source application code, upload it into the AWS SCT project\.

**To upload the updated application code**

1. Expand the **Pro\*C** node under **Applications** in the left panel\.

1. Choose the application to update, and open the context \(right\-click\) menu\.

1. Choose **Refresh** and then choose **Yes**\.

   AWS SCT uploads your application code from the source files and removes conversion results\. To keep code changes that you made in AWS SCT and the conversion results, create a new Pro\*C conversion project\.

**To remove a Pro\*C application conversion project**

1. Expand the **Pro\*C** node under **Applications** in the left panel\.

1. Choose the application to remove, and open the context \(right\-click\) menu\.

1. Choose **Delete** and then choose **OK**\.

## Converting your Pro\*C application SQL code in the AWS SCT<a name="CHAP_Converting.App.ProC.Convert"></a>

After you add your Pro\*C application to the AWS SCT project, convert SQL code from this application to a format compatible with your target database platform\. Use the following procedure to analyze and convert the SQL code embedded in your Pro\*C application in the AWS Schema Conversion Tool\. 

**To convert your SQL code**

1. Expand the **Pro\*C** node under **Applications** in the left panel\.

1. Choose the application to convert and then choose **Settings**\.

   1. For **Global header file path**, enter the path to the header files that your application project uses\.

   1. Choose **Interpret all unresolved host variables as** to see all unresolved variables in the converted code\.

   1. Choose **Use fixed\-width string conversion function from the extension pack** to use the extension pack functions in the converted SQL code\. AWS SCT includes the extension pack files in your application project\.

   1. Choose **Transform anonymous PL/SQL blocks to standalone SQL calls or stored functions** to create stored procedures in your target database for all anonymous PL/SQL blocks\. AWS SCT then includes the runs of these stored procedures in the converted application code\.

   1. Choose **Use custom cursor flow** to improve the conversion of Oracle database cursors\.

1. In the left panel, choose the application to convert, and open the context \(right\-click\) menu\.

1.  Choose **Convert**\. AWS SCT analyzes your source code files, determines the application logic, and loads code metadata into the project\. This code metadata includes Pro\*C classes, objects, methods, global variables, interfaces, and so on\. 

   In the target database panel, AWS SCT creates the similar folders structure to your source application project\. Here you can review the converted application code\.  
![\[SQL code to analyze\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/proc-applications-project-analyze.png)

1. Save your converted application code\. For more information, see [Editing and saving your converted application code](#CHAP_Converting.App.ProC.Save)\.

## Creating a Pro\*C application conversion assessment report in the AWS SCT<a name="CHAP_Converting.App.ProC.AssessmentReport"></a>

The *Pro\*C application conversion assessment report* provides information about converting the SQL code embedded in your Pro\*C application to a format compatible with your target database\. The assessment report provides conversion details for all SQL execution points and all source code files\. The assessment report also includes action items for SQL code that AWS SCT can't convert\. 

Use the following procedure to create a Pro\*C application conversion assessment report\.

**To create a Pro\*C application conversion assessment report**

1. Expand the **Pro\*C** node under **Applications** in the left panel\.

1. Choose the application to convert, and open the context \(right\-click\) menu\.

1. Choose **Convert**\.

1. On the **View** menu, choose **Assessment report view**\.

1. Review the **Summary** tab\.

   The **Summary** tab, shown following, displays the executive summary information from the Pro\*C application assessment report\. It shows conversion results for all SQL execution points and all source code files\.   
![\[Pro*C Application Assessment Report summary tab\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/proc-applications-summary.png)

1. Choose **Save statements to CSV** to save the extracted SQL code from your Pro\*C application as a comma\-separated values \(CSV\) file\.

1. \(Optional\) Save a local copy of the report as either a PDF file or a comma\-separated values \(CSV\) file:
   + Choose **Save to PDF** at upper right to save the report as a PDF file\.

      The PDF file contains the executive summary, action items, and recommendations for application conversion\.
   + Choose **Save to CSV **at upper right to save the report as a CSV file\.

     The CSV file contains action items, recommended actions, and an estimated complexity of manual effort required to convert the SQL code\.

## Editing and saving your converted application code with the AWS SCT<a name="CHAP_Converting.App.ProC.Save"></a>

You can edit the converted SQL statements and use AWS SCT to embed this edited code into the converted Pro\*C application code\. Use the following procedure to edit your converted SQL code\.

**To edit your converted SQL code**

1. Expand the **Pro\*C** node under **Applications** in the left panel\.

1. Choose the application to convert, open the context \(right\-click\) menu, and choose **Convert**\.

1. On the **View** menu, choose **Assessment report view**\.

1. Choose **Save statements to CSV** to save the extracted SQL code from your Pro\*C application as a CSV file\.

1. Enter the name of the CSV file to save the extracted SQL code, and choose **Save**\.

1. Edit the extracted SQL code\.

1. On the **View** menu, choose **Main view**\.

1. Expand the **Pro\*C** node under **Applications** in the target database panel\.

1. Choose your converted application, open the context \(right\-click\) menu, and choose **Import statements from CSV**\.

1. Choose **Yes**, then choose the file with your edited SQL code, and choose **Open**\.

AWS SCT breaks the converted SQL statements into parts and places them into the appropriate objects of your source application code\. Use the following procedure to save your converted application code\.

**To save your converted application code**

1. Expand the **Pro\*C** node under **Applications** in the target database panel\.

1. Choose your converted application, and choose **Save**\.

1. Enter the path to the folder to save the converted application code, and choose **Select folder**\.