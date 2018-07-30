# Release Notes for the AWS Schema Conversion Tool<a name="CHAP_ReleaseNotes"></a>

## Release Notes for the AWS Schema Conversion Tool Build 617<a name="CHAP_ReleaseNotes.617"></a>

The following table shows the features and bug fixes for the AWS Schema Conversion Tool \(AWS SCT\) version 1\.0\.617\.


| New feature or enhancement | Description | 
| --- | --- | 
|  Oracle to Amazon RDS for Oracle \- Oracle server level objects  |  AWS SCT adds support for user profiles, user roles, event schedules, and more\. For more information, see [ Converting Oracle to Amazon RDS for Oracle](CHAP_Source.Oracle.ToRDSOracle.md)\.  | 
|  SQL Server to Amazon RDS for SQL Server \- Assessment report includes additional metrics  |  The AWS SCT assessment report includes information on the Amazon RDS DB instance as well as SQL Server services in use by the source database\. For more information, see [ Converting SQL Server to Amazon RDS for SQL Server](CHAP_Source.SQLServer.ToRDSSQLServer.md)\.  | 
| Oracle to Amazon RDS for Oracle \- Assessment report includes additional metrics | The AWS SCT assessment report includes information on the Amazon RDS DB instance as well as Oracle services in use by the source database\. For more information, see [ Converting Oracle to Amazon RDS for Oracle](CHAP_Source.Oracle.ToRDSOracle.md)\. | 
|  Oracle to PostgreSQL 10 \- timestamp without time zone columns  |  AWS SCT supports timestamp without time zone columns\.  | 
|  Oracle to PostgreSQL 10 \- Row ID columns  | You can convert ROWID pseudocolumns to data columns\. For more information, see [Converting Oracle ROWID to PostgreSQL](CHAP_Source.Oracle.ToPostgreSQL.md#CHAP_Source.Oracle.ToPostgreSQL.ConvertRowID)\. | 
|  SQL Server to PostgreSQL \- Merge statement emulation   |  AWS SCT converts the MERGE statement when migrating to PostgreSQL\. For more information, see [ Using Microsoft SQL Server as a Source for AWS Schema Conversion Tool \(AWS SCT\)](CHAP_Source.SQLServer.md)\.  | 
|  Oracle to MySQL \- SELECT and WITH clause  |  AWS SCT converts a WITH clause when migrating to MySQL\. For more information, see [ Converting Oracle to Amazon RDS for MySQL or Amazon Aurora \(MySQL\)](CHAP_Source.Oracle.ToMySQL.md)  | 
|  SQL Server to MySQL \- Extension pack  |  The AWS SCT extension pack emulates several functions including ISDATE, FORMAT, PATINDEX, and CONVERT\.   | 
|  SQL Server to PostgreSQL \- user\-defined table types  |  You can use user\-defined table types to specify table structures\. For more information, see [ Using Microsoft SQL Server as a Source for AWS Schema Conversion Tool \(AWS SCT\)](CHAP_Source.SQLServer.md)\.  | 
|  Oracle \- Saving SQL for source tree creation   |  You can save the SQL statements that AWS SCT generates to create the source tree\.   | 

Issues Resolved
+ Improvements to the assessment report for server\-level objects\.
+ Fixed incorrect processing of objects ending with END block\.
+ Added assessment report generation date in the PDF file\.
+ Added logic to script generation for multiple files on Save as SQL option\.

## Release Notes for the AWS Schema Conversion Tool Build 616<a name="CHAP_ReleaseNotes.616"></a>

The following table shows the features and bug fixes for the AWS Schema Conversion Tool \(AWS SCT\) version 1\.0\.616\.


| New feature or enhancement | Description | 
| --- | --- | 
|  SQL Server to PostgreSQL \- SUSER\_SNAME support  |  AWS SCT adds support for converting SUSER\_SNAME\. For more information, see [ Converting SQL Server to PostgreSQL](CHAP_Source.SQLServer.ToPostgreSQL.md)\.  | 
|  SQL Server to PostgreSQL \- Table\-valued functions support  |  AWS SCT adds support for converting table\-valued functions\. For more information, see [ Converting SQL Server to PostgreSQL](CHAP_Source.SQLServer.ToPostgreSQL.md)\.  | 
| Oracle to Amazon RDS for Oracle \- Oracle jobs | AWS SCT adds support for many types of Oracle jobs in Amazon RDS for Oracle\. | 
|  Oracle to Amazon RDS for Oracle \- Oracle RAC  |  Amazon RDS for Oracle doesn't support Oracle RAC\. Consider using a Multi\-AZ deployment on an Amazon RDS instance for high availability\.  | 
|  Oracle to Amazon RDS for Oracle \- Oracle Data Guard and Active Data Guard  | Amazon RDS for Oracle doesn't support Oracle Data Guard and Active Data Guard\. Consider using a Multi\-AZ deployment on an Amazon RDS instance for high availability\. | 
|  Oracle to Amazon RDS for Oracle \- ongoing replication   |  Amazon RDS for Oracle doesn't support ongoing replication\. You can use AWS Database Migration Service if you need to have ongoing replication to a target on Amazon RDS\.  | 
|  Oracle to Amazon RDS for Oracle \- auditing  |  Amazon RDS for Oracle doesn’t support Oracle Unified Auditing\. Amazon RDS for Oracle supports traditional auditing and fine\-grained auditing \(DBMS\_FGA package\)\.   | 
|  Oracle to Amazon RDS for Oracle \- schedule objects  |  AWS SCT supports converting Oracle DBMS\_SCHEDULER objects when migrating to Amazon RDS for Oracle\.   | 
|  SQL Server to MySQL \- table\-valued functions  |  MySQL doesn't support multi\-statement table\-valued functions\. AWS SCT simulates table\-valued functions during a conversion by creating temporary tables\. For more information, see [ Using Microsoft SQL Server as a Source for AWS Schema Conversion Tool \(AWS SCT\)](CHAP_Source.SQLServer.md)\.  | 
|  AWS SCT assessment report updates   |  The AWS SCT assessment report updates include the following:  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/CHAP_ReleaseNotes.html)  | 
|  SQL Server to Amazon RDS for SQL Server \- Service Broker and endpoints  |  Amazon RDS currently does not support Service Broker or additional T\-SQL endpoints that use the CREATE ENDPOINT command\. For more information, see [ Using Microsoft SQL Server as a Source for AWS Schema Conversion Tool \(AWS SCT\)](CHAP_Source.SQLServer.md)\.  | 
|  Db2 LUW to PostgreSQL 10 \- partitioned tables  |  AWS SCT can convert Db2 LUW tables to partitioned tables in PostgreSQL 10\.  | 

