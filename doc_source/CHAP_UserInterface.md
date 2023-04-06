# Using the AWS SCT user interface<a name="CHAP_UserInterface"></a>

Use the following topics to help you work with the AWS SCT user interface\. For information on installing AWS SCT, see [Installing, verifying, and updating AWS SCT](CHAP_Installing.md)\.

**Topics**
+ [The AWS SCT project window](#CHAP_UserInterface.Overview.ProjectWindow)
+ [Starting AWS SCT](#CHAP_UserInterface.Launching)
+ [Creating an AWS SCT project](#CHAP_UserInterface.Project)
+ [Using a new project wizard in AWS SCT](#CHAP_UserInterface.Wizard)
+ [Saving and opening an AWS SCT project](#CHAP_UserInterface.SaveProject)
+ [Adding database servers to an AWS SCT project](#CHAP_UserInterface.AddServers)
+ [Running AWS SCT in an offline mode](#CHAP_UserInterface.OfflineMode)
+ [Using AWS SCT tree filters](#CHAP_UserInterface.TreeFilters)
+ [Hiding schemas in the AWS SCT tree view](#CHAP_UserInterface.HidingSchemas)
+ [Creating and reviewing the database migration assessment report](#CHAP_UserInterface.AssessmentReport)
+ [Converting your schema](#CHAP_UserInterface.Converting)
+ [Applying the converted schema to your target DB instance](#CHAP_UserInterface.ApplyingConversion)
+ [Storing AWS service profiles in AWS SCT](#CHAP_UserInterface.Profiles)
+ [Using AWS Secrets Manager](#CHAP_UserInterface.SecretsManager)
+ [Storing database passwords](#CHAP_UserInterface.StoringPasswords)
+ [Using the UNION ALL view for projects with partitioned tables](#CHAP_UserInterface.UnionAllView)
+ [Keyboard shortcuts for AWS SCT](#CHAP_UserInterface.KeyboardShortcuts)

## The AWS SCT project window<a name="CHAP_UserInterface.Overview.ProjectWindow"></a>

The illustration following is what you see in AWS SCT when you create a schema migration project, and then convert a schema\. 

1. In the left panel, the schema from your source database is presented in a tree view\. Your database schema is "lazy loaded\." In other words, when you select an item from the tree view, AWS SCT gets and displays the current schema from your source database\. 

1. In the top middle panel, action items appear for schema elements from the source database engine that couldn't be converted automatically to the target database engine\. 

1. In the right panel, the schema from your target DB instance is presented in a tree view\. Your database schema is "lazy loaded\." That is, at the point when you select an item from the tree view, AWS SCT gets and displays the current schema from your target database\. 

![\[The AWS SCT Project Window\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/AWS_Migration_Tool.png)

1. In the lower left panel, when you choose a schema element, properties are displayed\. These describe the source schema element and the SQL command to create that element in the source database\. 

1. In the lower right panel, when you choose a schema element, properties are displayed\. These describe the target schema element and the SQL command to create that element in the target database\. You can edit this SQL command and save the updated command with your project\. 

## Starting AWS SCT<a name="CHAP_UserInterface.Launching"></a>

To start the AWS Schema Conversion Tool, double\-click the application icon\.

## Creating an AWS SCT project<a name="CHAP_UserInterface.Project"></a>

Use the following procedure to create an AWS Schema Conversion Tool project\.

**To create your project**

1. Start the AWS Schema Conversion Tool\.

1. On the **File** menu, choose **New project**\. The **New project** dialog box appears\.   
![\[New Project dialog box\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/file-new-project.png)

1.  Enter a name for your project, which is stored locally on your computer\. 

1.  Enter the location for your local project file\. 

1. Choose **OK** to create your AWS SCT project\. 

1. Choose **Add source** to add a new source database to your AWS SCT project\. You can add multiple source databases to your AWS SCT project\. 

1. Choose **Add target** to add a new target platform in your AWS SCT project\. You can add multiple target platforms to your AWS SCT project\. 

1. Choose the source database schema in the left panel\. 

1. In the right panel, specify the target database platform for the selected source schema\. 

1. Choose **Create mapping**\. This button becomes active after you choose the source database schema and the target database platform\. For more information, see [Creating mapping rules](CHAP_Mapping.md)\.

 Now, your AWS SCT project is set up\. You can save your project, create database migration assessment report, and convert your source database schemas\. 

## Using a new project wizard in AWS SCT<a name="CHAP_UserInterface.Wizard"></a>

You can create a new database migration project using the new project wizard\. This wizard assists you in determining your migration target and connecting to your databases\. It estimates how complex a migration might be for all supported target destinations\. After you run the wizard, AWS SCT produces a summary report for the migration of your database to different target destinations\. You can use this report to compare possible target destinations and choose the optimal migration path\.

**To run the new project wizard**

1. Choose your source database\.

   1. Start the AWS Schema Conversion Tool\.

   1. On the **File** menu, choose **New project wizard**\. The **Create a new database migration project** dialog box opens\. 

   1. To enter the source database connection information, use the following instructions:    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/CHAP_UserInterface.html)

   1. Choose **Next**\. The **Connect to the source database** page opens\.

1. Connect to your source database\.

   1. Provide your connection information for the source database\. The connection parameters depend on your source database engine\. Make sure the user that you use for the analysis of your source database has the applicable permissions\. For more information, see [Sources for AWS SCT](CHAP_Source.md)\.

   1. Choose **Next**\. The **Choose a schema** page opens\.

1. Choose your database schema\.

   1. Select the check box for the name of schemas that you want to assess and then choose the schema itself\. The schema name is highlighted in blue when selected and the **Next** button is available\.  
![\[Choose one database schema in the new project wizard.\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/new-project-wizard-choose-schema.png)

   1. If you want to assess several database schemas, then select the check boxes for all the schemas and then choose the parent node\. For a successful assessment, you must choose the parent node\. For example, for a source SQL Server database, choose the **Databases** node\. The name of the parent node is highlighted in blue and the **Next** button is available\.  
![\[Choose multiple database schemas in the new project wizard.\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/new-project-wizard-choose-two-schemas.png)

   1. Choose **Next**\. AWS SCT analyzes your source database schemas and creates a database migration assessment report\. The number of database objects in your source database schemas affects the time it takes to run the assessment\. When complete, the **Run the database migration assessment** page opens\.

1. Run the database migration assessment\.

   1. You can review and compare the assessment reports for different migration targets or save a local copy of the assessment report files for the further analysis\.

   1. Save a local copy of the database migration assessment report\. Choose **Save**, then enter the path to the folder to save the files, and choose **Save**\. AWS SCT saves the assessment report files to the specified folder\.

   1. Choose **Next**\. The **Choose a target** page opens\.

1. Choose your target database\.

   1. For **Target engine**, choose the target database engine that you decide to use based on the assessment report\.

   1. Provide your connection information for your target database\. The connection parameters that you see depend on your selected target database engine\. Make sure the user specified for the target database has the required permissions\. For more information about the required permissions, see the sections that describe permissions for target databases in [Sources for AWS SCT](CHAP_Source.md) and [Privileges for Amazon Redshift as a target](CHAP_Converting.DW.md#CHAP_Converting.DW.ConfigureTarget)\.

   1. Choose **Finish**\. AWS SCT creates your project and adds the mapping rules\. For more information, see [Creating mapping rules](CHAP_Mapping.md)\.

Now you can use the AWS SCT project to convert your source database objects\.

## Saving and opening an AWS SCT project<a name="CHAP_UserInterface.SaveProject"></a>

Use the following procedure to save an AWS Schema Conversion Tool project\.

**To save your project**

1. Start the AWS Schema Conversion Tool\.

1. On the **File** menu, choose **Save project**\. 

    AWS SCT saves the project in the folder, which you specified when you created the project\. 

Use the following procedure to open an existing AWS Schema Conversion Tool project\.

**To open your project**

1. On the **File** menu, choose **Open project**\. The **Open** dialog box appears\. 

1.  Choose the project folder and then choose the Windows Script Component \(\*\.sct\) file\. 

1. AWS SCT opens your project but doesn't automatically connect to your source and target databases\. Choose **Connect to the server** at the top of your database schema trees to connect to your source and target databases\.

If you open a project saved in AWS SCT version 1\.0\.655 or before, AWS SCT automatically creates mapping rules for all source database schemas to the target database platform\. To add other target database platforms, delete existing mapping rules and then create new mapping rules\. For more information on creating mapping rules, see [Creating mapping rules in AWS SCT](CHAP_Mapping.md)\. 

## Adding database servers to an AWS SCT project<a name="CHAP_UserInterface.AddServers"></a>

You can add multiple source and target database servers to an AWS Schema Conversion Tool project\.

**To add a server to your project**

1. Start the AWS Schema Conversion Tool\.

1. Create a new project or open an existing project\.

1. Choose **Add source** from the menu to add a new source database\. 

1.  Choose a database platform and specify database connection credentials\. For more information on connecting to a source database, see [Sources for AWS SCT](CHAP_Source.md)\. 

Use the following procedure to connect to your database\.

**To connect to your database**

1. Open the context \(right\-click\) menu for a database server, and then choose **Establish connection**\.

   You can also choose **Connect to the server** at the top of your database schema tree\. 

1.  Enter the password to connect to your source database server\. 

1. Choose **Test connection** to verify that AWS SCT can connect to your source database\. 

1. Choose **Connect** to connect to your source database\.

Use the following procedure to remove a database server from your AWS SCT project\.

**To remove a database server**

1. Choose the database server to remove\.

1. Open the context \(right\-click\) menu, and then choose **Remove from project**\.

    AWS SCT removes the selected database server, all mapping rules, conversion results, and other metadata related to this server\. 

## Running AWS SCT in an offline mode<a name="CHAP_UserInterface.OfflineMode"></a>

You can run AWS Schema Conversion Tool in an offline mode\. Following, you can learn how to work with an existing AWS SCT project when disconnected from your source database\.

AWS SCT doesn't require a connection to your source database to run the following operations:
+ Add mapping rules\.
+ Create database migration assessment reports\.
+ Convert database schemas and code\.
+ Edit your source and converted code\.
+ Save your source and converted code as SQL scripts in a text file\.

Before you use AWS SCT in an offline mode, connect to your source database, load metadata, and save your project\. Open this project or disconnect from the source database server to use AWS SCT in an offline mode\.

**To run AWS SCT in an offline mode**

1. Start the AWS Schema Conversion Tool and create a new project\. For more information, see [Creating an AWS SCT project](#CHAP_UserInterface.Project)\.

1. Add a source database server and connect to your source database\. For more information, see [Adding database servers to an AWS SCT project](#CHAP_UserInterface.AddServers)\.

1. Add a target database server or use a virtual target database platform\. For more information, see [Using virtual targets](CHAP_Mapping.VirtualTargets.md)\.

1. Create a mapping rule to define the target database platform for your source database\. For more information, see [Creating mapping rules in AWS SCT](CHAP_Mapping.md)\.

1. Choose **View**, and then choose **Main view**\. 

1. In the left panel that displays the objects of your source database, choose your source database schemas\. Open the context \(right\-click\) menu for the object, and then choose **Load schema**\. This operation loads all source schema metadata into your AWS SCT project\.

   The **Create report** and **Convert schema** operations also load all source schema metadata into your AWS SCT project\. If you ran one of these operations from the context menu, skip the **Load schema** operation\.

1. On the **File** menu, choose **Save project** to save the source database metadata in your project\.

1. Choose **Disconnect from the server** to disconnect from your source database\. Now you can use AWS SCT in the offline mode\.

## Using AWS SCT tree filters<a name="CHAP_UserInterface.TreeFilters"></a>

To migrate data from a source to a target, AWS SCT loads all metadata from source and target databases into a tree structure\. This structure appears in AWS SCT as the tree view in the main project window\. 

Some databases can have a large number of objects in the tree structure\. You can use *tree filters* in AWS SCT to search for objects in the source and target tree structures\. When you use a tree filter, you don't change the objects that are converted when you convert your database\. The filter changes only what you see in the tree\.

Tree filters work with objects that AWS SCT has preloaded\. In other words, AWS SCT doesn't load objects from the database during searches\. This approach means that the tree structure generally contains fewer objects than are present in the database\.

For tree filters, keep the following in mind:
+ The filter default is ANY, which means that the filter uses a name search to find objects\.
+ When you select one or more object types, you see only those types of objects in the tree\.
+ You can use the filter mask to show different types of symbols, including Unicode, spaces, and special characters\. The “%” character is the wildcard for any symbol\.
+ After you apply a filter, the count shows only the number of filtered objects\.

### <a name="CHAP_UserInterface.UI.TreeFilters.Console"></a>

**To create a tree filter**

1. Open an existing AWS SCT project\.

1. Connect to the database that you want to apply the tree filter to\.

1. Choose the filter icon\.  
![\[The filter icon for the schema tree\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/filter-source-tree.png)

   The undo filter icon is grayed out because no filter is currently applied\.

1. Enter the following information in the **Filter** dialog box\. Options in the dialog box are different for each database engine\.    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/CHAP_UserInterface.html)  
![\[The filter icon for the schema tree\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/filter-tree-db.png)

1. Choose **Add new clause** to add an additional filter clause\. AWS SCT can apply multiple filter clauses using `AND` or `OR` logical operators\. 

1. Choose **Apply**\. After you choose **Apply**, the undo filter icon \(next to the filter icon\) is enabled\. Use this icon if you want to remove the filters you applied\.

1. Choose **Close** to close the dialog box\.

When you filter the schema that appears in the tree, you don't change the objects that are converted when you convert your schema\. The filter only changes what you see in the tree\. 

### Importing a file list for the tree filter<a name="CHAP_UserInterface.UI.TreeFilters.ImportingFileList"></a>

You can import a comma\-separated value \(CSV\) file with semicolon separators or a JSON file that contains names or values that you want the tree filter to use\. Open an existing AWS SCT project, connect to the database to apply the tree filter to, and then choose the filter icon\.

 To download an example of the file, choose **Download template**\. Enter the file name and choose **Save**\. 

 To download your existing filter settings, choose **Export**\. Enter the file name and choose **Save**\. 

To import a file list for the tree filter, choose **Import**\. Choose a file to import, and then choose **Open**\. Choose **Apply**, and then choose **Close**\.

CSV files use semicolon as the separator and have the following format:
+ `object_type` is the type of object that you want to find\.
+ `database_name` is the name of database where this object exists\.
+ `schema_name` is the name of schema where this object exists\.
+ `object_name` is the object name\. 
+ `import_type` specifies to `include` or `exclude` this item from the filter\.

Use JSON files to describe complex filtering cases, such as nested rules\. JSON files have the following format:
+ `filterGroupType` is the type of filter rule \(`AND` or `OR` logical operators\) that applies to multiple filter clauses\.
+ `filterCategory` is the level of the filter \(**Categories** or **Statuses**\)\.
+ `names` is the list of object names that applies for the **Categories** filter\.
+ `filterCondition` is the filtering condition \(`LIKE` or `NOT LIKE`\) that applies for the **Categories** filter\.
+ `transformName` is the status name that applies for the **Status** filter\.
+ `value` is the value to filter the tree by\.
+ `transformValue` is the value of the filter \(`TRUE` or `FALSE`\) that applies for the **Status** filter\.

## Hiding schemas in the AWS SCT tree view<a name="CHAP_UserInterface.HidingSchemas"></a>

By using tree view settings, you specify what schemas and databases you want to see in the AWS SCT tree view\. You can hide empty schemas, empty databases, system databases, and user\-defined databases and schemas\. 

**To hide databases and schemas in tree view**

1. Open an AWS SCT project\.

1. Connect to the data store that you want to show in tree view\.

1. Choose **Settings**, **Global settings**, **Tree view**\.  
![\[The Tree view settings section of the Global settings dialog box\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/treeview-hide.png)

1. In the **Tree view settings** section, do the following:
   + For **Vendor**, choose database platform\.
   + Choose **Hide empty schemas** to hide empty schemas for the selected database platform\.
   + Choose **Hide empty databases** to hide empty databases for the selected database platform\.
   + For **Hide system databases/schemas**, choose system databases and schemas by name to hide them\. 
   + For **Hide user\-defined databases/schemas**, enter the names of user\-defined databases and schemas that you want to hide, and then choose **Add**\. The names are case insensitive\.

1. Choose **OK**\.

## Creating and reviewing the database migration assessment report<a name="CHAP_UserInterface.AssessmentReport"></a>

The *database migration assessment report* summarizes all of the action items for schemas that can't be converted automatically to the engine of your target Amazon RDS DB instance\. The report also includes estimates of the amount of effort that it will take to write the equivalent code for your target DB instance\. 

You can create a database migration assessment report after you add the source databases and target platforms to your project and specify mapping rules\. 

**To create and view the database migration assessment report**

1. Make sure that you created a mapping rule for the source database schema to create an assessment report for\. For more information, see [Adding a new mapping rule](CHAP_Mapping.New.md)\.

1. On the **View** menu, choose **Main view**\. 

1. In the left panel that displays the schema from your source database, choose schema objects to create an assessment report for\. 

   Make sure that you selected the check boxes for all schema objects to create an assessment report for\.

1. Open the context \(right\-click\) menu for the object, and then choose **Create report**\.  
![\[Create database migration assessment report\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/create_assessment_report.png)

   The assessment report view opens\.

1. Choose the **Action items** tab\. 

   The **Action items** tab displays a list of items that describe the schema that can't be converted automatically\. Choose one of the action items in the list\. AWS SCT highlights the item from your schema that the action item applies to, as shown following\.   
![\[Action items tab\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/action_items_tab.png)

1. Choose the **Summary** tab\. 

   The **Summary** tab displays the summary information from the database migration assessment report\. It shows the number of items that were converted automatically, and the number of items that were not converted automatically\. The summary also includes an estimate of the time that it will take to create schema in your target DB instance that are equivalent to those in your source database\. 

   The section **License Evaluation and Cloud Support** contains information about moving your existing on\-premises database schema to an Amazon RDS DB instance running the same engine\. For example, if you want to change license types, this section of the report tells you which features from your current database to remove\. 

   An example of an assessment report summary is shown following\.   
![\[Assessment report summary\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/summary_tab.png)

1. Choose the **Summary** tab, and then choose **Save to PDF**\. The database migration assessment report is saved as a PDF file\. The PDF file contains both the summary and action item information\. 

   You can also choose **Save to CSV** to save the report as a CSV file\. When you choose this option, AWS SCT creates three CSV files\. These files contain the following information:
   + A list of conversion action items with recommended actions\.
   + A summary of conversion action items with an estimate of the effort required to convert an occurrence of the action item\.
   + An executive summary with a number of action items categorized by the estimated time to convert\.  
![\[Database migration assessment report\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/assessment_report.png)

## Converting your schema<a name="CHAP_UserInterface.Converting"></a>

After you added source and target databases to your project and created mapping rules, you can convert your source database schemas\. Use the following procedure to convert schema\.

**To convert your schema**

1. Choose **View**, and then choose **Main view**\.   
![\[Select main view\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/select_main_view.png)

1. In the left panel that displays the schema from your source database, select the check box for the name of the object to convert\. Next, choose this object\. AWS SCT highlights the object name in blue\. Open the context \(right\-click\) menu for the object, and choose **Convert schema**\.

   To convert several database objects, select the check boxes for all objects\. Next, choose the parent node\. For example, for tables, the parent node is **Tables**\. Make sure that AWS SCT highlights the name of the parent node in blue\. Open the context \(right\-click\) menu for the parent node, and choose **Convert schema**\.  
![\[Convert schema\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/transform_schema.png)

1. When AWS SCT finishes converting the schema, you can view the proposed schema in the panel on the right of your project\. 

   At this point, no schema is applied to your target database instance\. The planned schema is part of your project\. If you choose a converted schema item, you can see the planned schema command in the panel at lower center for your target database instance\. 

   You can edit the schema in this window\. The edited schema is stored as part of your project and is written to the target database instance when you choose to apply your converted schema\.   
![\[View the converted schema\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/view_transformed_schema.png)

## Applying the converted schema to your target DB instance<a name="CHAP_UserInterface.ApplyingConversion"></a>

You can apply the converted database schema to your target DB instance\. After the schema has been applied to your target DB instance, you can update the schema based on the action items in the database migration assessment report\. 

**Warning**  
The following procedure overwrites the existing target schema\. Be careful not to overwrite schemas unintentionally\. Be careful not to overwrite schemas in your target DB instance that you have already modified, or you overwrite those changes\. 

**To apply the converted database schema to your target database instance**

1. Choose **Connect to the server** at the top of the right panel of your project to connect to your target database\. If you're connected to your target database, then skip this step\.

1. Choose the schema element in the right panel of your project that displays the planned schema for your target DB instance\. 

1. Open the context \(right\-click\) menu for the schema element, and then choose **Apply to database**\.   
![\[Apply to database\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/write_to_database.png)

   The converted schema is applied to the target DB instance\.

## Storing AWS service profiles in AWS SCT<a name="CHAP_UserInterface.Profiles"></a>

You can store your AWS credentials in AWS SCT\. AWS SCT uses your credentials when you use features that integrate with AWS services\. For example, AWS SCT integrates with Amazon S3, AWS Lambda, Amazon Relational Database Service \(Amazon RDS\), and AWS Database Migration Service \(AWS DMS\)\. 

AWS SCT asks you for your AWS credentials when you access a feature that requires them\. You can store your credentials in the global application settings\. When AWS SCT asks for your credentials, you can select the stored credentials\. 

You can store different sets of AWS credentials in the global application settings\. For example, you can store one set of credentials that you use in test scenarios, and a different set of credentials that you use in production scenarios\. You can also store different credentials for different AWS Regions\. 

### Storing AWS credentials<a name="CHAP_UserInterface.Profiles.Storing"></a>

Use the following procedure to store AWS credentials globally\.

**To store AWS credentials**

1. Start the AWS Schema Conversion Tool\.

1. Open the **Settings** menu, and then choose **Global settings**\. The **Global settings** dialog box appears\.

1. Choose **AWS service profiles**, and then choose **Add a new AWS service profile**\. 

1. Enter your AWS information as follows\.     
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/CHAP_UserInterface.html)

   Choose **Use FIPS endpoint for S3** if you need to comply with the security requirements for the Federal Information Processing Standard \(FIPS\)\. FIPS endpoints are available in the following AWS Regions:
   + US East \(N\. Virginia\) Region
   + US East \(Ohio\) Region
   + US West \(N\. California\) Region
   + US West \(Oregon\) Region

1. Choose **Test connection** to verify that your credentials are correct and active\. 

   The **Test connection** dialog box appears\. You can see the status for each of the services connected to your profile\. **Pass** indicates that the profile can successfully access the service\.   
![\[The Test connection dialog box\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/AWSServiceProfileSettings-Test.png)

1. After you have configured your profile, choose **Save** to save your profile or **Cancel** to cancel your changes\. 

1. Choose **OK** to close the **Global settings** dialog box\. 

### Setting the default profile for a project<a name="CHAP_UserInterface.Profiles.Project"></a>

You can set the default profile for an AWS SCT project\. Doing this associates the AWS credentials stored in the profile with the project\. With your project open, use the following procedure to set the default profile\. 

**To set the default profile for a project**

1. Start the AWS Schema Conversion Tool and create a new project\.

1. On the **Settings** menu, choose **Project settings**\. The **Project settings** dialog box appears\. 

1. Choose the **Project environment** tab\. 

1. Choose **Add a new AWS service profile** to add a new profile\. Then for **AWS service profile**, choose the profile that you want to associate with the project\. 

1. Choose **OK** to close the **Project settings** dialog box\. You can also choose **Cancel** to cancel your changes\. 

### Permissions for using the AWS service profile<a name="CHAP_UserInterface.Profiles.Permissions"></a>

The following permissions are required for accessing your Amazon S3 bucket from your AWS service profile:
+ `s3:PutObject` – to add objects in your Amazon S3 bucket\.
+ `s3:DeleteObject` – to remove the null version of an object and insert a delete marker, which becomes the current version of the object\.
+ `s3:ListBucket` – to return up to 1,000 objects from your Amazon S3 bucket\.
+ `s3:GetObject` – to retrieve objects from your Amazon S3 bucket\.

The following code example shows you how to grant these permissions to your user\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "s3:DeleteObject",
                "s3:GetObject",
                "s3:ListBucket",
                "s3:PutObject"
            ],
            "Resource": [
                "*"
            ]
        }
    ]
}
```

## Using AWS Secrets Manager<a name="CHAP_UserInterface.SecretsManager"></a>

AWS SCT can use database credentials that you store in AWS Secrets Manager\. You can fill in all values in the database connection dialog box from Secrets Manager\. To use Secrets Manager, make sure that you store AWS profiles in the AWS Schema Conversion Tool\.

For more information about using AWS Secrets Manager, see [What is AWS Secrets Manager?](https://docs.aws.amazon.com/secretsmanager/latest/userguide/intro.html) in the *AWS Secrets Manager User Guide*\. For more information about storing AWS profiles, see [Storing AWS service profiles in AWS SCT](#CHAP_UserInterface.Profiles)\.

**To retrieve database credentials from Secrets Manager**

1. Start the AWS Schema Conversion Tool and create a new project\.

1. Choose **Add source** or **Add target** to add a new database to your project\.

1. Choose a database platform and then choose **Next**\.

1. For **AWS Secret**, choose the secret you want to use\.

1. Choose **Populate**\. Then AWS SCT fills in all values in the database connection dialog box\.

1. Choose **Test connection** to verify that AWS SCT can connect to your database\.

1. Choose **Connect** to connect to your database\.

 AWS SCT supports secrets that have the following structure\. 

```
{
  "username": "secret_user",
  "password": "secret_password",
  "engine": "oracle",
  "host": "secret_host.eu-west-1.compute.amazonaws.com",
  "port": "1521",
  "dbname": "ora_db"
}
```

In this structure, the `username` and `password` values are required, and all other values are optional\. Make sure that the values that you store in Secrets Manager include all database credentials\. 

## Storing database passwords<a name="CHAP_UserInterface.StoringPasswords"></a>

You can store a database password or SSL certificate in the AWS SCT cache\. To store a password, choose **Store Password** when you create a connection\. 

The password is encrypted using the randomly generated token in the `seed.dat` file\. The password is then stored with the user name in the cache file\. If you lose the `seed.dat` file or it becomes corrupted, the database password might be unencrypted incorrectly\. In this case, the connection fails\. 

## Using the UNION ALL view for projects with partitioned tables<a name="CHAP_UserInterface.UnionAllView"></a>

If a source table is partitioned, AWS SCT creates *n* target tables, where *n* is the number of partitions on the source table\. AWS SCT creates a UNION ALL view on top of the target tables to represent the source table\. If you use an AWS SCT data extractor to migrate your data, the source table partitions will be extracted and loaded in parallel by separate subtasks\.

**To use Union All view for a project**

1. Start AWS SCT\. Create a new project or open an existing AWS SCT project\.

1. On the **Settings** menu, choose **Conversion settings**\. 

1. Choose a pair of OLAP databases from the list at the top\.

1. Turn on **Use Union all view?**  
![\[Conversion settings\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/conversion-settings.png)

1. Choose **OK** to save the settings and close the **Conversion settings** dialog box\. 

## Keyboard shortcuts for AWS SCT<a name="CHAP_UserInterface.KeyboardShortcuts"></a>

The following are the keyboard shortcuts that you can use with AWS SCT\. 


| Keyboard shortcut | Description | 
| --- | --- | 
| Ctrl\+N | Create a new project\. | 
| Ctrl\+O | Open an existing project\. | 
| Ctrl\+S | Save an open project\. | 
| Ctrl\+W | Create a new project by using the wizard\. | 
| Ctrl\+M | Create a new multiserver assessment\. | 
| Ctrl\+L | Add a new source database\. | 
| Ctrl\+R | Add a new target database\. | 
| Ctrl\+F4 | Close an open project\. | 
| F1 | Open the *AWS SCT User Guide*\. | 