# Using the AWS Schema Conversion Tool \(AWS SCT\) User Interface<a name="CHAP_UserInterface"></a>

The following sections help you work with the AWS SCT user interface\. For information on installing AWS SCT, see [Installing, Verifying, and Updating the AWS Schema Conversion Tool \(AWS SCT\)](CHAP_Installing.md)\.

**Topics**
+ [The AWS SCT Project Window](#CHAP_UserInterface.Overview.ProjectWindow)
+ [Using AWS Service Profiles in the AWS Schema Conversion Tool](#CHAP_UserInterface.Profiles)
+ [Storing Database Passwords](#CHAP_UserInterface.StoringPasswords)
+ [Using the Union All View for Projects with Partitioned Tables](#CHAP_UserInterface.UnionAllView)
+ [Using AWS SCT Tree Filters](#CHAP_UserInterface.TreeFilters)
+ [Hiding Schemas in the AWS SCT Tree View](#CHAP_UserInterface.HidingSchemas)
+ [Keyboard Shortcuts for the AWS SCT](#CHAP_UserInterface.KeyboardShortcuts)
+ [Creating and Reviewing the Database Migration Assessment Report](#CHAP_UserInterface.AssessmentReport)
+ [Starting the AWS Schema Conversion Tool](#CHAP_UserInterface.Launching)
+ [Creating an AWS Schema Conversion Tool Project](#CHAP_UserInterface.Project)
+ [Converting Your Schema](#CHAP_UserInterface.Converting)
+ [Applying the Converted Schema to Your Target DB Instance](#CHAP_UserInterface.ApplyingConversion)

## The AWS SCT Project Window<a name="CHAP_UserInterface.Overview.ProjectWindow"></a>

The illustration following is what you see in the AWS SCT when you create a schema migration project, and then convert a schema\. 

1. In the left panel, the schema from your source database is presented in a tree view\. Your database schema is "lazy loaded\." In other words, when you select an item from the tree view, AWS SCT gets and displays the current schema from your source database\. 

1. In the top middle panel, action items appear for schema elements from the source database engine that couldn't be converted automatically to the target database engine\. 

1. In the right panel, the schema from your target DB instance is presented in a tree view\. Your database schema is "lazy loaded\." That is, at the point when you select an item from the tree view, AWS SCT gets and displays the current schema from your target database\. 

![\[The AWS SCT Project Window\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/AWS_Migration_Tool.png)

1. In the lower left panel, when you choose a schema element, properties describing the source schema element and the SQL command to create that element in the source database are displayed\. 

1. In the lower right panel, when you choose a schema element, properties describing the target schema element and the SQL command to create that element in the target database are displayed\. You can edit this SQL command and save the updated command with your project\. 

## Using AWS Service Profiles in the AWS Schema Conversion Tool<a name="CHAP_UserInterface.Profiles"></a>

You can store your AWS credentials in the AWS Schema Conversion Tool \(AWS SCT\)\. AWS SCT uses your credentials when you use features that integrate with AWS services\. For example, AWS SCT integrates with Amazon S3, AWS Lambda, Amazon Relational Database Service, and AWS Database Migration Service\. 

AWS SCT asks you for your AWS credentials when you access a feature that requires them\. You can store your credentials in the global application settings\. When AWS SCT asks for your credentials, you can select the stored credentials\. 

You can store different sets of AWS credentials in the global application settings\. For example, you can store one set of credentials that you use in test scenarios, and a different set of credentials that you use in production scenarios\. You can also store different credentials for different AWS Regions\. 

### Storing AWS Credentials<a name="CHAP_UserInterface.Profiles.Storing"></a>

Use the following procedure to store AWS credentials globally\. 

**To store AWS credentials**

1. Start the AWS Schema Conversion Tool\.

1. Open the **Settings Menu**, and then choose **Global Settings**\. The **Global Settings** dialog box appears\. 

   Choose **AWS Service Profiles**, as shown following\.   
![\[The Global Settings dialog box with the AWS Service Profiles tab selected\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/AWSServiceProfileSettings.png)

1. Choose **Add new AWS Service Profile**\. 

1. Enter your AWS information as follows\.     
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/CHAP_UserInterface.html)

   1. For **Profile name**, type a name for your profile\. 

   1. For **AWS Access Key**, type your AWS access key\. 

   1. For **AWS Secret Key**, type your AWS secret key\. 

   1. For **Region**, choose the region for your profile\. 

   1. For **S3 Bucket**, choose the Amazon S3 bucket for your profile\. You need to specify a bucket only if you are using a feature that connects to S3\. 

   1. Choose **Use FIPS endpoint for S3** if you need to comply with the security requirements for the Federal Information Processing Standard \(FIPS\)\. FIPS endpoints are available in the following AWS Regions: 
      + US East \(N\. Virginia\) Region
      + US East \(Ohio\) Region
      + US West \(N\. California\) Region
      + US West \(Oregon\) Region

1. Choose **Test Connection** to verify that your credentials are correct and active\. 

   The **Test Connection** dialog box appears\. You can see the status for each of the services connected to your profile\. **Pass** indicates that the profile can successfully access the service\.   
![\[The Global Settings dialog box with the AWS Service Profiles tab selected\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/AWSServiceProfileSettings-Test.png)

1. After you have configured your profile, choose **Save** to save your profile or **Cancel** to cancel your changes\. 

1. Choose **OK** to close the **Global Settings** dialog box\. 

### Setting the Default Profile for a Project<a name="CHAP_UserInterface.Profiles.Project"></a>

You can set the default profile for an AWS SCT project\. Doing this associates the AWS credentials stored in the profile with the project\. With your project open, use the following procedure to set the default profile\. 

**To set the default profile for a project**

1. Start the AWS Schema Conversion Tool\.

1. Open the **Settings Menu**, and then choose **Project Settings**\. The **Current project settings** dialog box appears\. 

1. Choose the **Project Environment** tab\. 

1. For **AWS Service Profile**, choose the profile that you want to associate with the project\. 

1. Choose **OK** to close the **Current project settings** dialog box\. You can also choose **Cancel** to cancel your changes\. 

## Storing Database Passwords<a name="CHAP_UserInterface.StoringPasswords"></a>

You can store a database password or SSL certificate in the AWS SCT cache\. To store a password, choose **Store Password** when you create a connection\. 

The password is encrypted using the randomly generated token in the `seed.dat` file\. The password is then stored with the user name in the cache file\. If you lose the `seed.dat` file or it becomes corrupted, the database password might be unencrypted incorrectly\. In this case, the connection fails\. 

## Using the Union All View for Projects with Partitioned Tables<a name="CHAP_UserInterface.UnionAllView"></a>

If a source table is partitioned, AWS SCT creates *n* target tables, where *n* is the number of partitions on the source table\. AWS SCT creates a UNION ALL view on top of the target tables to represent the source table\. If you use an AWS SCT data extractor to migrate your data, the source table partitions will be extracted and loaded in parallel by separate subtasks\.

**To use Union All view for a project**

1. Start AWS SCT\. Choose a data warehouse \(OLAP\) project\.

1. Choose **Settings**, and then choose **Project settings**\. The **Current project settings** dialog box appears\. 

1. Choose **Use Union all view**\. 

1. Choose **OK** to save the settings and close the **Current project settings** dialog box\. 

## Using AWS SCT Tree Filters<a name="CHAP_UserInterface.TreeFilters"></a>

To migrate data from a source to a target, AWS SCT loads all metadata from source and target databases into a tree structure\. This structure appears in AWS SCT as the tree view in the main project window\. 

Some databases can have a large number of objects in the tree structure\. You can use *tree filters* in AWS SCT to search for objects in the source and target tree structures\. When you use a tree filter, you don't change the objects that are converted when you convert your database\. The filter only changes what you see in the tree\.

Tree filters work with objects that AWS SCT has preloaded\. In other words, AWS SCT doesn't load objects from the database during searches\. This approach means that the tree structure generally contains fewer objects than are present in the database\.

For tree filters, keep the following in mind:
+ The filter default is ANY, which means that the filter uses a name search to find objects\.
+ When you select one or more object types, you see only those types of objects in the tree\.
+ You can use the filter mask to show different types of symbols, including Unicode, spaces, and special characters\. The “%” character is the wildcard for any symbol\.
+ After you apply a filter, the count shows only the number of filtered objects\.

### <a name="CHAP_UserInterface.UI.TreeFilters.Console"></a>

**To create a tree filter**

1. Open an existing AWS SCT project\.

1. Connect to the database you want to apply the tree filter to\.

1. Choose the filter icon\.
**Note**  
 The undo filter icon is grayed out because no filter is currently applied\.  
![\[The filter icon for the schema tree\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/filter-source-tree.png)

1. Enter the following information in the **Tree Filter** dialog box\. Options in the dialog box are different for each database engine\.  
![\[The filter icon for the schema tree\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/filter-tree-db.png)    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/CHAP_UserInterface.html)

1. Choose **Apply**\. After you choose **Apply**, the undo filter icon \(next to the filter icon\) is enabled\. Use this icon if you want to remove the filters you applied\.

1. Choose **Close** to close the dialog box\.

When you filter the schema that appears in the tree, you don't change the objects that are converted when you convert your schema\. The filter only changes what you see in the tree\. 

### Importing a File List for the Tree Filter<a name="CHAP_UserInterface.UI.TreeFilters.ImportingFileList"></a>

You can import a file that contains names or values that you want the tree filter to use\. In this file, the following convention is used:
+ `Object` is the type of object that you want to find\. 
+ `Database` is the name of database where this object exists\.
+ `Schema` is the name of schema where this object exists\.
+ `Name` is the object name\. 

The file to import should have the following format:
+ `Object;Database;Schema;Name` – This format is mandatory for the Microsoft SQL Server, SQL Data Warehouse, and Netezza dialects of SQL\.
+ `Object;Schema;Name` – Use this format for other SQL dialects\.

**To import a file list for the tree filter**

1. Open an existing AWS SCT project, connect to the database you want to apply the tree filter to, and then choose the filter icon\.  
![\[The filter icon for the schema tree\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/filter-source-tree.png)

1. Choose the **Import File List** tab\.

1. Choose **Import File**\.

1. Choose a file to import, and then choose **Open**\.

1. Choose **Apply**, and then choose **Close**\.

## Hiding Schemas in the AWS SCT Tree View<a name="CHAP_UserInterface.HidingSchemas"></a>

By using tree view settings, you specify what schemas and databases you want to see in the AWS SCT tree view\. You can hide empty schemas, empty databases, system databases, and user\-defined databases and schemas\. 

**To hide databases and schemas in tree view**

1. Open an AWS SCT project\.

1. Connect to the data store that you want to show in tree view\.

1. Choose **Settings**, **Global Settings**, **Tree View**\.  
![\[The Tree View Settings section of the Global Settings dialog box\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/treeview-hide.png)

1. In the **Tree View Settings** section, do the following:
   + For **Hide System Databases/Schemas**, choose system databases and schemas by name to hide them\. 
   + For **Hide User Defined Databases/Schemas**, type the names of user\-defined schemas and databases that you want to hide, and then choose **Add**\. The names are case insensitive\.
   + Choose **Reset to Default** to reset the tree view to default settings\.

1. Choose **OK**\.

## Keyboard Shortcuts for the AWS SCT<a name="CHAP_UserInterface.KeyboardShortcuts"></a>

The following are the keyboard shortcuts that you can use with the AWS SCT\. 


****  

| Keyboard Shortcut | Description | 
| --- | --- | 
| Ctrl\+N | Create a new project\. | 
| Ctrl\+O | Open an existing project\. | 
| Ctrl\+S | Save an open project\. | 
| Ctrl\+W | Create a new project by using the wizard\. | 
| Ctrl\+L | Connect to the source database\. | 
| Ctrl\+R | Connect to the target database\. | 

## Creating and Reviewing the Database Migration Assessment Report<a name="CHAP_UserInterface.AssessmentReport"></a>

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

## Starting the AWS Schema Conversion Tool<a name="CHAP_UserInterface.Launching"></a>

To start the AWS Schema Conversion Tool, use the instructions for your operating system shown following\. 


****  

| Operating System | Instructions | 
| --- | --- | 
| Fedora Linux |  Run the following command:  `/opt/AWSSchemaConversionTool/AWSSchemaConversionTool`  | 
| Microsoft Windows | Double\-click the icon for the application\. | 
| Ubuntu Linux |  Run the following command:  `/opt/AWSSchemaConversionTool/AWSSchemaConversionTool`  | 

## Creating an AWS Schema Conversion Tool Project<a name="CHAP_UserInterface.Project"></a>

The following procedure shows you how to create an AWS Schema Conversion Tool project\. 

**To create your project**

1. Start the AWS Schema Conversion Tool\.

1. Choose **New Project** from the **File** menu\. The **New Project** dialog box appears\.   
![\[New Project dialog box\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/file-new-project.png)

1. Add the following preliminary project information\.   
****    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/CHAP_UserInterface.html)

1. Choose **OK** to create your AWS SCT project\. 

## Converting Your Schema<a name="CHAP_UserInterface.Converting"></a>

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

## Applying the Converted Schema to Your Target DB Instance<a name="CHAP_UserInterface.ApplyingConversion"></a>

You can apply the converted database schema to your target Amazon RDS DB instance\. After the schema has been applied to your target DB instance, you can update the schema based on the action items in the database migration assessment report\. 

**Warning**  
This procedure overwrites the existing target schema\. Be careful not to overwrite schema unintentionally\. Be careful not to overwrite schema in your target DB instance that you have already modified, or you will overwrite those changes\. 

**To apply the converted database schema to your target Amazon RDS DB instance**

1. Choose the schema element in the right panel of your project that displays the planned schema for your target DB instance\. 

1. Open the context \(right\-click\) menu for the schema element, and then choose **Apply to database**\.   
![\[Apply to database\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/write_to_database.png)

   The converted schema is applied to the target DB instance\.