Issues Resolved
+ Db2 LUW to Amazon RDS for MySQL or Amazon Aurora \(MySQL\)\. Added ability to show target SQL for several transformed related objects\.
+ Db2 LUW to Amazon RDS for PostgreSQL or Amazon Aurora \(PostgreSQL\)\. Added ability to show target SQL for several transformed related objects\.
+ MySQL to Amazon RDS for PostgreSQL or Amazon Aurora \(PostgreSQL\)\. Added ability to show target SQL for several transformed related objects\.
+ OLAP\. Added ability to show target SQL for several transformed related objects\.
+ AWS SCT issue with MySQL to MySQL conversion fixed\.

  \.

## Release Notes for the AWS Schema Conversion Tool Build 615<a name="CHAP_ReleaseNotes.615"></a>

The following table shows the features and bug fixes for the AWS Schema Conversion Tool \(AWS SCT\) version 1\.0\.615\.


| New feature or enhancement | Description | 
| --- | --- | 
|  SQL Server to MySQL \- Support for MERGE statement  |  MySQL does not support the MERGE statement, but AWS SCT can emulate the statement by using the INSERT ON DUPLICATE KEY clause and the UPDATE FROM and DELETE FROM statements\. For more information, see [ Converting SQL Server to MySQL](CHAP_Source.SQLServer.ToMySQL.md)\.  | 
|  SQL Server to PostgreSQL \- Support for creating unique index names  |  AWS SCT gives you the option of generating unique index names if your index names are not unique\. To do this, choose the option **Generate unique index names** in the project properties\. For more information, see [ Converting SQL Server to PostgreSQL](CHAP_Source.SQLServer.ToPostgreSQL.md)\.  | 
|  Oracle to PostgreSQL \- Prevent overlapping database sequence values  |  For Oracle to PostgreSQL migration projects, choose the option **Populate converted sequences with the last values generated on the source side** in the Conversion settings tab of Project Settings\. For more information, see [ Converting Oracle to Amazon RDS for PostgreSQL or Amazon Aurora \(PostgreSQL\)](CHAP_Source.Oracle.ToPostgreSQL.md)\.  | 
|  Oracle to PostgreSQL \- Support for PostgreSQL 10 partitioning  | AWS SCT can emulate partitions and subpartitions when converting a schema from an Oracle database to a PostgreSQL database\. For more information, see [ Converting Oracle to Amazon RDS for PostgreSQL or Amazon Aurora \(PostgreSQL\)](CHAP_Source.Oracle.ToPostgreSQL.md)\. | 
|  SQL Server to PostgreSQL \- Support for PostgreSQL 10 partitioning   |  AWS SCT can emulate partitions and subpartitions when converting a schema from an SQL Server database to a PostgreSQL database\. For more information, see [ Converting SQL Server to PostgreSQL](CHAP_Source.SQLServer.ToPostgreSQL.md)\.  | 
|  SQL Server to MySQL \- Support for GOTO statement  |  MySQL does not use a GOTO statement\. When AWS SCT converts code that contains the GOTO statement, it converts the statement to use a BEGIN…END or LOOP…END LOOP statement\.   | 
|  SQL Server to PostgreSQL \- Support for GOTO statement  |  PostgreSQL does not use a GOTO statement\. When AWS SCT converts code that contains the GOTO statement, it converts the statement to use a BEGIN…END or LOOP…END LOOP statement\.   | 
|  Oracle to PostgreSQL \- Support for GOTO statement  |  PostgreSQL does not use a GOTO statement\. When AWS SCT converts code that contains the GOTO statement, it converts the statement to use a BEGIN…END or LOOP…END LOOP statement\. | 
|  DB2 LUW to PostgreSQL \- Support for triggers from DB2 to PostgreSQL  |  AWS SCT can convert the various TRIGGER statements used with DB2 LUW\. For more information, see [ Converting DB2 LUW to Amazon RDS for PostgreSQL or Amazon Aurora \(PostgreSQL\)](CHAP_Source.DB2LUW.ToPostgreSQL.md)  | 
|  SQL Server to Amazon RDS for SQL Server \- Support for database level triggers  |  AWS SCT can add database triggers to the object tree when Amazon RDS for SQL Server is the target\.  | 
|  SQL Server to Amazon RDS for SQL Server \- Support for server\-level triggers, linked servers, and SQL Server Agents  |  AWS SCT now supports server\-level triggers, linked servers, and SQL Server Agents\. For more information, see [ Using Microsoft SQL Server as a Source for AWS Schema Conversion Tool \(AWS SCT\)](CHAP_Source.SQLServer.md)\.  | 
|  Oracle to Amazon RDS for Oracle \- Support for directory objects, tablespaces, and user roles and privileges  |  AWS SCT can add directory objects to the object tree\. For more information, see [ Using Microsoft SQL Server as a Source for AWS Schema Conversion Tool \(AWS SCT\)](CHAP_Source.SQLServer.md)\.  | 
|  Db2 support version 10\.1  |  AWS SCT now supports IBM Db2 LUW version 10\.1\.  | 
|  Added support of isolated government regions  |  AWS SCT now supports isolated government regions\.  | 

