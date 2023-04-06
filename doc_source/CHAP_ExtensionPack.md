# Using AWS SCT extension packs<a name="CHAP_ExtensionPack"></a>

An *AWS SCT extension pack* is an add\-on module that emulates functions present in a source database that are required when converting objects to the target database\. Before you can install an AWS SCT extension pack, you convert your database schema\. 

Each AWS SCT extension pack includes the following components:
+ DB schema – Includes SQL functions, procedures, and tables for emulating certain online transaction processing \(OLTP\) and online analytical processing \(OLAP\) database objects such as sequences\. Also, emulates unsupported built\-in\-functions from the source database\. The name of this schema has the following format: `aws_database_engine_name_ext`\.
+ AWS Lambda functions \(for certain OLTP databases\) – Includes AWS Lambda functions that emulate complex database functionality, such as job scheduling and sending emails\. 
+ Custom libraries for OLAP databases – Includes a set of Java and Python libraries that that you can use to migrate Microsoft SQL Server Integration Services \(SSIS\) extract, transform, and load \(ETL\) scripts to AWS Glue or AWS Glue Studio\.

  Java libraries include the following modules:
  + `spark-excel_2.11-0.13.1.jar` – To emulate the functionality of Excel source and target components\.
  + `spark-xml_2.11-0.9.0.jar`, `poi-ooxml-schemas-4.1.2.jar`, and `xmlbeans-3.1.0.jar` – To emulate the functionality of the XML source component\.

  Python libraries include the following modules:
  + `sct_utils.py` – To emulate source data types and prepare parameters for the Spark SQL query\.
  + `ssis_datetime.py` – To emulate date and time built\-in functions\.
  + `ssis_null.py` – To emulate the `ISNULL` and `REPLACENULL` built\-in functions\.
  + `ssis_string.py` – To emulate string built\-in functions\.

  For more information about these libraries, see [Using custom libraries for AWS SCT extension packs](#CHAP_ExtensionPack.DW)\.

You can apply AWS SCT extension packs in two ways:
+ AWS SCT can automatically apply an extension pack when you apply a target database script by choosing **Apply to database** from the context menu\. AWS SCT applies the extension pack before it applies all other schema objects\.
+ To manually apply an extension pack, choose the target database and then choose **Apply extension pack for** from the context \(right\-click\) menu\. In most situations, automatic application is sufficient\. However, you might want to apply the pack manually if it's accidentally deleted\. 

Each time that you apply an AWS SCT extension pack to a target data store, the components are overwritten, and AWS SCT displays a notification about this\. To turn off these notifications, choose **Settings**, **Global settings**, **Notifications**, and then select **Hide the extension pack replacement alert**\.

For a conversion from Microsoft SQL Server to PostgreSQL, you can use the SQL Server to PostgreSQL extension pack in AWS SCT\. This extension pack emulates SQL Server Agent and SQL Server Database Mail\. For more information, see [Emulating SQL Server Agent in PostgreSQL with an extension pack](CHAP_Source.SQLServer.ToPostgreSQL.ExtensionPack.Agent.md) and [Emulating SQL Server Database Mail in PostgreSQL with an extension pack](CHAP_Source.SQLServer.ToPostgreSQL.ExtensionPack.Mail.md)\. 

Following, you can find more information about working with AWS SCT extension packs\. 

**Topics**
+ [Permissions for using the AWS SCT extension pack](#CHAP_ExtensionPack.Permissions)
+ [Using the extension pack schema](#CHAP_ExtensionPack.Schema)
+ [Using custom libraries for AWS SCT extension packs](#CHAP_ExtensionPack.DW)
+ [Using the AWS Lambda functions from the AWS SCT extension pack](#CHAP_ExtensionPack.OLTP)

## Permissions for using the AWS SCT extension pack<a name="CHAP_ExtensionPack.Permissions"></a>

The AWS SCT extension pack for Amazon Aurora emulates mail sending, job scheduling, queueing, and other operations using AWS Lambda functions\. When you apply the AWS SCT extension pack to your target Aurora database, AWS SCT creates a new AWS Identity and Access Management \(IAM\) role and an inline IAM policy\. Next, AWS SCT creates a new Lambda function, and configures your Aurora DB cluster for outbound connections to AWS Lambda\. To run these operations, make sure that you grant the following required permissions to your IAM user:
+ `iam:CreateRole` – to create a new IAM role for your AWS account\.
+ `iam:CreatePolicy` – to create a new IAM policy for your AWS account\.
+ `iam:AttachRolePolicy` – to attach the specified policy to your IAM role\.
+ `iam:PutRolePolicy` – to update an inline policy document that is embedded in your IAM role\.
+ `iam:PassRole` – to pass the specified IAM role to the rules engine\.
+ `iam:TagRole` – to add tags to an IAM role\.
+ `iam:TagPolicy` – to add tags to an IAM policy\.
+ `lambda:ListFunctions` – to see the list of your Lambda functions\.
+ `lambda:ListTags` – to see the list of tags of your Lambda functions\.
+ `lambda:CreateFunction` – to create a new Lambda function\.
+ `rds:AddRoleToDBCluster` – to associate an IAM role with your Aurora DB cluster\.

The AWS SCT extension pack for Amazon Redshift emulates source data warehouse base functions that are required when applying converted objects to Amazon Redshift\. Before you apply your converted code to Amazon Redshift, you must apply the extension pack for Amazon Redshift\. To do so, include the `iam:SimulatePrincipalPolicy` action in your IAM policy\.

AWS SCT uses the IAM Policy Simulator to check the required permissions for installing the Amazon Redshift extension pack\. The IAM Policy Simulator can display an error message even if you have correctly configured your \. This is a known issue of the IAM Policy Simulator\. Also, the IAM Policy Simulator displays an error message when you don't have the `iam:SimulatePrincipalPolicy` action in your IAM policy\. In these cases, you can ignore the error message and apply the extension pack using the extension pack wizard\. For more information, see [Applying the extension pack](#CHAP_ExtensionPack.DW.Installing)\.

## Using the extension pack schema<a name="CHAP_ExtensionPack.Schema"></a>

When you convert your database or data warehouse schema, AWS SCT adds an additional schema to your target database\. This schema implements SQL system functions of the source database that are required when writing your converted schema to your target database\. This additional schema is called the extension pack schema\.

The extension pack schema for OLTP databases is named according to the source database as follows: 
+ Microsoft SQL Server: `AWS_SQLSERVER_EXT`
+ MySQL: `AWS_MYSQL_EXT`
+ Oracle: `AWS_ORACLE_EXT`
+ PostgreSQL: `AWS_POSTGRESQL_EXT`

The extension pack schema for OLAP data warehouse applications is named according to the source data store as follows: 
+ Greenplum: `AWS_GREENPLUM_EXT`
+ Microsoft SQL Server: `AWS_SQLSERVER_EXT`
+ Netezza: `AWS_NETEZZA_EXT`
+ Oracle: `AWS_ORACLE_EXT`
+ Teradata: `AWS_TERADATA_EXT`
+ Vertica: `AWS_VERTICA_EXT`

## Using custom libraries for AWS SCT extension packs<a name="CHAP_ExtensionPack.DW"></a>

In some cases, AWS SCT can't convert source database features to equivalent features in your target database\. The relevant AWS SCT extension pack contains custom libraries that emulate some source database functionality on in your target database\.

If you are converting a transactional database, see [Using the AWS Lambda functions from the AWS SCT extension pack ](#CHAP_ExtensionPack.OLTP)\. 

### Applying the extension pack<a name="CHAP_ExtensionPack.DW.Installing"></a>

You can apply the AWS SCT extension pack using the extension pack wizard or when you apply the converted code to your target database\.

**To apply the extension pack using the extension pack wizard**

1. In the AWS Schema Conversion Tool, in the target database tree, open the context \(right\-click\) menu, choose **Apply extension pack for**, and then choose your source database platform\.  
![\[Apply extension pack context menu\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/extension-pack-context.png)

   The extension pack wizard appears\.

1. Read the **Welcome** page, and then choose **Next**\.

1. On the **AWS profile settings** page, do the following:
   + If you are reinstalling the extension pack schema only, choose **Skip this step for now**, and then choose **Next**\. The **Skip this step for now** option is only available for online transaction processing \(OLTP\) databases\.
   + If you are uploading a new library, then provide the credentials to connect to your AWS account\. Use this step only when you convert OLAP databases or ETL scripts\. You can use your AWS Command Line Interface \(AWS CLI\) credentials if you have the AWS CLI installed\. You can also use credentials that you previously stored in a profile in the global application settings and associated with the project\. If necessary, choose **Navigate to global settings** to configure of associate a different profile with your AWS SCT project\. For more information, see [Storing AWS service profiles in AWS SCT](CHAP_UserInterface.md#CHAP_UserInterface.Profiles)\. 

1. If you are uploading a new library, then choose **I need to upload a library** on the **Library upload** page\. Use this step only when you convert OLAP databases or ETL scripts\. Next, provide the Amazon S3 path, and then choose **Upload library to S3**\.

   If you have already uploaded the library, then choose **I already have libraries uploaded, use my existing S3 bucket** on the **Library upload** page\. Next, provide the Amazon S3 path\.

   When you are done, choose **Next**\.

1. On the **Function emulation** page, choose **Create extension pack**\. Messages appear with the status of the extension pack operations\. 

   When you are done, choose **Finish**\. 

**To apply the extension pack when applying the converted code**

1. Specify the Amazon S3 bucket in your AWS service profile\. Use this step only when you convert OLAP databases or ETL scripts\. For more information, see [Storing AWS service profiles in AWS SCT](CHAP_UserInterface.md#CHAP_UserInterface.Profiles)\.

   Make sure that your Amazon S3 bucket policy includes the following permissions:

   ```
   {
       "Version": "2012-10-17",
       "Statement": [
         {
           "Effect": "Allow",
           "Action": ["s3:ListBucket"],
           "Resource": ["*"]
         },
         {
           "Effect": "Allow",
           "Action": ["s3:PutObject"],
           "Resource": ["*"]
         },
         {
           "Effect": "Allow",
           "Action": ["iam:SimulatePrincipalPolicy"],
           "Resource": ["*"]
         },
         {
           "Effect": "Allow",
           "Action": ["iam:GetUser"],
           "Resource": ["arn:aws:iam::111122223333:user/DataExtractionAgentName"]
         }
       ]
   }
   ```

   In the preceding example, replace *111122223333:user/DataExtractionAgentName* with the name of your IAM user\.

1. Convert your source data warehouse schemas\. For more information, see [Converting data warehouse schemas to Amazon Redshift](CHAP_Converting.DW.md)\.

1. In the right pane, choose the converted schema\.

1. Open the context \(right\-click\) menu for the schema element, and then choose **Apply to database**\.

1. AWS SCT generates extension packs with the required components and adds the `aws_database_engine_name_ext` schema in the target tree\. Next, AWS SCT applies the converted code and the extension pack schema to your target data warehouse\.

   When you use a combination of Amazon Redshift and AWS Glue as your target database platform, AWS SCT adds an additional schema in the extension pack\.

## Using the AWS Lambda functions from the AWS SCT extension pack<a name="CHAP_ExtensionPack.OLTP"></a>

AWS SCT provides an extension pack that contains Lambda functions for email, job scheduling, and other features for databases hosted on Amazon EC2\.

### Using AWS Lambda functions to emulate database functionality<a name="CHAP_ExtensionPack.OLTP.Services"></a>

In some cases, database features can't be converted to equivalent Amazon RDS features\. For example, Oracle sends email calls that use `UTL_SMTP`, and Microsoft SQL Server can use a job scheduler\. If you host and self\-manage a database on Amazon EC2, you can emulate these features by substituting AWS services for them\.

The AWS SCT extension pack wizard helps you install, create, and configure Lambda functions to emulate email, job scheduling, and other features\.

### Applying the extension pack to support Lambda functions<a name="CHAP_ExtensionPack.OLTP.Installing"></a>

You can apply the extension pack to support Lambda functions using the extension pack wizard or when you apply the converted code to your target database\.

**Important**  
The AWS service emulation features are supported only for databases installed and self\-managed on Amazon EC2\. Don't install the service emulation features if your target database is on an Amazon RDS DB instance\. 

**To apply the extension pack using the extension pack wizard**

1. In the AWS Schema Conversion Tool, in the target database tree, open the context \(right\-click\) menu, choose **Apply extension pack for**, and then choose your source database platform\.   
![\[Apply extension pack context menu\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/extension-pack-context.png)

   The extension pack wizard appears\. 

1. Read the **Welcome** page, and then choose **Next**\. 

1. On the **AWS profile settings** page, do the following:
   + If you are reinstalling the extension pack schema only, choose **Skip this step for now**, and then choose **Next**\. 
   + If you are installing AWS services, provide the credentials to connect to your AWS account\. You can use your AWS CLI credentials if you have the AWS CLI installed\. You can also use credentials that you previously stored in a profile in the global application settings and associated with the project\. If necessary, choose **Navigate to Project Settings** to associate a different profile with the project\. If necessary, choose **Global Settings** to create a new profile\. For more information, see [Storing AWS service profiles in AWS SCT](CHAP_UserInterface.md#CHAP_UserInterface.Profiles)\. 

1. On the **Email Sending Service** page, do the following: 
   + If you are reinstalling the extension pack schema only, choose **Skip this step for now**, and then choose **Next**\. 
   + If you are installing AWS services and you have an existing Lambda function, you can provide it\. Otherwise, the wizard creates it for you\. When you are done, choose **Next**\. 

1. On the **Job Emulation Service** page, do the following: 
   + If you are reinstalling the extension pack schema only, choose **Skip this step for now**, and then choose **Next**\. 
   + If you are installing AWS services and you have an existing Lambda function, you can provide it\. Otherwise, the wizard creates it for you\. When you are done, choose **Next**\. 

1. On the **Function emulation** page, choose **Create extension pack**\. Messages appear with the status of the extension pack operations\. 

   When you are done, choose **Finish**\. 

**Note**  
To update an extension pack and overwrite the old extension pack components, make sure that you use the latest version of AWS SCT\. For more information, see [Installing, verifying, and updating AWS SCT](CHAP_Installing.md)\.