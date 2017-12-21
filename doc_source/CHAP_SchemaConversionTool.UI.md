# About the AWS Schema Conversion Tool User Interface<a name="CHAP_SchemaConversionTool.UI"></a>

The following sections help you work with the AWS Schema Conversion Tool \(AWS SCT\) user interface\. 

## The Project Window<a name="CHAP_SchemaConversionTool.Overview.ProjectWindow"></a>

The illustration following is what you see in the AWS Schema Conversion Tool when you create a schema migration project, and then convert a schema\. 

1. In the left panel, the schema from your source database is presented in a tree view\. Your database schema is "lazy loaded\." In other words, when you select an item from the tree view, AWS SCT gets and displays the current schema from your source database\. 

1. In the top middle panel, action items appear for schema elements from the source database engine that couldn't be converted automatically to the target database engine\. 

1. In the right panel, the schema from your target DB instance is presented in a tree view\. Your database schema is "lazy loaded\." That is, at the point when you select an item from the tree view, AWS SCT gets and displays the current schema from your target database\. 

![\[The AWS Schema Conversion Tool Project Window\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/AWS_Migration_Tool.png)

1. In the lower left panel, when you choose a schema element, properties describing the source schema element and the SQL command to create that element in the source database are displayed\. 

1. In the lower right panel, when you choose a schema element, properties describing the target schema element and the SQL command to create that element in the target database are displayed\. You can edit this SQL command and save the updated command with your project\. 

## Using Tree Filters<a name="CHAP_SchemaConversionTool.UI.TreeFilters"></a>

 To migrate data from a source to a target, AWS Schema Conversion Tool \(AWS SCT\) loads all metadata from source and target databases into a tree structure\. This is displayed in the AWS SCT UI as the tree view on the Main window\. Because some databases can have a large number of objects in the tree structure, AWS SCT uses filters to lets you search for objects in the source and target tree structures\. When you use tree filters, you don't change the objects that are converted when you convert your database\. The filter only changes what you see in the tree\.

Tree filters work with objects that AWS SCT has preloaded; it does not load objects from the database during searches\. This means the tree structure contains fewer objects than are actually present in the database\.

There are several important things to know about tree filters\. These include:

+ The filter default is ANY, which means the filter uses name search to find objects\.

+ When you select one or more object types, you will see only those objects in the tree\.

+ The filter mask can be used to show different types of symbols, including Unicode, spaces, and special characters\. The “%” character is the wildcard for any symbol\.

+ After you apply a filter, the count shows only the number of filtered objects\.

### <a name="CHAP_SchemaConversionTool.UI.TreeFilters.Console"></a>

You can use the AWS SCT UI to filter your tree view\. 

**To create a tree filter**

1. Open an existing AWS SCT project\.

1. Connect to the database you want to apply the tree filter to\.

1. Choose the filter icon\. Note that the undo filter icon is grayed out since you currently do not have a filter applied\.  
![\[The filter icon for the schema tree\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/filter-source-tree.png)

1. Enter the following information in the **Tree Filter** dialog box\. Note that the fields in the dialog box are different for each database engine\.  
![\[The filter icon for the schema tree\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/filter-tree-db.png)    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/CHAP_SchemaConversionTool.UI.html)

1. Choose **Apply**\. Once you select **Apply**, the undo filter icon \(next to the filter icon\) is enabled\. Use this icon if you want to remove the filters you applied\.

1. Choose **Close** to close the dialog box\.

When you filter the schema that appears in the tree, you don't change the objects that are converted when you convert your schema\. The filter only changes what you see in the tree\. 

### Importing a File List for the Tree Filter<a name="CHAP_SchemaConversionTool.UI.TreeFilters.ImportingFileList"></a>

You can import a file that contains names or values that you want the tree filter to use\. Object is type of object you want to find, Database is the name of database where this object exist, and Schema is the name of schema where this object exist, Name is the object name\. The file to import should have the following format:

+ Object;Database;Schema;Name \- This is a mandatory format for the following SQL dialects: Microsoft SQL Server, Netezza, Microsoft SQL Server DW\.

+ Object;Schema;Name – Use this format for other SQL dialects\.

1. Choose the filter icon\.  
![\[The filter icon for the schema tree\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/filter-source-tree.png)

1. Select the Import File List tab\.

1. Choose **Import File**\.

1. Select a file to import and choose **Open**\.

1. Choose **Apply** and then **Close**\.

## Hiding Schemas in the AWS SCT Tree View<a name="CHAP_SchemaConversionTool.HidingSchemas"></a>

In **Tree View Settings**, you can hide empty schemas, empty databases, system databases, and user defined databases and schemas\. You specify what schemas and databases you want to see in the AWS SCT tree view\.

**To hide databases and schemas in tree view**

1. Open an AWS SCT project\.

1. Connect to the data store you want to show in tree view\.

1. Select **Settings**, then **Global Settings**, then **Tree View**\.  
![\[The tree view dialog box\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/treeview-hide.png)

1. Choose the databases and schemas you want to hide\. Choose system databases or schemas to hide them\. Choose **Add** and type the name of user defined schemas or databases that you want to hide\. The names are case insensitive\. To reset the tree view to default settings, choose **Reset to Default**\. 

1. Choose **OK**\.

## Keyboard Shortcuts for the AWS Schema Conversion Tool<a name="CHAP_SchemaConversionTool.KeyboardShortcuts"></a>

The following are the keyboard shortcuts that you can use with the AWS Schema Conversion Tool \(AWS SCT\)\. 


****  

| Keyboard Shortcut | Description | 
| --- | --- | 
| Ctrl\+N | Create a new project\. | 
| Ctrl\+O | Open an existing project\. | 
| Ctrl\+S | Save an open project\. | 
| Ctrl\+W | Create a new project by using the wizard\. | 
| Ctrl\+L | Connect to the source database\. | 
| Ctrl\+R | Connect to the target database\. | 

## Related Topics<a name="CHAP_SchemaConversionTool.UI.Related"></a>

+ [What Is the AWS Schema Conversion Tool?](Welcome.md)

+ [Installing and Updating the AWS Schema Conversion Tool](CHAP_SchemaConversionTool.Installing.md)