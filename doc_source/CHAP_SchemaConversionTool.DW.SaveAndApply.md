# Saving and Applying Your Converted Schema in the AWS Schema Conversion Tool<a name="CHAP_SchemaConversionTool.DW.SaveAndApply"></a>

When the AWS Schema Conversion Tool \(AWS SCT\) generates converted schema \(as shown in [Converting Your Schema by Using the AWS Schema Conversion Tool](CHAP_SchemaConversionTool.DW.Convert.md)\), it doesn't immediately apply the converted schema to the target database\. Instead, converted schema are stored locally in your project until you are ready to apply them to the target database\. Using this functionality, you can work with schema items that can't be converted automatically to your target database engine\. For more information on items that can't be converted automatically, see [Creating and Using the Assessment Report in the AWS Schema Conversion Tool](CHAP_SchemaConversionTool.DW.AssessmentReport.md)\. 

You can optionally have the tool save your converted schema to a file as a SQL script prior to applying the schema to your target database\. You can also have the tool apply the converted schema directly to your target database\. 

## Saving Your Converted Schema to a File<a name="CHAP_SchemaConversionTool.DW.Saving"></a>

You can save your converted schema as SQL scripts in a text file\. By using this approach, you can modify the generated SQL scripts from AWS SCT to address items that the tool can't convert automatically\. You can then run your updated scripts on your target database to apply your converted schema to your target database\. 

To save your converted schema as SQL scripts, open the context \(right\-click\) menu for the schema element, and choose **Save as SQL**, as shown following\. 

![\[Save SQL scripts to a file\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/save_as_file.png)

## Applying Your Converted Schema<a name="CHAP_SchemaConversionTool.DW.Applying"></a>

When you are ready to apply your converted schema to your target database, choose the schema element from the right panel of your project\. Open the context \(right\-click\) menu for the schema element, and then choose **Apply to database**, as shown following\. 

![\[Apply to database\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/write_to_database.png)

## The Extension Pack Schema<a name="CHAP_SchemaConversionTool.DW.SaveAndApply.Ext"></a>

The first time that you apply your converted schema to your target DB instance, AWS SCT adds an additional schema to your target DB instance\. This schema implements system functions of the source database that are required when writing your converted schema to your target DB instance\. The schema is called the extension pack schema\. 

Don't modify the extension pack schema, or you might encounter unexpected results in the converted schema that is written to your target DB instance\. When your schema is fully migrated to your target DB instance, and you no longer need AWS SCT, you can delete the extension pack schema\. 

The extension pack schema is named according to your source database as follows: 

+ Greenplum: `AWS_GREENPLUM_EXT`

+ Microsoft SQL Server: `AWS_SQLSERVER_EXT`

+ Netezza: `AWS_NETEZZA_EXT`

+ Oracle: `AWS_ORACLE_EXT`

+ Teradata: `AWS_TERADATA_EXT`

+ Vertica: `AWS_VERTICA_EXT`

For more information, see [Using the AWS Schema Conversion Tool Extension Pack Custom Python Library](CHAP_SchemaConversionTool.ExtensionPack.DW.md)\. 

## Python Libraries<a name="CHAP_SchemaConversionTool.DW.SaveAndApply.Py"></a>

To create custom functions in Amazon Redshift, you use the Python language\. Use the AWS SCT extension pack to install python libraries for your Amazon Redshift database\. For more information, see [Using the AWS Schema Conversion Tool Extension Pack Custom Python Library](CHAP_SchemaConversionTool.ExtensionPack.DW.md)\. 