Issues Resolved
+ AWS Profile\. Working with federated credentials\.
+ DB2 to PostgreSQL\. Conversion of DB2 triggers\.
+ OLAP Migration\. Current Project Settings \- Skewed Threshold Value\. Changed percent support\.
+ Assessment Report\. Flag LOB tables without Primary Key\.
+ Some UI bugs were fixed\.

## Release Notes for the AWS Schema Conversion Tool Build 614<a name="CHAP_ReleaseNotes.614"></a>

The following table shows the features and bug fixes for the AWS Schema Conversion Tool \(AWS SCT\) version 1\.0\.614\.


| New feature or enhancement | Description | 
| --- | --- | 
|  Oracle to PostgreSQL: Assessment Report for SQL\*Plus Conversion  |  AWS SCT can convert SQL\*Plus files into PSQL\. The assessment report shows how AWS SCT converted the SQL\*Plus files into PSQL\. For more information, see [ Using Oracle as a Source for AWS Schema Conversion Tool \(AWS SCT\)](CHAP_Source.Oracle.md)\.  | 
|  Aurora MySQL Compatible 5\.7 version support   |  Added support for converting Aurora MySQL 5\.7 schemas\.  | 
|  Db2 LUW 9\.1  |  Added support for Db2 LUW version 9\.1\.  | 
|  OLTP Data Migration\. Data compression\.   |  Data compression during migration is now optional when you set up a task using a Replication agent\.  | 
|  Oracle to Oracle RDS: DB Links support   |  Oracle to Oracle RDS migrations now support DB Links\. For more information, see [ Using Oracle as a Source for AWS Schema Conversion Tool \(AWS SCT\)](CHAP_Source.Oracle.md)\.  | 
|  Oracle to PostgreSQL: SELECT INTO BULK COLLECT \(VARRAY\) conversion  |  SQL statements using BULK COLLECT \(VARRAY\) can now be converted when migrating between Oracle and PostgreSQL\.  | 
|  Oracle comments conversion  |  Added support for converting Oracle comments into the format used by the target database engine\. For more information, see [ Using Oracle as a Source for AWS Schema Conversion Tool \(AWS SCT\)](CHAP_Source.Oracle.md)\.  | 
|  Emulation of Oracle system objects  |  Added support for converting Oracle system objects into PostgreSQL\. For more information, see [ Using Oracle as a Source for AWS Schema Conversion Tool \(AWS SCT\)](CHAP_Source.Oracle.md)\. | 
|  Oracle to PostgreSQL: ROWNUM converted to LIMIT   |  Added support for converting ROWNUM\.  | 
|  Microsoft SQL Server to Microsoft SQL Server RDS: BULK INSERT and OPENROWSET\(\)  |  Added support converting BULK INSERT and OPENROWSET\(\)  | 
|  Microsoft SQL Server to Microsoft SQL Server RDS: Links inside storage objects   |  AWS SCT now supports links inside stored objects during a migration to Amazon RDS\. For more information, see [ Using Microsoft SQL Server as a Source for AWS Schema Conversion Tool \(AWS SCT\)](CHAP_Source.SQLServer.md)\.  | 
|  Microsoft SQL Server to PostgreSQL: PATINDEX  |  AWS SCT now supports converting PATINDEX during a migration to PostgreSQL\. For more information, see [ Using Microsoft SQL Server as a Source for AWS Schema Conversion Tool \(AWS SCT\)](CHAP_Source.SQLServer.md)\.  | 
|  Microsoft SQL Server to PostgreSQL: System objects access  |  SQL Server system object are now converted to objects in PostgreSQL\. For more information, see [ Using Microsoft SQL Server as a Source for AWS Schema Conversion Tool \(AWS SCT\)](CHAP_Source.SQLServer.md)\.  | 
|  Microsoft SQL Server to PostgreSQL: Inline function creation  |  Added support for inline functions\. For more information, see [ Using Microsoft SQL Server as a Source for AWS Schema Conversion Tool \(AWS SCT\)](CHAP_Source.SQLServer.md)\.  | 

