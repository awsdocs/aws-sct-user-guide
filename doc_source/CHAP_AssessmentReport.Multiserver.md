# Creating a multiserver assessment report for database migration<a name="CHAP_AssessmentReport.Multiserver"></a>

To determine the best target direction for your overall environment, create a multiserver assessment report\. 

A *multiserver assessment report* evaluates multiple servers based on input that you provide for each schema definition that you want to assess\. Your schema definition contains database server connection parameters and the full name of each schema\. After assessing each schema, AWS SCT produces a summary, aggregated assessment report for database migration across your multiple servers\. This report shows the estimated complexity for each possible migration target\.

You can use AWS SCT to create a multiserver assessment report for the following source and target databases\.


| Source database | Target database | 
| --- | --- | 
|  Amazon Redshift  |  Amazon Redshift  | 
|  Greenplum  |  Amazon Redshift  | 
|  IBM Db2 LUW  |  Amazon Aurora MySQL\-Compatible Edition \(Aurora MySQL\), Amazon Aurora PostgreSQL\-Compatible Edition \(Aurora PostgreSQL\), MariaDB, MySQL, PostgreSQL  | 
|  Microsoft Azure SQL  |  Aurora MySQL, Aurora PostgreSQL, MySQL, PostgreSQL  | 
|  Microsoft SQL Server  |  Aurora MySQL, Aurora PostgreSQL, Amazon Redshift, MariaDB, Microsoft SQL Server, MySQL, PostgreSQL  | 
|  MySQL  |  Aurora PostgreSQL, MySQL, PostgreSQL  | 
|  Netezza  |  Amazon Redshift  | 
|  Oracle  |  Aurora MySQL, Aurora PostgreSQL, Amazon Redshift, MariaDB, MySQL, Oracle, PostgreSQL  | 
|  PostgreSQL  |  Aurora MySQL, Aurora PostgreSQL, MySQL, PostgreSQL  | 
|  SAP ASE  |  Aurora MySQL, Aurora PostgreSQL, MariaDB, MySQL, PostgreSQL  | 
|  Snowflake  |  Amazon Redshift  | 
|  Teradata  |  Amazon Redshift  | 
|  Vertica  |  Amazon Redshift  | 

## Performing a multiserver assessment<a name="CHAP_AssessmentReport.Multiserver.Procedure"></a>

Use the following procedure to perform a multiserver assessment with AWS SCT\. You don't need to create a new project in AWS SCT to perform a multiserver assessment\. Before you get started, make sure that you have prepared a comma\-separated value \(CSV\) file with database connection parameters\. 

**To perform a multiserver assessment and create an aggregated summary report**

