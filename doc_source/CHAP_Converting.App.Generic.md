# Converting SQL code in your applications with the AWS SCT<a name="CHAP_Converting.App.Generic"></a>

You can use AWS Schema Conversion Tool \(AWS SCT\) to convert SQL code embedded into your applications\. The generic AWS SCT application converter treats your application code as plain text\. It scans your application code and extracts SQL code with regular expressions\. This converter supports different types of source code files and works with application code that is written in any programming language\.

The generic application converter has the following limitations\. It doesn't dive deep into the application logic that is specific for the programming language of your application\. Also, the generic converter doesn't support SQL statements from different application objects, such as functions, parameters, local variables, and so on\.

To improve your application SQL code conversion, use language\-specific application SQL code converters\. For more information, see [Converting SQL code in C\# applications](CHAP_Converting.App.Csharp.md), [Converting SQL code in Java applications](CHAP_Converting.App.Java.md), and [Converting SQL code in Pro\*C applications](CHAP_Converting.App.ProC.md)\.

## Creating generic application conversion projects in the AWS SCT<a name="CHAP_Converting.App.Project"></a>

In the AWS Schema Conversion Tool, the application conversion project is a child of the database schema conversion project\. Each database schema conversion project can have one or more child application conversion projects\. Use the following procedure to create a generic application conversion project\. 

**To create an application conversion project**

1. In the AWS Schema Conversion Tool, choose **New generic application** on the **Applications** menu\. 

   The **New application conversion project** dialog box appears\.   
![\[The New application conversion project dialog box\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/applications-new-project.png)

1. Add the following project information\.   
****    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/CHAP_Converting.App.Generic.html)

1. Select **Don't cast bind variables to SQL types** to avoid conversion of bind variables types to SQL types\. This option is available only for an Oracle to PostgreSQL conversion\.

   For example, your source application code includes the following Oracle query:

   ```
   SELECT * FROM ACCOUNT WHERE id = ?
   ```

   When you select **Don't cast bind variables to SQL types**, AWS SCT converts this query as shown following\.

   ```
   SELECT * FROM account WHERE id = ?
   ```

   When you clear **Don't cast bind variables to SQL types**, AWS SCT changes the bind variable type to the `NUMERIC` data type\. The conversion result is shown following\.

   ```
   SELECT * FROM account WHERE id = (?)::NUMERIC
   ```

1. Select **Keep object names** to avoid adding the schema name to the name of the converted object\. This option is available only for an Oracle to PostgreSQL conversion\.

   For example, suppose that your source application code includes the following Oracle query\.

   ```
   SELECT * FROM ACCOUNT
   ```

   When you select **Keep object names**, AWS SCT converts this query as shown following\.

   ```
   SELECT * FROM account
   ```

   When you clear **Keep object names**, AWS SCT adds the schema name to the name of the table\. The conversion result is shown following\.

   ```
   SELECT * FROM schema_name.account
   ```

   If your source code includes the names of the parent objects in the names of the objects, AWS SCT uses this format in the converted code\. In this case, ignore the **Keep object names** option because AWS SCT adds the names of the parent objects in the converted code\.

1. Choose **OK** to create your application conversion project\. 

   The project window opens\.  
![\[The project window\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/applications-project-window.png)

## Managing application conversion projects in the AWS SCT<a name="CHAP_Converting.App.Manage"></a>

You can open an existing application conversion project and add multiple application conversion projects\.

After you create an application conversion project, the project window opens automatically\. You can close the application conversion project window and get back to it later\.

**To open an existing application conversion project**

1. In the left panel, choose the application conversion project node, and open the context \(right\-click\) menu\.

1. Choose **Manage application**\.

**To add an additional application conversion project**

1. In the left panel, choose the application conversion project node, and open the context \(right\-click\) menu\.

1. Choose **New application**\.

1. Enter the information that is required to create a new application conversion project\. For more information, see [Creating generic application conversion projects](#CHAP_Converting.App.Project)\.

## Analyzing and converting your SQL code in the AWS SCT<a name="CHAP_Converting.App.Convert"></a>

Use the following procedure to analyze and convert your SQL code in the AWS Schema Conversion Tool\. 

**To analyze and convert your SQL code**

1. Open an existing application conversion project, and choose **Analyze**\. 

   AWS SCT analyzes your application code and extracts the SQL code\. AWS SCT displays the extracted SQL code in the **Parsed SQL scripts** list\. 

1. For **Parsed SQL scripts**, choose an item to review its extracted SQL code\. AWS SCT displays the code of the selected item in the **Extracted SQL script** pane\.

1. Choose **Convert** to convert the SQL code the **Extracted SQL script** pane\. AWS SCT converts the code to a format compatible with your target database\. 

   You can edit the converted SQL code\. For more information, see [Editing and saving your converted SQL code](#CHAP_Converting.App.Edit)\.  
![\[SQL code to analyze\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/applications-project-analyze.png)

1. When you create an application conversion assessment report, AWS SCT converts all extracted SQL code items\. For more information, see [Creating and using the assessment report](#CHAP_Converting.App.AssessmentReport)\. 

## Creating and using the AWS SCT assessment report in the AWS SCT<a name="CHAP_Converting.App.AssessmentReport"></a>

The *application conversion assessment report* provides information about converting the application SQL code to a format compatible with your target database\. The report details all extracted SQL code, all converted SQL code, and action items for SQL code that AWS SCT can't convert\. 

### Creating an application conversion assessment report<a name="CHAP_Converting.App.AssessmentReport.Create"></a>

Use the following procedure to create an application conversion assessment report\.

**To create an application conversion assessment report**

1. In the application conversion project window, choose **Create report** on the **Actions** menu\. 

   AWS SCT creates the application conversion assessment report and opens it in the application conversion project window\. 

1. Review the **Summary** tab\. 

   The **Summary** tab, shown following, displays the summary information from the application assessment report\. It shows the SQL code items that were converted automatically, and items that were not converted automatically\.   
![\[Application Assessment Report summary tab\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/applications-summary.png)

1. Choose **SQL extraction actions**\. 

   Review the list of SQL code items that AWS SCT can't extract from your source code\. 

1. Choose **SQL conversion actions**\. 

   Review the list of SQL code items that AWS SCT can't convert automatically\. Use recommended actions to manually convert the SQL code\. For information about how to edit your converted SQL code, see [Editing and saving your converted SQL code with the AWS SCT](#CHAP_Converting.App.Edit)\. 

1. \(Optional\) Save a local copy of the report as either a PDF file or a comma\-separated values \(CSV\) file:
   + Choose **Save to PDF** at upper right to save the report as a PDF file\.

      The PDF file contains the executive summary, action items, and recommendations for application conversion\.
   + Choose **Save to CSV **at upper right to save the report as a CSV file\.

     The CSV file contains action items, recommended actions, and an estimated complexity of manual effort required to convert the SQL code\.

## Editing and saving your converted SQL code with the AWS SCT<a name="CHAP_Converting.App.Edit"></a>

The assessment report includes a list of SQL code items that AWS SCT can't convert\. For each item, AWS SCT creates an action item on the **SQL conversion actions** tab\. For these items, you can edit the SQL code manually to perform the conversion\. 

Use the following procedure to edit your converted SQL code, apply the changes, and then save them\. 

**To edit, apply changes to, and save your converted SQL code**

1. Edit your converted SQL code directly in the **Target SQL script** pane\. If there is no converted code shown, you can click in the pane and start typing\. 

1. After you are finished editing your converted SQL code, choose **Apply**\. At this point, the changes are saved in memory, but not yet written to your file\. 

1. Choose **Save** to save your changes to your file\. 

   When you choose **Save**, you overwrite your original file\. Make a copy of your original file before saving so you have a record of your original application code\. 