Issues Resolved
+ Type Mapping\. Bug fixing and improvements\.
+ OLAP Conversion\. Optimization strategies\. Ability to reset strategies fixed\.
+ Oracle to PostgreSQL\. Dynamic SQL Conversion bug fixing and improvements
+ SQL\*Plus script conversion\. Bug fixing and improvements
+ Oracle to PostgreSQL Conversion\. Bind variables recognition fix\.
+ Added ability to update server info by clicking "Update server info" on server level\.
+ Netezza\. Schema conversion for objects in lower\-case fixed\.
+ Handling some specific characters in the AWS SCT navigation tree nodes' names derived from file names
+ Some UI bugs were fixed\.

## Release Notes for the AWS Schema Conversion Tool Build 613<a name="CHAP_ReleaseNotes.613"></a>

The following table shows the features and bug fixes for the AWS Schema Conversion Tool \(AWS SCT\) version 1\.0\.613\.


| New feature or enhancement | Description | 
| --- | --- | 
|  DB2 LUW support  |  Added support for migrating a DB2 database as a source\. For more information, see [Converting Database Schemas Using the AWS Schema Conversion Tool](CHAP_Converting.md)\.  | 
|  Oracle to PostgreSQL Conversion\. Added SQL\*Plus files conversion  |  You can now convert SQL\*Plus files\.  | 
|  Snowball Tab added for OLTP Data Migration  |  A new Snowball tab was added for OLTP Data Migration that shows you the current status of a Snowball device for particular project\. For more information, see [Using Data Extraction Agents](CHAP_Agents.DW.md)\.  | 
|  Oracle To PostgreSQL Conversion\. Convert Oracle spatial code to PostGIS  |  Oracle To PostgreSQL Conversion\. Oracle spatial code converts to PostGIS\.  | 
|  Schema Compare Added Oracle 10 Support  |  You can now run Schema Compare with Oracle 10\. For more information, see [Comparing Database Schemas](CHAP_Converting.SchemaCompare.md)  | 
|  Oracle to PostgreSQL Conversion\. Implicit typecasting of Oracle db handled in PostgresSQL  |  While converting from Oracle to PostgreSQL, SCT add datatype casting\.  | 
|  SQL Server, Windows Authentication  |  SQL Server\. Windows Authentication connection method support added\.  | 
|  SQL Server To PostgreSQL Conversion   |  Added CITEXT type support\. Now you can choose it with data type `mappint`\. | 
|  Oracle to PostgreSQL Conversion   |  Additional improvements of Dynamic SQL Conversion for EXECUTE IMMEDIATE and DBMS\_SQL and Cursors\.  | 
|  Oracle to PostgreSQL Conversion   |  Added support of SELECT INTO BULK COLLECT Conversion for Oracle to PostgreSQL\.  | 
|  Oracle to PostgreSQL Conversion  |  Now it is possible to convert an Associative array from Oracle to PostgreSQL\.  | 
|  Type Mapping \- Custom type mapping improvements  |  Added ability to select source data types based on length and precision\.  | 
|  AWS Profile Settings  |  Added ability to select default profile in AWS Profile Settings\.   | 
|  Greenplum to Redshift Conversion  |  BuiltIn SQL Functions to Redshift Scalar SQL UDF conversion added\.  | 


