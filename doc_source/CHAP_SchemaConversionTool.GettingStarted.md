# Getting Started with the AWS Schema Conversion Tool<a name="CHAP_SchemaConversionTool.GettingStarted"></a>

Following, you can find procedures that help you get started using the AWS Schema Conversion Tool \(AWS SCT\)\.


+ [Before You Begin](#CHAP_SchemaConversionTool.GettingStarted.Before)
+ [Starting the AWS Schema Conversion Tool](#CHAP_SchemaConversionTool.GettingStarted.Launching)
+ [Creating an AWS Schema Conversion Tool Project](#CHAP_SchemaConversionTool.GettingStarted.Project)
+ [Connecting to Your Source Database](#CHAP_SchemaConversionTool.Converting.CreateProject)
+ [Connecting to Your Target Database](#CHAP_SchemaConversionTool.GettingStarted.Target)
+ [Converting Your Schema](#CHAP_SchemaConversionTool.GettingStarted.Next)
+ [Required Database Privileges for Using the AWS Schema Conversion Tool](CHAP_SchemaConversionTool.GettingStarted.Privs.md)
+ [Getting Started Converting Database Schema with the AWS Schema Conversion Tool](CHAP_SchemaConversionTool.GettingStarted.Rel.md)
+ [Getting Started Converting Data Warehouse Schema with the AWS Schema Conversion Tool](CHAP_SchemaConversionTool.GettingStarted.DW.md)

AWS SCT provides a project\-based user interface\. Almost all work you do with AWS SCT starts with the following three steps:

1. Create an AWS SCT project\.

1. Connect to your source database\.

1. Connect to your target database\.

## Before You Begin<a name="CHAP_SchemaConversionTool.GettingStarted.Before"></a>

Before you complete the procedures in this topic, you must first do the following: 

+ Install the AWS Schema Conversion Tool\. For more information, see [Installing, Verifying, and Updating the AWS Schema Conversion Tool](CHAP_SchemaConversionTool.Installing.md)\. 

   

+ Create your target Amazon Relational Database Service \(Amazon RDS\) DB instance or Amazon Redshift database, if it doesn't already exist\. For more information, see the following documentation\. 

     
****    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/CHAP_SchemaConversionTool.GettingStarted.html)

+ Verify that you have sufficient privileges for the source and target databases so that you can run AWS SCT\. For more information, see [Required Database Privileges for Using the AWS Schema Conversion Tool](CHAP_SchemaConversionTool.GettingStarted.Privs.md)\. 

## Starting the AWS Schema Conversion Tool<a name="CHAP_SchemaConversionTool.GettingStarted.Launching"></a>

To start the AWS Schema Conversion Tool, use the instructions for your operating system shown following\. 


****  

| Operating System | Instructions | 
| --- | --- | 
| Fedora Linux |  Run the following command:  `/opt/AWSSchemaConversionTool/AWSSchemaConversionTool`  | 
| Microsoft Windows | Double\-click the icon for the application\. | 
| Ubuntu Linux |  Run the following command:  `/opt/AWSSchemaConversionTool/AWSSchemaConversionTool`  | 

## Creating an AWS Schema Conversion Tool Project<a name="CHAP_SchemaConversionTool.GettingStarted.Project"></a>

The following procedure shows you how to create an AWS Schema Conversion Tool project\. 

**To create your project**

1. Start the AWS Schema Conversion Tool\.

1. Choose **New Project** from the **File** menu\. The **New Project** dialog box appears\.   
![\[New Project dialog box\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/file-new-project.png)

1. Add the following preliminary project information\.   
****    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/CHAP_SchemaConversionTool.GettingStarted.html)

1. Choose **OK** to create your AWS SCT project\. 

## Connecting to Your Source Database<a name="CHAP_SchemaConversionTool.Converting.CreateProject"></a>

The following topics show you how to connect to your source database\. Choose the topic appropriate for your source database\. 

+ [Connecting to an Amazon Redshift Source Database](CHAP_SchemaConversionTool.GettingStarted.Source.Redshift.md)

+ [Connecting to a Greenplum Source Database](CHAP_SchemaConversionTool.GettingStarted.Source.Greenplum.md)

+ [Connecting to a Microsoft SQL Server Source Database](CHAP_SchemaConversionTool.GettingStarted.Source.SQLServer.md)

+ [Connecting to a Microsoft SQL Server Data Warehouse Source Database](CHAP_SchemaConversionTool.GettingStarted.Source.SQLServerDW.md)

+ [Connecting to a MySQL Source Database](CHAP_SchemaConversionTool.GettingStarted.Source.MySQL.md)

+ [Connecting to a Netezza Source Database](CHAP_SchemaConversionTool.GettingStarted.Source.Netezza.md)

+ [Connecting to an Oracle Source Database](CHAP_SchemaConversionTool.GettingStarted.Source.Oracle.md)

+ [Connecting to an Oracle Data Warehouse Source Database](CHAP_SchemaConversionTool.GettingStarted.Source.OracleDW.md)

+ [Connecting to a PostgreSQL Source Database](CHAP_SchemaConversionTool.GettingStarted.Source.Postgres.md)

+ [ Connecting to a Teradata Source Database](CHAP_SchemaConversionTool.GettingStarted.Source.Teradata.md)

+ [Connecting to a Vertica Source Database](CHAP_SchemaConversionTool.GettingStarted.Source.Vertica.md)

## Connecting to Your Target Database<a name="CHAP_SchemaConversionTool.GettingStarted.Target"></a>

The following procedure shows you how to connect to your target database\. 

**To connect to your target database**

1. Start the AWS Schema Conversion Tool\.

1. Choose **Connect to *target***, where *target* indicates the database engine for your target DB instance\. 

1. Add the following information to connect to your target Amazon RDS DB instance\.   
****    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/CHAP_SchemaConversionTool.GettingStarted.html)

1. Choose **Test Connection** to verify that you can successfully connect to your target database\. 

1. Choose **OK** to connect to your target DB instance\. 

## Converting Your Schema<a name="CHAP_SchemaConversionTool.GettingStarted.Next"></a>

After you get started by using the procedures in this topic, you can continue working with AWS SCT with transactional databases and data warehouses in the following topics: 

+ [Getting Started Converting Database Schema with the AWS Schema Conversion Tool](CHAP_SchemaConversionTool.GettingStarted.Rel.md)

+ [Getting Started Converting Data Warehouse Schema with the AWS Schema Conversion Tool](CHAP_SchemaConversionTool.GettingStarted.DW.md)