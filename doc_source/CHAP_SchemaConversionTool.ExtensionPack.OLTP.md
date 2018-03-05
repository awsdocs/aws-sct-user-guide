# Using the AWS Lambda Functions from the AWS SCT Extension Pack<a name="CHAP_SchemaConversionTool.ExtensionPack.OLTP"></a>

The AWS Schema Conversion Tool \(AWS SCT\) extension pack contains Lambda functions that provide email, job scheduling, and other features to databases hosted on the Amazon EC2 platform\.

## Using AWS Lambda Functions to Emulate Database Functionality<a name="CHAP_SchemaConversionTool.ExtensionPack.OLTP.Services"></a>

In some cases, database features can't be converted to equivalent Amazon RDS features\. For example, Oracle sends email calls that use `UTL_SMTP`, and Microsoft SQL Server can use a job scheduler\. If you host and self\-manage a database on Amazon EC2, you can emulate these features by substituting AWS services for them\. 

The AWS SCT extension pack wizard helps you install, create, and configure Lambda functions to emulate email, job scheduling, and other features\. 

## Before You Begin<a name="CHAP_SchemaConversionTool.ExtensionPack.OLTP.Before"></a>

Almost all work you do with the AWS SCT starts with the following three steps: 

1. Create an AWS SCT project\.

1. Connect to your source database\.

1. Connect to your target database\.

If you have not created an AWS SCT project yet, see [Getting Started with the AWS Schema Conversion Tool](CHAP_SchemaConversionTool.GettingStarted.md)\. 

Before you install the extension pack, you need to convert your database schema\. For more information, see [Converting Database Schemas Using the AWS Schema Conversion Tool](CHAP_SchemaConversionTool.Converting.md)\. 

## Applying the Extension Pack<a name="CHAP_SchemaConversionTool.ExtensionPack.OLTP.Installing"></a>

Use the following procedure to apply the extension pack\. 

**Important**  
The AWS service emulation features are supported only for databases installed and self\-managed on Amazon EC2\. Don't install the service emulation features if your target database is on an Amazon RDS DB instance\. 

**To apply the extension pack**

1. In the AWS Schema Conversion Tool, in the target database tree, open the context \(right\-click\) menu, and choose **Apply Extension Pack**\.   
![\[Apply Extension Pack context menu\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/extension-pack-context.png)

   The extension pack wizard appears\. 

1. Read the **Welcome** page, and then choose **Next**\. 

1. On the **AWS Services Settings** page, do the following: 

   + If you are reinstalling the extension pack schema only, choose **Skip this step for now**, and then choose **Next**\. 

   + If you are installing AWS services, provide the credentials to connect to your AWS account\. You can use your AWS Command Line Interface \(AWS CLI\) credentials if you have the AWS CLI installed\. You can also use credentials that you previously stored in a profile in the global application settings and associated with the project\. If necessary, choose **Navigate to Project Settings** to associate a different profile with the project\. If necessary, choose **Global Settings** to create a new profile\. For more information, see [Using AWS Service Profiles in the AWS Schema Conversion Tool](CHAP_SchemaConversionTool.UI.md#CHAP_SchemaConversionTool.Profiles)\. 

1. On the **Email Sending Service** page, do the following: 

   + If you are reinstalling the extension pack schema only, choose **Skip this step for now**, and then choose **Next**\. 

   + If you are installing AWS services and you have an existing Lambda function, you can provide it\. Otherwise, the wizard creates it for you\. When you are done, choose **Next**\. 

1. On the **Job Emulation Service** page, do the following: 

   + If you are reinstalling the extension pack schema only, choose **Skip this step for now**, and then choose **Next**\. 

   + If you are installing AWS services and you have an existing Lambda function, you can provide it\. Otherwise, the wizard creates it for you\. When you are done, choose **Next**\. 

1. On the **Functions Emulation** page, choose **Create Extension Pack**\. Messages appear with the status of the extension pack operations\. 

   When you are done, choose **Finish**\. 