1. In AWS SCT, choose **File**, **New multiserver assessment**\. The **New multiserver assessment** dialog box opens\.  
![\[New multiuser assessment access\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/new_assess_screen_v3.png)

1. Choose **Download a connections file example** to download an empty template of a CSV file with database connection parameters\.

1. Enter values for **Project name**, **Location** \(to store reports\), and **Connections file** \(a CSV file\)\.

1. Choose **Run**\. 

   A progress bar appears indicating the pace of database assessment\. The number of target engines can affect the assessment runtime\. 

1. Choose **Yes** if the following message is displayed: **Full analysis of all Database servers may take some time\. Do you want to proceed?**

   When the multiserver assessment report is done, a screen appears indicating so\.

1. Choose **Open Report** to view the aggregated summary assessment report\.

## Preparing an input CSV file<a name="CHAP_AssessmentReport.Multiserver.Input"></a>

To provide connection parameters as input for multiserver assessment report, use a CSV file as shown in the following example\.

```
Name,Description,Server IP,Port,Service Name,SID,Source Engine,Schema Names,Login,Password,Target Engines
Sales,,192.0.2.0,1521,pdb,,ORACLE,Q4_2021;FY_2021,user,password,POSTGRESQL;AURORA_POSTGRESQL
Marketing,,ec2-a-b-c-d.eu-west-1.compute.amazonaws.com,1433,,target_audience,MSSQL,customers.dbo,user,password,AURORA_MYSQL
Analytics,,198.51.100.0,8195,,STATISTICS,DB2LUW,BI_REPORTS,user,password,POSTGRESQL
Products,,203.0.113.0,8194,,products_db,TERADATA,new_products,user,password,REDSHIFT
```

The example preceding uses a semicolon to separate the two schema names for the `Sales` database\. It also uses a semicolon to separate the two target database migration platforms for the `Sales` database\.

You can create a new CSV file or download a template for a CSV file from AWS SCT and fill in the required information\. Make sure that the first row of your CSV file includes the same column names as shown in the preceding example\.

**To download a template of the input CSV file**

1. Start AWS SCT\.

1. Choose **File**, then choose **New multiserver assessment**\.

1. Choose **Download a connections file example**\.

Make sure that your CSV file includes the following values, provided by the template:  
+ **Name** – The text label that helps identify your database\. AWS SCT displays this text label in the assessment report\.
+ **Description** – An optional value, where you can provide additional information about the database\.
+ **Server IP** – The Domain Name Service \(DNS\) name or IP address of your source database server\. 
+ **Port** – The port used to connect to your source database server\.
+ **Service Name** – If you use a service name to connect to your Oracle database, the name of the Oracle service to connect to\. 
+ **SID** – The database name\. For Oracle databases, use the Oracle System ID \(SID\)\.
+ **Source Engine** – The type of your source database\. Use one of the following values:
  + **AZURE\_MSSQL** for a Microsoft Azure SQL database\.
  + **DB2LUW** for an IBM Db2 LUW database\.
  + **GREENPLUM** for a Greenplum database\.
  + **MSSQL** for a Microsoft SQL Server database\.
  + **MYSQL** for a MySQL database\.
  + **NETEZZA** for a Netezza database\.
  + **ORACLE** for an Oracle database\.
  + **POSTGRESQL** for a PostgreSQL database\.
  + **REDSHIFT** for an Amazon Redshift database\.
  + **SNOWFLAKE** for a Snowflake database\.
  + **SYBASE\_ASE** for an SAP ASE database\.
  + **TERADATA** for a Teradata database\.
  + **VERTICA** for a Vertica database\.
+ **Schema Names** – The names of the database schemas to include in the assessment report\.

  For Microsoft Azure SQL, Microsoft SQL Server, Netezza, SAP ASE, and Snowflake, use the following format of the schema name:

  `db_name.schema_name`

  Replace `db_name` with the name of the source database\.

  Replace `schema_name` with the name of the source schema\.

  Separate multiple schema names by using semicolons like this: `Schema1;Schema2`\.
+ **Login** – The user name to connect to your source database server\.
+ **Password** – The password to connect to your source database server\.
+ **Target Engines** – The target database platforms\. Use the following values to specify one or more targets in the assessment report:
  + **AURORA\_MYSQL** for an Aurora MySQL\-Compatible database\.
  + **AURORA\_POSTGRESQL** for an Aurora PostgreSQL\-Compatible database\.
  + **MARIA\_DB** for a MariaDB database\.
  + **MSSQL** for a Microsoft SQL Server database\.
  + **MYSQL** for a MySQL database\.
  + **ORACLE** for an Oracle database\.
  + **POSTGRESQL** for a PostgreSQL database\.
  + **REDSHIFT** for an Amazon Redshift database\.

  Separate multiple targets by using semicolons like this: `MYSQL;MARIA_DB`\. The number of targets affects the time it takes to run the assessment\.

## Locating and viewing reports<a name="CHAP_AssessmentReport.Multiserver.Review"></a>

The multiserver assessment generates two types of reports: 
+ An aggregated report of all source databases\.
+ A detailed assessment report of target databases for each schema name in a source database\. 

Reports are stored in the directory that you chose for **Location** in the **New multiserver assessment** dialog box\.

To access the detailed reports, you can navigate the subdirectories, which are organized by source database, schema name, and target database engine\.

Aggregated reports show information in four columns about conversion complexity of a target database\. The columns include information about conversion of code objects, storage objects, syntax elements, and conversion complexity\. 

The following example shows information for conversion of two Oracle database schemas to Amazon RDS for PostgreSQL\. 

![\[Aggregate report one target\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/aggregate_rpt5.png)

The same four columns are appended to the reports for each additional target database engine specified\.

For details on how to read this information, see following\.  

## Output for an aggregated assessment report<a name="CHAP_AssessmentReport.Multiserver.Agreggated"></a>

The aggregated multiserver database migration assessment report in AWS Schema Conversion Tool is a CSV file with the following columns: 
+ `Server IP`
+ `Name`
+ `Description`
+ `Schema Name`
+ `Code object conversion % for target_database`
+ `Storage object conversion % for target_database`
+ `Syntax elements conversion % for target_database`
+ `Conversion complexity for target_database`

To gather information, AWS SCT runs full assessment reports and then aggregates reports by schemas\.

In the report, the following three fields show the percentage of possible automatic conversion based on the assessment: 

**Code object conversion % **  
The percentage of code objects in the schema that AWS SCT can convert automatically or with minimal change\. Code objects include procedures, functions, views, and similar\.

**Storage object conversion % **  
The percentage of storage objects that SCT can convert automatically or with minimal change\. Storage objects include tables, indexes, constraints, and similar\.

**Syntax elements conversion % **  
The percentage of syntax elements that SCT can convert automatically\. Syntax elements include `SELECT`, `FROM`, `DELETE`, and `JOIN` clauses, and similar\.

The conversion complexity calculation is based on the notion of action items\. An *action item* reflects a type of problem found in source code that you need to fix manually during migration to a particular target\. An action item can have multiple occurrences\.

A weighted scale identifies the level of complexity for performing a migration\. The number 1 represents the lowest level of complexity, and the number 10 represents the highest level of complexity\.