# Handling Manual Conversions in the AWS Schema Conversion Tool<a name="CHAP_SchemaConversionTool.Manual"></a>

The assessment report includes a list of items that can't be converted automatically to the database engine of your target Amazon RDS DB instance\. For each item that can't be converted, there is an action item on the **Action Items** tab\. 

You can respond to the action items in the assessment report in the following ways: 

+ Modify your source database schema\.

+ Modify your target database schema\.

## Modifying Your Source Schema<a name="CHAP_SchemaConversionTool.Manual.Source"></a>

For some items, it might be easier to modify the database schema in your source database to schema that can be converted automatically\. First, verify that the new changes are compatible with your application architecture, then update the schema in your source database\. Finally, refresh your project with the updated schema information\. You can then convert your updated schema, and generate a new database migration assessment report\. The action items no longer appear for the items that changed in the source schema\. 

The advantage of this process is that your updated schema is always available when you refresh from your source database\. 

## Modifying Your Target Schema<a name="CHAP_SchemaConversionTool.Manual.Target"></a>

For some items, it might be easier to apply the converted schema to your target database, and then add equivalent schema items manually to your target database for the items that couldn't be converted automatically\. You can write all of the schema that can be converted automatically to your target DB instance by applying the schema\. For more information, see [Saving and Applying Your Converted Schema in the AWS Schema Conversion Tool](CHAP_SchemaConversionTool.SaveAndApply.md)\. 

The schema that are written to your target DB instance don't contain the items that can't be converted automatically\. After applying the schema to your target DB instance, you can then manually create schema in your target DB instance that are equivalent to those in the source database\. The action items in the database migration assessment report contain suggestions for how to create the equivalent schema\. 

**Warning**  
If you manually create schema in your target DB instance, save a copy of any manual work that you do\. If you apply the converted schema from your project to your target DB instance again, it overwrites the manual work you have done\. 

In some cases, you can't create equivalent schema in your target DB instance\. You might need to rearchitect a portion of your application and database to use the functionality that is available from the DB engine for your target DB instance\. In other cases, you can simply ignore the schema that can't be converted automatically\. 

## Related Topics<a name="w3ab1c15c15c29c13"></a>

+ [Converting Your Schema by Using the AWS Schema Conversion Tool](CHAP_SchemaConversionTool.Convert.md)

+ [Creating and Using the Assessment Report in the AWS Schema Conversion Tool](CHAP_SchemaConversionTool.AssessmentReport.md)

+ [Updating and Refreshing Your Converted Schema in the AWS Schema Conversion Tool](CHAP_SchemaConversionTool.UpdateRefresh.md)