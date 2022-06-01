# Converting application SQL using AWS SCT<a name="CHAP_Converting.App"></a>

When you convert your database schema from one engine to another, you also need to update the SQL code in your applications to interact with the new database engine instead of the old one\. You can view, analyze, edit, and save the converted SQL code\.

You can use the AWS Schema Conversion Tool \(AWS SCT\) to convert the SQL code in your C\+\+, C\#, Java, or other application code\. For an Oracle to PostgreSQL conversion, you can use AWS SCT to convert SQL\*Plus code to PSQL\. Also, for an Oracle to PostgreSQL conversion, you can use AWS SCT to convert SQL code embedded into C\#, C\+\+, Java, and Pro\*C applications\.

**Topics**
+ [Overview of converting application SQL](#CHAP_Converting.App.Overview)
+ [Converting SQL code in your applications with AWS SCT](CHAP_Converting.App.Generic.md)
+ [Converting SQL code in C\# applications with AWS SCT](CHAP_Converting.App.Csharp.md)
+ [Converting SQL code in C\+\+ applications with AWS SCT](CHAP_Converting.App.Cplusplus.md)
+ [Converting SQL code in Java applications with AWS SCT](CHAP_Converting.App.Java.md)
+ [Converting SQL code in Pro\*C applications with AWS SCT](CHAP_Converting.App.ProC.md)

## Overview of converting application SQL<a name="CHAP_Converting.App.Overview"></a>

To convert the SQL code in your application, take the following high\-level steps: 
+ **Create an application conversion project** – The application conversion project is a child of the database schema conversion project\. Each database schema conversion project can have one or more child application conversion projects\. For more information, see [Creating generic application conversion projects in AWS SCT](CHAP_Converting.App.Generic.md#CHAP_Converting.App.Project)\. 
+ **Analyze and convert your SQL code** – AWS SCT analyzes your application, extracts the SQL code, and creates a local version of the converted SQL for you to review and edit\. The tool doesn't change the code in your application until you are ready\. For more information, see [Analyzing and converting your SQL code in AWS SCT](CHAP_Converting.App.Generic.md#CHAP_Converting.App.Convert)\. 
+ **Create an application assessment report** – The application assessment report provides important information about the conversion of the application SQL code from your source database schema to your target database schema\. For more information, see [Creating and using the AWS SCT assessment report in AWS SCT](CHAP_Converting.App.Generic.md#CHAP_Converting.App.AssessmentReport)\. 
+ **Edit, apply changes to, and save your converted SQL code** – The assessment report includes a list of SQL code items that can't be converted automatically\. For these items, you can edit the SQL code manually to perform the conversion\. For more information, see [Editing and saving your converted SQL code with AWS SCT](CHAP_Converting.App.Generic.md#CHAP_Converting.App.Edit)\. 