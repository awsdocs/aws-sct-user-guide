# Working with Data Warehouses<a name="WorkingWith.DW"></a>

You can use the AWS Schema Conversion Tool \(AWS SCT\) to convert your existing data warehouse schema\. Your converted schema is suitable for an Amazon Redshift cluster\. 

In some cases, source database features can't be converted to equivalent Amazon Redshift features\. The AWS SCT Extension Pack contains a custom Python library that emulates some source database functionality on Amazon Redshift\. 

You can use data extraction agents to extract data from your data warehouse to prepare to migrate it to Amazon Redshift\. To manage the data extraction agents, you can use AWS SCT\. For more information, see [Using Data Extraction Agents](Agents.DW.md)\. 

You can use AWS SCT to optimize your existing Amazon Redshift database\. AWS SCT recommends sort keys and distribution keys to optimize your database\. 

Following, you can find more information about these processes\. 


+ [Converting Data Warehouse Schema to Amazon Redshift by Using the AWS Schema Conversion Tool](CHAP_SchemaConversionTool.Converting.DW.md)
+ [Optimizing Amazon Redshift by Using the AWS Schema Conversion Tool](CHAP_SchemaConversionTool.RedshiftOpt.md)