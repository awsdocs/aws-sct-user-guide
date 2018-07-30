# Converting Data Warehouse Schemas to Amazon Redshift Using the AWS Schema Conversion Tool<a name="CHAP_Converting.DW"></a>

The AWS Schema Conversion Tool \(AWS SCT\) automates much of the process of converting your data warehouse schema to an Amazon Redshift database schema\. Because the source and target database engines can have many different features and capabilities, AWS SCT attempts to create an equivalent schema in your target database wherever possible\. If no direct conversion is possible, AWS SCT provides an assessment report with a list of possible actions for you to take\. Using AWS SCT, you can manage keys, map data types and objects, and create manual conversions\.

AWS SCT can convert the following data warehouse schemas to Amazon Redshift\.
+ Greenplum Database \(version 4\.3 and later\)
+ Microsoft SQL Server \(version 2008 and later\)
+ Netezza \(version 7\.0\.3 and later\)
+ Oracle \(version 10 and later\)
+ Teradata \(version 13 and later\)
+ Vertica \(version 7\.2\.2 and later\)

If you want to convert an online transaction processing \(OLTP\) database schema, see [Converting Database Schemas Using the AWS Schema Conversion Tool](CHAP_Converting.md)\. 

To convert a data warehouse schema, you take the following steps\. 

