# Converting SQL code in C\+\+ applications with AWS SCT<a name="CHAP_Converting.App.Cplusplus"></a>

For an Oracle to PostgreSQL conversion, you can use AWS SCT to convert SQL code embedded into your C\+\+ applications\. This specific C\+\+ application converter understands the application logic\. It collects statements that are located in different application objects, such as functions, parameters, local variables, and so on\. 

Because of this deep analysis, the C\+\+ application SQL code converter provides better conversion results than the generic converter\. 

## Creating C\+\+ application conversion projects in AWS SCT<a name="CHAP_Converting.App.Cplusplus.Create"></a>

You can create a C\+\+ application conversion project only for converting Oracle database schemas to PostgreSQL database schemas\. Make sure that you add a mapping rule in your project that includes a source Oracle schema and a target PostgreSQL database\. For more information, see [Creating mapping rules in AWS SCT](CHAP_Mapping.md)\. 

You can add multiple application conversion projects in a single AWS SCT project\.

**To create a C\+\+ application conversion project**

1. Create a database conversion project, and add a source Oracle database\. For more information, see [Creating an AWS SCT project](CHAP_UserInterface.md#CHAP_UserInterface.Project) and [Adding database servers to an AWS SCT project](CHAP_UserInterface.md#CHAP_UserInterface.AddServers)\. 

1. Add a mapping rule that includes your source Oracle database and a target PostgreSQL database\. You can add a target PostgreSQL database or use a virtual PostgreSQL target database platform in a mapping rule\. For more information, see [Creating mapping rules in AWS SCT](CHAP_Mapping.md) and [Using virtual targets](CHAP_Mapping.VirtualTargets.md)\. 

1. On the **View** menu, choose **Main view**\.

1. On the **Applications** menu, choose **New C\+\+ application**\. 

   The **Creating a C\+\+ application conversion project** dialog box appears\.   
![\[The new C++ application conversion project dialog box\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/cplusplus-application-new-project.png)

1. For **Name**, enter a name for your C\+\+ application conversion project\. Because each database schema conversion project can have one or more child application conversion projects, choose a name that makes sense if you add multiple projects\. 

1. For **Location**, enter the location of the source code for your application\. 

1. In the source tree, choose the schema that your application uses\. Make sure that this schema is part of a mapping rule\. AWS SCT highlights the schemas that are part of a mapping rule in bold\. 

1. Choose **OK** to create your C\+\+ application conversion project\.

1. Find your C\+\+ application conversion project in the **Applications** node in the left panel\.

## Converting your C\+\+ application SQL code in AWS SCT<a name="CHAP_Converting.App.Cplusplus.Convert"></a>

After you add your C\+\+ application to the AWS SCT project, convert SQL code from this application to a format compatible with your target database platform\. Use the following procedure to analyze and convert the SQL code embedded in your C\+\+ application in AWS SCT\. 

**To convert your SQL code**

1. Expand the **C\+\+** node under **Applications** in the left panel, and choose the application to convert\.

1. In the **Source Oracle application project**, choose **Settings**\. Review and edit the conversion settings for the selected C\+\+ application\. You can also specify the conversion settings for all C\+\+ applications that you added to your AWS SCT project\. For more information, see [Managing C\+\+ application conversion projects](#CHAP_Converting.App.Cplusplus.Manage)\.

1. For **Compiler type**, choose the compiler that you use for the source code of your C\+\+ application\. AWS SCT supports the following C\+\+ compilers: **Microsoft Visual C\+\+**, **GCC, the GNU Compiler Collection**, and **Clang**\. The default option is **Microsoft Visual C\+\+**\.

1. For **User\-defined macros**, enter the path to the file that includes user\-defined macros from your C\+\+ project\. Make sure that this file has the following structure: `#define name value`\. In the preceding example, `value` is an optional parameter\. The default value for this optional parameter is `1`\.

   To create this file, open your project in Microsoft Visual Studio, and then choose **Project**, **Properties**, **C/C\+\+**, and **Preprocessor**\. For **Preprocessor definitions**, choose **Edit** and copy names and values to a new text file\. Then, for each string in the file, add the following prefix: `#define `\.

1. For **External include directories**, enter the paths to the folders that include external libraries that you use in your C\+\+ project\.

1. In the left pane, choose the application to convert, and open the context \(right\-click\) menu\.

1.  Choose **Convert**\. AWS SCT analyzes your source code files, determines the application logic, and loads code metadata into the project\. This code metadata includes C\+\+ classes, objects, methods, global variables, interfaces, and so on\. 

   In the target database panel, AWS SCT creates the similar folders structure to your source application project\. Here you can review the converted application code, as shown following\.  
![\[SQL code to analyze\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/cplusplus-applications-project-analyze.png)

1. Save your converted application code\. For more information, see [Saving your converted application code](#CHAP_Converting.App.Cplusplus.Save)\.

## Saving your converted application code with AWS SCT<a name="CHAP_Converting.App.Cplusplus.Save"></a>

Use the following procedure to save your converted application code\. 

**To save your converted application code**

1. Expand the **C\+\+** node under **Applications** in the target database panel\.

1. Choose your converted application, and choose **Save**\.

1. Enter the path to the folder to save the converted application code, and choose **Select folder**\.

## Managing C\+\+ application conversion projects in AWS SCT<a name="CHAP_Converting.App.Cplusplus.Manage"></a>

You can add multiple C\+\+ application conversion projects, edit conversion settings, update the C\+\+ application code, or remove a C\+\+ conversion project from your AWS SCT project\.

**To add an additional C\+\+ application conversion project**

1. Expand the **Applications** node in the left panel\.

1. Choose the **C\+\+** node, and open the context \(right\-click\) menu\.

1. Choose **New application**\.

1. Enter the information that is required to create a new C\+\+ application conversion project\. For more information, see [Creating C\+\+ application conversion projects](#CHAP_Converting.App.Cplusplus.Create)\.

You can specify conversion settings for all C\+\+ application conversion projects in your AWS SCT project\.

**To edit conversion settings for all C\+\+ applications**

1. On the **Settings** menu, choose **Project settings**, and then choose **Application conversion**\.

1. For **Compiler type**, choose the compiler that you use for the source code of your C\+\+ application\. AWS SCT supports the following C\+\+ compilers: **Microsoft Visual C\+\+**, **GCC, the GNU Compiler Collection**, and **Clang **\. The default option is **Microsoft Visual C\+\+**\.

1. For **User\-defined macros**, enter the path to the file that includes user\-defined macros from your C\+\+ project\. Make sure that this file has the following structure: `#define name value`\. In the preceding example, `value` is an optional parameter\. The default value for this optional parameter is `1`\.

   To create this file, open your project in Microsoft Visual Studio, and then choose **Project**, **Properties**, **C/C\+\+**, and **Preprocessor**\. For **Preprocessor definitions**, choose **Edit** and copy names and values to a new text file\. Then, for each string in the file, add the following prefix: `#define `\.

1. For **External include directories**, enter the paths to the folders that include external libraries that you use in your C\+\+ project\.

1. Choose **OK** to save the project settings and close the window\.

Or you can specify conversion settings for each C\+\+ application conversion project\. For more information, see [Converting your C\+\+ application SQL code](#CHAP_Converting.App.Cplusplus.Convert)\.

After you make changes in your source application code, upload it into the AWS SCT project\.

**To upload the updated application code**

1. Expand the **C\+\+** node under **Applications** in the left panel\.

1. Choose the application to update, and open the context \(right\-click\) menu\.

1. Choose **Refresh** and then choose **Yes**\.

   AWS SCT uploads your application code from the source files and removes conversion results\. To keep code changes that you made in AWS SCT and the conversion results, create a new C\+\+ conversion project\.

   Also, AWS SCT removes the application conversion settings that you specified for the selected application\. After you upload the updated application code, AWS SCT applies the default values from the project settings\.

**To remove a C\+\+ application conversion project**

1. Expand the **C\+\+** node under **Applications** in the left panel\.

1. Choose the application to remove, and open the context \(right\-click\) menu\.

1. Choose **Delete** and then choose **OK**\.

## Creating a C\+\+ application conversion assessment report in AWS SCT<a name="CHAP_Converting.App.Cplusplus.AssessmentReport"></a>

The *C\+\+ application conversion assessment report* provides information about converting the SQL code embedded in your C\+\+ application to a format compatible with your target database\. The assessment report provides conversion details for all SQL execution points and all source code files\. The assessment report also includes action items for SQL code that AWS SCT can't convert\. 

**To create a C\+\+ application conversion assessment report**

1. Expand the **C\+\+** node under **Applications** in the left panel\.

1. Choose the application to convert, and open the context \(right\-click\) menu\.

1. Choose **Convert**\.

1. On the **View** menu, choose **Assessment report view**\.

1. View the **Summary** tab\.

   The **Summary** tab displays the executive summary information from the C\+\+ application assessment report\. It shows conversion results for all SQL execution points and all source code files\. 

1. Choose **Save statements to JSON** to save the extracted SQL code from your Java application as a JSON file\.

1. \(Optional\) Save a local copy of the report as either a PDF file or a comma\-separated values \(CSV\) file:
   + Choose **Save to PDF** at upper right to save the report as a PDF file\.

      The PDF file contains the executive summary, action items, and recommendations for application conversion\.
   + Choose **Save to CSV **at upper right to save the report as a CSV file\.

     The CSV file contains action items, recommended actions, and an estimated complexity of manual effort required to convert the SQL code\.