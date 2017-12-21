# Using the AWS Schema Conversion Tool Extension Pack<a name="CHAP_ExtensionPack"></a>

The AWS SCT Extension Pack is an add\-on module that emulates functions present in the source database that are required when converting objects to the target database\. Before you can install the AWS SCT Extension Pack, you need to convert your database schema\. 

The AWS SCT Extension Pack includes the following components\.

+ DB Schema \(aws\_<database engine name>\_ext\) — Includes SQL functions, procedures, and tables for emulating some OLTP and OLAP objects \(e\.g\. sequence\) or unsupported built\-in\-functions from the source database\.

+ Custom Python Library \(for select OLAP databases\) — Includes a set of Python functions that emulate unsupported built\-in database functions\. This library is for use when you migrate from one of the supported databases to Amazon Redshift\.

+ AWS Lambda Functions \(for select OLTP databases\) — Includes AWS Lambda Services functions that emulate complex database functionality such as job scheduling and sending emails\.

There are two ways to apply the AWS SCT Extension Pack\. 

+ You can manually apply the AWS SCT Extension Pack by selecting the target database and choosing **Apply Extension Pack Wizard** from the context menu\.

+ AWS SCT automatically applies the Extension Pack when you apply a target database script by choosing **ApplyToTarget** from the context menu\. AWS SCT applies the Extension Pack before it applies all other schema objects\.

Each time the AWS SCT Extension Pack is applied to a target data store, the components are overwritten\. Each component has a version number, and AWS SCT warns you if the current component version is older than the one being applied\. You can control these notifications in the **Notification Settings** in the **Global Settings** section of **Settings**\.

## Using the AWS Schema Conversion Tool Extension Pack DB Schema<a name="CHAP_ExtensionPack.Schema"></a>

When you convert your database or data warehouse schema, the AWS Schema Conversion Tool \(AWS SCT\) adds an additional schema to your target database\. This schema implements SQL system functions of the source database that are required when writing your converted schema to your target database\. The schema is called the Extension Pack schema\.

The Extension Pack schema for OLTP databases is named according to the source database as follows: 

+ Microsoft SQL Server: `AWS_SQLSERVER_EXT`

+ MySQL: `AWS_MYSQL_EXT`

+ Oracle: `AWS_ORACLE_EXT`

+ PostgreSQL: `AWS_POSTGRESQL_EXT`

The Extension Pack schema for OLAP data warehouse applications is named according to the source data store as follows: 

+ Greenplum: `AWS_GREENPLUM_EXT`

+ Microsoft SQL Server: `AWS_SQLSERVER_EXT`

+ Netezza: `AWS_NETEZZA_EXT`

+ Oracle: `AWS_ORACLE_EXT`

+ Teradata: `AWS_TERADATA_EXT`

+ Vertica: `AWS_VERTICA_EXT`