1. Specify the optimization strategy and rules, and specify the mapping that you want AWS SCT to use\. You can set up rules that change the data type of columns, move objects from one schema to another, and change the names of objects\.

    You can specify optimization and mapping in **Settings**\. For more information on optimization strategies, see [ Choosing Optimization Strategies and Rules for Use with the AWS Schema Conversion Tool](#CHAP_Converting.DW.Strategy)\. for more information about mapping, see [ Creating Mapping Rules in the AWS Schema Conversion Tool](#CHAP_Converting.DW.Mapping) 

1. Provide statistics on your source data warehouse so that AWS SCT can optimize how your data warehouse is converted\. You can either collect statistics directly from the database, or upload an existing statistics file\. For more information about providing data warehouse statistics, see [ Collecting or Uploading Statistics for the AWS Schema Conversion Tool](#CHAP_Converting.DW.Statistics)\. 

1. Create a database migration assessment report that details the schema elements that can't be converted automatically\. You can use this report to identify where you need to manually create a schema in your target database that is compatible with your source database\. For more information about the assessment report, see [AWS Schema Conversion Tool Assessment Report](CHAP_AssessmentReport.md)\. 

1. Convert the schema\. AWS SCT creates a local version of the converted schema for you to review, but it doesn't apply it to your target database until you are ready\. For more information about converting, see [Converting Your Schema by Using the AWS Schema Conversion Tool](#CHAP_Converting.DW.Convert) 

1.  After you convert your schema, you can manage and edit your keys\. Key management is the heart of a data warehouse conversion\. For more information about managing keys, see [ Managing and Customizing Keys in the AWS Schema Conversion Tool](#CHAP_Converting.DW.Keys)\. 

1.  If you have schema elements that can't be converted automatically, you have two choices: update the source schema and then convert again, or create equivalent schema elements in your target database\. For more information on manually converting schema elements, see [ Handling Manual Conversions in the AWS Schema Conversion Tool](#CHAP_Converting.DW.Manual)\. For more information about updating your source schema, see [ Updating and Refreshing Your Converted Schema in the AWS Schema Conversion Tool](#CHAP_Converting.DW.UpdateRefresh)\. 

1. When you are ready, you can apply the converted schema to your target database\. For more information about saving and applying the converted schema, see [ Saving and Applying Your Converted Schema in the AWS Schema Conversion Tool](#CHAP_Converting.DW.SaveAndApply)\. 

## Choosing Optimization Strategies and Rules for Use with the AWS Schema Conversion Tool<a name="CHAP_Converting.DW.Strategy"></a>

To optimize how the AWS Schema Conversion Tool \(AWS SCT\) converts your data warehouse schema, you can choose the strategies and rules you want the tool to use\. After converting your schema, and reviewing the suggested keys, you can adjust your rules or change your strategy to get the results you want\. 

**To choose your optimization strategies and rules**

1. Choose **Settings**, and then choose **Project Settings**\. The **Current project settings** dialog box appears\. 

1. In the left pane, choose **Optimization Strategies**\. The optimization strategies appear in the right pane with the defaults selected\. 

1. For **Strategy Sector**, choose the optimization strategy you want to use\. You can choose from the following: 
   + **Use metadata, ignore statistical information** – In this strategy, only information from the metadata is used for optimization decisions\. For example, if there is more than one index on a source table, the source database sort order is used, and the first index becomes a distribution key\. 

      
   + **Ignore metadata, use statistical information** – In this strategy, optimization decisions are derived from statistical information only\. This strategy applies only to tables and columns for which statistics are provided\. For more information, see [ Collecting or Uploading Statistics for the AWS Schema Conversion Tool](#CHAP_Converting.DW.Statistics)\. 

      
   + **Use metadata and use statistical information** – In this strategy, both metadata and statistics are used for optimization decisions\. 

      

1. After you choose your optimization strategy, you can choose the rules you want to use\. You can choose from the following: 
   + **Choose Distribution Key and Sort Keys using metadata**
   + **Choose fact table and appropriate dimension for collation**
   + **Analyze cardinality of indexes' columns**
   + **Find the most used tables and columns from QueryLog table**

   For each rule, you can enter a weight for the sort key and a weight for the distribution key\. AWS SCT uses the weights you choose when it converts your schema\. Later, when you review the suggested keys, if you are not satisfied with the results, you can return here and change your settings\. For more information, see [ Managing and Customizing Keys in the AWS Schema Conversion Tool](#CHAP_Converting.DW.Keys)\. 

## Collecting or Uploading Statistics for the AWS Schema Conversion Tool<a name="CHAP_Converting.DW.Statistics"></a>

To optimize how the AWS Schema Conversion Tool \(AWS SCT\) converts your data warehouse schema, you can provide statistics from your source database that the tool can use\. You can either collect statistics directly from the database, or upload an existing statistics file\. 

**To provide and review statistics**

1. Open your project and connect to your source database\. 

1. Choose a schema object from the left panel of your project, and open the context \(right\-click\) menu for the object\. Choose **Collect Statistics** or **Upload Statistics** as shown following\.   
![\[Context menu with collect statistics\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/collect-statistics.png)

1. Choose a schema object from the left panel of your project, and then choose the **Statistics** tab\. You can review the statistics for the object\.   
![\[Statistics tab\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/statistics.png)

   Later, when you review the suggested keys, if you are not satisfied with the results, you can collect additional statistics and repeat this procedure\. For more information, see [ Managing and Customizing Keys in the AWS Schema Conversion Tool](#CHAP_Converting.DW.Keys)\. 

## Creating Mapping Rules in the AWS Schema Conversion Tool<a name="CHAP_Converting.DW.Mapping"></a>

Before you convert your schema with the AWS Schema Conversion Tool \(AWS SCT\), you can set up rules that change the data type of columns, move objects from one schema to another, and change the names of objects\. For example, if you have a set of tables in your source schema named `test_TABLE_NAME`, you can set up a rule that changes the prefix `test_` to the prefix `demo_` in the target schema\. 

**Note**  
You can only create mapping rules if your source database engine and target database engine are different\. 

You can create mapping rules that perform the following tasks: 
+ Change data type 
+ Move objects 
+ Rename objects 
+ Prefix \- add prefix, remove prefix, replace prefix 
+ Suffix \- add suffix, remove suffix, replace suffix 

You can create mapping rules for the following objects: 
+ Database 
+ Schema 
+ Table 
+ Column 

### Creating Mapping Rules<a name="CHAP_Converting.DW.Mapping.Map"></a>

You can create mapping rules and save the rules as part of your project\. With your project open, use the following procedure to create mapping rules\. 

**To create mapping rules**

1. Choose **Mapping Rules** from the **Settings** menu\. The **Mapping Rules** dialog box appears\. The top pane contains mapping \(transformation\) rules\.   
![\[The mapping rules dialog box\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/mapping-rules-2.PNG)

1. In the **Tranformation Rules** pane, choose **Add new rule**\. 

1. Configure your transformation rule\. 

   1. For **Name**, type a name for your rule\. 

   1. For **For**, choose the type of object that the rule applies to\. 

   1. For **where**, type a filter to apply to objects before applying the mapping rule\. The where clause is evaluated by using a like clause\. You can enter an exact name to select one object, or you can enter a pattern to select multiple objects\. 

      The fields available for the **where** clause are different depending on the type of the object\. For example, if the object type is schema there is only one field available, for the schema name\. 

   1. For **Actions**, choose the type of mapping rule you want to create\. 

   1. Depending on the rule type, type one or two additional values\. For example, to rename an object, type the new name of the object\. To replace a prefix, type the old prefix and the new prefix\. 

1. After you have configured your mapping rule, choose **Save** to save your rule\. You can also choose **Cancel** to cancel your changes\. 

1. After you are done adding, editing, and deleting rules, choose **Save All** to save all your changes\. 

1. Choose **Close** to close the **Mapping Rules** dialog box\. 

You can use the toggle icon to turn off a mapping rule without deleting it\. You can use the copy icon to duplicate an existing mapping rule\. You can use the delete icon to delete an existing mapping rule\. To save any changes you make to your mapping rules, choose **Save All**\. 

### Viewing Mapping Rules for Objects<a name="CHAP_Converting.DW.Mapping.View"></a>

After you set up your mapping rules, you can view the effect of the rules on specific objects in your schema before you convert your schema\. In the source schema tree, choose the object you are interested in\. In the main view, choose the **Mapping** tab\. The **Mapping** tab opens and displays a list of all mapping rules that are applied to the object\. You can see the name of the object in the source schema and the new name of the object in the target schema\. If you have data type rules, you also see the data type of the column in the source schema and the new data type of the column in the target schema\. 

### Exporting Mapping Rules<a name="CHAP_Converting.DW.Mapping.Export"></a>

If you use AWS Database Migration Service \(AWS DMS\) to migrate your data from your source database to your target database, you can provide information about your mapping rules to AWS DMS\. For more information about tasks, see [Working with AWS Database Migration Service Replication Tasks](http://docs.aws.amazon.com/dms/latest/userguide/CHAP_Tasks.html)\. 

**To export mapping rules**

1. In the AWS Schema Conversion Tool, in the source schema tree, open the context \(right\-click\) menu and choose **Export script for DMS**\. The save dialog box opens\. 

1. Browse to the location where you want to save your script, and then choose **Save**\. Your mapping rules are saved as a JSON script that can be consumed by AWS DMS\. 

## Converting Your Schema by Using the AWS Schema Conversion Tool<a name="CHAP_Converting.DW.Convert"></a>

After you have connected your project to both your source database and your target database, your AWS Schema Conversion Tool \(AWS SCT\) project displays the schema from your source database in the left panel\. The schema is presented in a tree\-view format, and each node of the tree is lazy loaded\. When you choose a node in the tree view, AWS SCT requests the schema information from your source database at that time\. 

You can choose schema items from your source database and then convert the schema to equivalent schema for the database engine of your target database\. You can choose any schema item from your source database to convert\. If the schema item that you choose depends on a parent item, then AWS SCT also generates the schema for the parent item\. For example, if you choose a column from a table to convert, then AWS SCT generates the schema for the column, the table that the column is in, and the database that the table is in\. 

### Converting Schema<a name="CHAP_Converting.DW.Convert.Convert"></a>

To convert schema from your source database, choose a schema object to convert from the left panel of your project\. Open the context \(right\-click\) menu for the object, and then choose **Convert schema**, as shown following\. 

![\[Convert schema\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/transform_schema.png)

After you have converted the schema from your source database, you can choose schema items from the left panel of your project and view the converted schema in the center panels of your project\. The lower\-center panel displays the properties of and the SQL command to create the converted schema, as shown following\. 

![\[Choose source schema item\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/select_schema_item.png)

After you have converted your schema, you can save your project\. The schema information from your source database is saved with your project\. This functionality means that you can work offline without being connected to your source database\. AWS SCT connects to your source database to update the schema in your project if you choose **Refresh from Database** for your source database\. For more information, see [ Updating and Refreshing Your Converted Schema in the AWS Schema Conversion Tool](#CHAP_Converting.DW.UpdateRefresh)\. 

You can create a database migration assessment report of the items that can't be converted automatically\. The assessment report is useful for identifying and resolving schema items that can't be converted automatically\. For more information, see [AWS Schema Conversion Tool Assessment Report](CHAP_AssessmentReport.md)\. 

When AWS SCT generates a converted schema, it doesn't immediately apply it to the target database\. Instead, the converted schema is stored locally until you are ready to apply it to the target database\. For more information, see [ Applying Your Converted Schema](#CHAP_Converting.DW.Applying)\. 

### Editing Converted Schema<a name="CHAP_Converting.DW.Convert.Edit"></a>

You can edit converted schema and save the changes as part of your project\.

**To edit converted schema**

1. In the left panel that displays the schema from your source database, choose the schema item that you want to edit the converted schema for\. 

1. In the lower\-center panel that displays the converted schema for the selected item, choose the **SQL** tab\. 

1. In the text displayed for the **SQL** tab, change the schema as needed\. The schema is automatically saved with your project as you update it\.   
![\[Refresh the schema from the target database\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/edit_converted_schema.png)

The changes that you make to converted schema are stored with your project as you make updates\. If you newly convert a schema item from your source database, and you have made updates to previously converted schema for that item, those existing updates are replaced by the newly converted schema item based on your source database\. 

### Clearing a Converted Schema<a name="CHAP_Converting.DW.Convert.Clear"></a>

Until you apply the schema to your target database, AWS SCT only stores the converted schema locally in your project\. You can clear the planned schema from your project by choosing the tree\-view node for your target database, and then choosing **Refresh from Database**\. Because no schema has been written to your target database, refreshing from the database removes the planned schema elements in your AWS SCT project to match what exists in your target database\. 

![\[Refresh the schema from the target database\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/refresh_from_target_instance.png)

## Managing and Customizing Keys in the AWS Schema Conversion Tool<a name="CHAP_Converting.DW.Keys"></a>

After you convert your schema with the AWS Schema Conversion Tool \(AWS SCT\), you can manage and edit your keys\. Key management is the heart of a data warehouse conversion\. 

To manage keys, select a table in your target database, and then choose the **Key Management** tab as shown following\. 

![\[Key management tab\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/key-management.png)

The left pane contains key suggestions, and includes the confidence rating for each suggestion\. You can choose one of the suggestions, or you can customize the key by editing it in the right pane\. 

If the choices for the key don't look like what you expected, you can edit your edit your optimization strategies, and then retry the conversion\. For more information, see [ Choosing Optimization Strategies and Rules for Use with the AWS Schema Conversion Tool](#CHAP_Converting.DW.Strategy)\. 

## Handling Manual Conversions in the AWS Schema Conversion Tool<a name="CHAP_Converting.DW.Manual"></a>

The assessment report includes a list of items that can't be converted automatically to the database engine of your target database\. For each item that can't be converted, there is an action item on the **Action Items** tab\. 

You can respond to the action items in the assessment report in the following ways: 
+ Modify your source database schema\.
+ Modify your target database schema\.

### Modifying Your Source Schema<a name="CHAP_Converting.DW.Manual.Source"></a>

For some items, it might be easier to modify the database schema in your source database to schema that can be converted automatically\. First, verify that the new changes are compatible with your application architecture, then update the schema in your source database\. Finally, refresh your project with the updated schema information\. You can then convert your updated schema, and generate a new database migration assessment report\. The action items no longer appear for the items that changed in the source schema\. 

The advantage of this process is that your updated schema is always available when you refresh from your source database\. 

### Modifying Your Target Schema<a name="CHAP_Converting.DW.Manual.Target"></a>

For some items, it might be easier to apply the converted schema to your target database, and then add equivalent schema items manually to your target database for the items that couldn't be converted automatically\. You can write all of the schema that can be converted automatically to your target database by applying the schema\. For more information, see [ Saving and Applying Your Converted Schema in the AWS Schema Conversion Tool](#CHAP_Converting.DW.SaveAndApply)\. 

The schema that are written to your target database don't contain the items that can't be converted automatically\. After applying the schema to your target database, you can then manually create schema in your target database that are equivalent to those in the source database\. The action items in the database migration assessment report contain suggestions for how to create the equivalent schema\. 

**Warning**  
If you manually create schema in your target database, save a copy of any manual work that you do\. If you apply the converted schema from your project to your target database again, it overwrites the manual work you have done\. 

In some cases, you can't create equivalent schema in your target database\. You might need to rearchitect a portion of your application and database to use the functionality that is available from the engine for your target database\. In other cases, you can simply ignore the schema that can't be converted automatically\. 

## Updating and Refreshing Your Converted Schema in the AWS Schema Conversion Tool<a name="CHAP_Converting.DW.UpdateRefresh"></a>

You can update both the source schema and the target schema in your AWS Schema Conversion Tool \(AWS SCT\) project\. 
+ **Source** – If you update the schema for your source database, AWS SCT replaces the schema in your project with the latest schema from your source database\. Using this functionality, you can update your project if changes have been made to the schema of your source database\. 

   
+ **Target** – If you update the schema for your target database, AWS SCT replaces the schema in your project with the latest schema from your target database\. If you haven't applied any schema to your target database, AWS SCT clears the converted schema from your project\. You can then convert the schema from your source database for a clean target database\. 

   

You update the schema in your AWS SCT project by choosing **Refresh from Database**, as shown following\. 

![\[Refresh the schema from the source database\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/refresh_from_source_database.png)

## Saving and Applying Your Converted Schema in the AWS Schema Conversion Tool<a name="CHAP_Converting.DW.SaveAndApply"></a>

When the AWS Schema Conversion Tool \(AWS SCT\) generates converted schema \(as shown in [Converting Your Schema by Using the AWS Schema Conversion Tool](#CHAP_Converting.DW.Convert)\), it doesn't immediately apply the converted schema to the target database\. Instead, converted schema are stored locally in your project until you are ready to apply them to the target database\. Using this functionality, you can work with schema items that can't be converted automatically to your target database engine\. For more information on items that can't be converted automatically, see [AWS Schema Conversion Tool Assessment Report](CHAP_AssessmentReport.md)\. 

You can optionally have the tool save your converted schema to a file as a SQL script prior to applying the schema to your target database\. You can also have the tool apply the converted schema directly to your target database\. 

### Saving Your Converted Schema to a File<a name="CHAP_Converting.DW.Saving"></a>

You can save your converted schema as SQL scripts in a text file\. By using this approach, you can modify the generated SQL scripts from AWS SCT to address items that the tool can't convert automatically\. You can then run your updated scripts on your target database to apply your converted schema to your target database\. 

To save your converted schema as SQL scripts, open the context \(right\-click\) menu for the schema element, and choose **Save as SQL**, as shown following\. 

![\[Save SQL scripts to a file\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/save_as_file.png)

### Applying Your Converted Schema<a name="CHAP_Converting.DW.Applying"></a>

When you are ready to apply your converted schema to your target database, choose the schema element from the right panel of your project\. Open the context \(right\-click\) menu for the schema element, and then choose **Apply to database**, as shown following\. 

![\[Apply to database\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/write_to_database.png)

### The Extension Pack Schema<a name="CHAP_Converting.DW.SaveAndApply.Ext"></a>

The first time that you apply your converted schema to your target DB instance, AWS SCT adds an additional schema to your target DB instance\. This schema implements system functions of the source database that are required when writing your converted schema to your target DB instance\. The schema is called the extension pack schema\. 

Don't modify the extension pack schema, or you might encounter unexpected results in the converted schema that is written to your target DB instance\. When your schema is fully migrated to your target DB instance, and you no longer need AWS SCT, you can delete the extension pack schema\. 

The extension pack schema is named according to your source database as follows: 
+ Greenplum: `AWS_GREENPLUM_EXT`
+ Microsoft SQL Server: `AWS_SQLSERVER_EXT`
+ Netezza: `AWS_NETEZZA_EXT`
+ Oracle: `AWS_ORACLE_EXT`
+ Teradata: `AWS_TERADATA_EXT`
+ Vertica: `AWS_VERTICA_EXT`

For more information, see [Using the AWS Schema Conversion Tool Extension Pack](CHAP_ExtensionPack.md)\. 

### Python Libraries<a name="CHAP_Converting.DW.SaveAndApply.Py"></a>

To create custom functions in Amazon Redshift, you use the Python language\. Use the AWS SCT extension pack to install python libraries for your Amazon Redshift database\. For more information, see [Using the AWS Schema Conversion Tool Extension Pack](CHAP_ExtensionPack.md)\. 