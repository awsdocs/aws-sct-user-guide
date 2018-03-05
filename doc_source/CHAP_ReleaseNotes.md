# Release Notes for the AWS Schema Conversion Tool<a name="CHAP_ReleaseNotes"></a>

## Release Notes for the AWS Schema Conversion Tool Build 612<a name="CHAP_ReleaseNotes.612"></a>

The following table shows the features and bug fixes for the AWS Schema Conversion Tool \(AWS SCT\) version 1\.0\.612\.


| New feature or enhancement | Description | 
| --- | --- | 
|  Custom Data Type Mapping  |  You can now set up mapping rules to change the data type for storage objects\. You define what data type should be changed in Mapping Rules tab\.   | 
|  What's New option added  |  A new "What's New" option under the Help menu shows you all major features that were added for this release\.  | 
|  Schema Compare Added Oracle 10 Support  |  You can now run Schema Compare with Oracle 10\.  | 
|  Oracle to PostgreSQL Conversion\.   |  The migration from Oracle to PostgreSQL now supports  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/CHAP_ReleaseNotes.html)  | 
|  Added support for loading some PostgreSQL function attributes and domain constraints  |  Added support for loading PostgreSQL IMMUTABLE, STABLE, and VOLATILE function attributes\.  Added support for loading PostgreSQL domain constraints\.  | 


**Issues Resolved**  

| Date reported | Description | 
| --- | --- | 
| post version 611 |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/CHAP_ReleaseNotes.html)  | 

## Release Notes for the AWS Schema Conversion Tool Build 611<a name="CHAP_ReleaseNotes.611"></a>

The following table shows the features and bug fixes for the AWS Schema Conversion Tool \(AWS SCT\) version 1\.0\.611\.


| New feature or enhancement | Description | 
| --- | --- | 
|  Schema Compare for MySQL to MySQL  |  Added the ability to compare MySQL to MySQL databases\. For more information, see [ Comparing Database Schemas](http://docs.aws.amazon.com/dms/latest/userguide/CHAP_Converting.SchemaCompare.html)\.   | 
|  Oracle to PostgreSQL dynamic statements conversion  |  Added first version of DBMS\_SQL package conversion support\. For more information, see [ Converting Dynamic SQL for Oracle to PostgreSQL Migrations](http://docs.aws.amazon.com/dms/latest/userguide/CHAP_Converting.DynamicSQL.html)\.  | 
|  Oracle to PostgreSQL GOTO statement conversion  |  PostgreSQL doesn't support the GOTO operator in functionality such as Oracle, but it can be converted using BEGIN/END or LOOP/END loop statements\.   | 
|  Open log file from error message  |  When you encounter an error, you can click on it and have it take you to the associated log file rather than having to search around on the source system for it\.  | 
|  Added Estimated Complexity field to PDF export of Assessment Report  |  The Estimated Complexity field is exported in the \.pdf version of the Assessment report, but it is not included in the \.csv version\. For more information, see [ Creating and Using the Assessment Report in the AWS Schema Conversion Tool](http://docs.aws.amazon.com/dms/latest/userguide/CHAP_SchemaConversionTool.RedshiftOpt.html)\.   | 
|  OLAP Data Migration\. Added option to not delete files on S3 after Redshift copy  |  After a migration to Amazon Redshift, the agent can either keep or delete the uploaded files\. For more information, see [ Optimizing Amazon Redshift by Using the AWS Schema Conversion Tool ](http://docs.aws.amazon.com/dms/latest/userguide/CHAP_SchemaConversionTool.RedshiftOpt.html)\.  | 
|  OLAP Data Migration\. Added LOB migration support for Greenplum, Vertica, Netezza, and Microsoft SQL Server\.  |  Added ability to migrate LOB columns\. For more information, see [ Migrating LOBs to Amazon Redshift](http://docs.aws.amazon.com/dms/latest/userguide/Agents.DW.html#Agents.DW.LOBs)\.  | 
| Added ability to see related objects for conversions such as Oracle to MySQL or Aurora for MySQL and Microsoft SQL to MySQL or Aurora for MySQL\. | When AWS SCT transforms source object into multiple target objects, you can now see a full list of related objects that were created\. For more information, see [ Finding Related Transformed Objects ](http://docs.aws.amazon.com/dms/latest/userguide/CHAP_Converting.RelatedObjects.html) \. | 
| OLAP Data Extractors\. Added possibility to recover agent after reinstall | During installation or configuration, you can recover the agent if port or location changed\. For more information, see [ Hiding and Recovering Information for an AWS SCT Agent ](http://docs.aws.amazon.com/dms/latest/userguide/Agents.DW.html#Agents.DW.Recovering)\. | 
| Ability to hide schemas in tree view | You can decide what objects and information in your schemas you want to view in tree view\. For more information, see [Hiding Schemas in the AWS SCT Tree View ](http://docs.aws.amazon.com/dms/latest/userguide/CHAP_SchemaConversionTool.UI.html#CHAP_SchemaConversionTool.HidingSchemas)\. | 
| Supports virtual partitioning | You can now manage large non\-partitioned tables by creating subtasks that create virtual partitions of the table data using filtering rules\. For more information, see [ Using Virtual Partitioning with AWS Schema Conversion Tool ](http://docs.aws.amazon.com/dms/latest/userguide/Agents.DW.html#Agents.DW.VirtualPartitioning)\. | 


**Issues Resolved**  

| Date reported | Description | 
| --- | --- | 
| post version 608 |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/CHAP_ReleaseNotes.html) | 