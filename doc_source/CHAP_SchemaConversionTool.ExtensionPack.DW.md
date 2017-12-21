# Using the AWS Schema Conversion Tool Extension Pack Custom Python Library<a name="CHAP_SchemaConversionTool.ExtensionPack.DW"></a>

In some cases, AWS Schema Conversion Tool \(AWS SCT\) can't convert source database features to equivalent Amazon Redshift features\. The AWS SCT Extension Pack contains a custom Python library that emulates some source database functionality on Amazon Redshift\. 

If you are converting a transactional database, instead see [Using the AWS Schema Conversion Tool Extension Pack AWS Lambda Functions](CHAP_SchemaConversionTool.ExtensionPack.OLTP.md)\. 

In two cases, you might want to install the extension pack manually: 

+ You accidentally delete the extension pack database schema from your target database\. 

+ You want to upload custom Python libraries to emulate database functionality\. 

## Using AWS Services to Upload Custom Python Libraries<a name="CHAP_SchemaConversionTool.ExtensionPack.DW.Services"></a>

The AWS SCT extension pack wizard helps you install the custom Python library\. 

## Before You Begin<a name="CHAP_SchemaConversionTool.ExtensionPack.DW.Before"></a>

Almost all work you do with AWS SCT starts with the following three steps: 

1. Create an AWS SCT project\.

1. Connect to your source database\.

1. Connect to your target database\.

If you have not created an AWS SCT project yet, see [Getting Started with the AWS Schema Conversion Tool](CHAP_SchemaConversionTool.GettingStarted.md)\. 

## Applying the Extension Pack<a name="CHAP_SchemaConversionTool.ExtensionPack.DW.Installing"></a>

Use the following procedure to apply the extension pack\. 

**To apply the extension pack**

1. In the AWS Schema Conversion Tool, in the target database tree, open the context \(right\-click\) menu, and choose **Apply Extension Pack**\.   
![\[Apply Extension Pack context menu\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/extension-pack-context.png)

   The extension pack wizard appears\. 

1. Read the **Welcome** page, and then choose **Next**\. 

1. On the **AWS Services Settings** page, do the following: 

   + If you are reinstalling the extension pack database schema only, choose **Skip this step for now**, and then choose **Next**\. 

   + If you are uploading the Python library, provide the credentials to connect to your AWS account\. You can use your AWS Command Line Interface \(AWS CLI\) credentials if you have the AWS CLI installed\. You can also use credentials that you previously stored in a profile in the global application settings and associated with the project\. If necessary, choose **Navigate to Project Settings** to associate a different profile with the project\. If necessary, choose **Global Settings** to create a new profile\. For more information, see [Using AWS Service Profiles in the AWS Schema Conversion Tool](CHAP_SchemaConversionTool.Profiles.md)\. 

1. On the **Python Library Upload** page, do the following: 

   + If you are reinstalling the extension pack database schema only, choose **Skip this step for now**, and then choose **Next**\. 

   + If you are uploading the Python library, provide the Amazon S3 path, and then choose **Upload Library to S3**\. When you are done, choose **Next**\. 

1. On the **Functions Emulation** page, choose **Create Extension Pack**\. Messages appear with the status of the extension pack operations\. When you are done, choose **Finish**\. 