**Issues Resolved**  

| Date reported | Description | 
| --- | --- | 
| post version 612 |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/CHAP_ReleaseNotes.html)  | 

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
|  Added Estimated Complexity field to PDF export of Assessment Report  |  The Estimated Complexity field is exported in the \.pdf version of the Assessment report, but it is not included in the \.csv version\. For more information, see [ Creating and Using the Assessment Report in the AWS Schema Conversion Tool](http://docs.aws.amazon.com/dms/latest/userguide/CHAP_Converting.DW.RedshiftOpt.html)\.   | 
|  OLAP Data Migration\. Added option to not delete files on S3 after Redshift copy  |  After a migration to Amazon Redshift, the agent can either keep or delete the uploaded files\. For more information, see [ Optimizing Amazon Redshift by Using the AWS Schema Conversion Tool ](http://docs.aws.amazon.com/dms/latest/userguide/CHAP_Converting.DW.RedshiftOpt.html)\.  | 
|  OLAP Data Migration\. Added LOB migration support for Greenplum, Vertica, Netezza, and Microsoft SQL Server\.  |  Added ability to migrate LOB columns\. For more information, see [ Migrating LOBs to Amazon Redshift](http://docs.aws.amazon.com/dms/latest/userguide/Agents.DW.html#Agents.DW.LOBs)\.  | 
| Added ability to see related objects for conversions such as Oracle to MySQL or Aurora for MySQL and Microsoft SQL to MySQL or Aurora for MySQL\. | When AWS SCT transforms source object into multiple target objects, you can now see a full list of related objects that were created\. For more information, see [ Finding Related Transformed Objects ](http://docs.aws.amazon.com/dms/latest/userguide/CHAP_Converting.RelatedObjects.html) \. | 
| OLAP Data Extractors\. Added possibility to recover agent after reinstall | During installation or configuration, you can recover the agent if port or location changed\. For more information, see [ Hiding and Recovering Information for an AWS SCT Agent ](http://docs.aws.amazon.com/dms/latest/userguide/Agents.DW.html#Agents.DW.Recovering)\. | 
| Ability to hide schemas in tree view | You can decide what objects and information in your schemas you want to view in tree view\. For more information, see [Hiding Schemas in the AWS SCT Tree View ](http://docs.aws.amazon.com/dms/latest/userguide/CHAP_.HidingSchemas)\. | 
| Supports virtual partitioning | You can now manage large non\-partitioned tables by creating subtasks that create virtual partitions of the table data using filtering rules\. For more information, see [Using Virtual Partitioning with AWS Schema Conversion Tool](CHAP_Agents.DW.md#CHAP_Agents.DW.VirtualPartitioning)\. | 


**Issues Resolved**  

| Date reported | Description | 
| --- | --- | 
| post version 608 |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/CHAP_ReleaseNotes.html) | 