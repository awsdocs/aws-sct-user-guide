# Converting Your Schema by Using the AWS Schema Conversion Tool<a name="CHAP_SchemaConversionTool.Convert"></a>

After you have connected your project to both your source database and your target Amazon RDS DB instance, your AWS Schema Conversion Tool \(AWS SCT\) project displays the schema from your source database in the left panel\. The schema is presented in a tree\-view format, and each node of the tree is lazy loaded\. When you choose a node in the tree view, AWS SCT requests the schema information from your source database at that time\. 

You can choose schema items from your source database and then convert the schema to equivalent schema for the DB engine of your target DB instance\. You can choose any schema item from your source database to convert\. If the schema item that you choose depends on a parent item, then AWS SCT also generates the schema for the parent item\. For example, if you choose a column from a table to convert, then AWS SCT generates the schema for the column, the table that the column is in, and the database that the table is in\. 

## Converting Schema<a name="CHAP_SchemaConversionTool.Convert.Convert"></a>

To convert schema from your source database, choose a schema object to convert from the left panel of your project\. Open the context \(right\-click\) menu for the object, and then choose **Convert schema**, as shown following\. 

![\[Convert schema\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/transform_schema.png)

After you have converted the schema from your source database, you can choose schema items from the left panel of your project and view the converted schema in the center panels of your project\. The lower\-center panel displays the properties of and the SQL command to create the converted schema, as shown following\. 

![\[Choose source schema item\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/select_schema_item.png)

After you have converted your schema, you can save your project\. The schema information from your source database is saved with your project\. This functionality means that you can work offline without being connected to your source database\. AWS SCT connects to your source database to update the schema in your project if you choose **Refresh from Database** for your source database\. For more information, see [Updating and Refreshing Your Converted Schema in the AWS Schema Conversion Tool](CHAP_SchemaConversionTool.UpdateRefresh.md)\. 

You can create a database migration assessment report of the items that can't be converted automatically\. The assessment report is useful for identifying and resolving schema items that can't be converted automatically\. For more information, see [Creating and Using the Assessment Report in the AWS Schema Conversion Tool](CHAP_SchemaConversionTool.AssessmentReport.md)\. 

When AWS SCT generates a converted schema, it doesn't immediately apply it to the target DB instance\. Instead, the converted schema is stored locally until you are ready to apply it to the target DB instance\. For more information, see [Applying Your Converted Schema](CHAP_SchemaConversionTool.SaveAndApply.md#CHAP_SchemaConversionTool.Applying)\. 

## Editing Converted Schema<a name="CHAP_SchemaConversionTool.Convert.Edit"></a>

You can edit converted schema and save the changes as part of your project\.

**To edit converted schema**

1. In the left panel that displays the schema from your source database, choose the schema item that you want to edit the converted schema for\. 

1. In the lower\-center panel that displays the converted schema for the selected item, choose the **SQL** tab\. 

1. In the text displayed for the **SQL** tab, change the schema as needed\. The schema is automatically saved with your project as you update it\.   
![\[Refresh the schema from the target DB instance\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/edit_converted_schema.png)

The changes that you make to converted schema are stored with your project as you make updates\. If you newly convert a schema item from your source database, and you have made updates to previously converted schema for that item, those existing updates are replaced by the newly converted schema item based on your source database\. 

## Clearing a Converted Schema<a name="CHAP_SchemaConversionTool.Convert.Clear"></a>

Until you apply the schema to your target DB instance, AWS SCT only stores the converted schema locally in your project\. You can clear the planned schema from your project by choosing the tree\-view node for your target DB instance, and then choosing **Refresh from Database**\. Because no schema has been written to your target DB instance, refreshing from the database removes the planned schema elements in your AWS SCT project to match what exists in your target DB instance\. 

![\[Refresh the schema from the target DB instance\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/refresh_from_target_instance.png)