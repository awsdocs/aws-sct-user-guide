# Updating and Refreshing Your Converted Schema in the AWS Schema Conversion Tool<a name="CHAP_SchemaConversionTool.DW.UpdateRefresh"></a>

You can update both the source schema and the target schema in your AWS Schema Conversion Tool \(AWS SCT\) project\. 

+ **Source** – If you update the schema for your source database, AWS SCT replaces the schema in your project with the latest schema from your source database\. Using this functionality, you can update your project if changes have been made to the schema of your source database\. 

   

+ **Target** – If you update the schema for your target database, AWS SCT replaces the schema in your project with the latest schema from your target database\. If you haven't applied any schema to your target database, AWS SCT clears the converted schema from your project\. You can then convert the schema from your source database for a clean target database\. 

   

You update the schema in your AWS SCT project by choosing **Refresh from Database**, as shown following\. 

![\[Refresh the schema from the source database\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/refresh_from_source_database.png)