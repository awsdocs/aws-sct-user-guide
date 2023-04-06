# Using Apache Oozie as a source for AWS SCT<a name="CHAP_Source.Oozie"></a>

You can use the AWS SCT command line interface \(CLI\) to convert Apache Oozie workflows to AWS Step Functions\. After you migrate your Apache Hadoop workloads to Amazon EMR, you can use a native service in the AWS Cloud to orchestrate your jobs\. For more information, see [Using Apache Hadoop as a source](CHAP_Source.Hadoop.md)\.

AWS SCT converts your Oozie workflows to AWS Step Functions and uses AWS Lambda to emulate features that AWS Step Functions doesn't support\. Also, AWS SCT converts your Oozie job properties to AWS Systems Manager\.

To convert Apache Oozie workflows, make sure that you use AWS SCT version 1\.0\.671 or later\. Also, familiarize yourself with the command line interface of AWS SCT\. For more information, see [AWS SCT CLI Reference](CHAP_Reference.md)\.

## Prerequisites for using Apache Oozie as a source<a name="CHAP_Source.Oozie.Prerequisites"></a>

The following prerequisites are required to connect to Apache Oozie with the AWS SCT CLI\.
+ Create an Amazon S3 bucket to store the definitions of state machines\. You can use these definitions to configure your state machines\. For more information, see [Creating a bucket](https://docs.aws.amazon.com/AmazonS3/latest/userguide/create-bucket-overview.html) in the *Amazon S3 User Guide*\.
+ Create an AWS Identity and Access Management \(IAM\) role with the `AmazonS3FullAccess` policy\. AWS SCT uses this IAM role to access your Amazon S3 bucket\.
+ Take a note of your AWS secret key and AWS secret access key\. For more information about AWS access keys, see [Managing access keys](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html) in the *IAM User Guide*\.
+ Store your AWS credentials and the information about your Amazon S3 bucket in the AWS service profile in the global application settings\. Then, AWS SCT uses this AWS service profile to work with your AWS resources\. For more information, see [Storing AWS service profiles in AWS SCT](CHAP_UserInterface.md#CHAP_UserInterface.Profiles)\.

To work with your source Apache Oozie workflows, AWS SCT requires the specific structure of your source files\. Each of your application folders must include the `job.properties` file\. This file includes key\-value pairs of your job properties\. Also, each of your application folders must include the `workflow.xml` file\. This file describes the action nodes and control flow nodes of your workflow\.

## Connecting to Apache Oozie as a source<a name="CHAP_Source.Oozie.Connecting"></a>

Use the following procedure to connect to your Apache Oozie source files\.

**To connect to Apache Oozie in the AWS SCT CLI**

1. Create a new AWS SCT CLI script or edit an existing scenario template\. For example, you can download and edit the `OozieConversionTemplate.scts` template\. For more information, see [Getting CLI scenarios](CHAP_Reference.md#CHAP_Reference.Scenario)\.

1. Configure the AWS SCT application settings\.

   The following code example saves the application settings and allows to store passwords in your project\. You can use these saved settings in other projects\.

   ```
   SetGlobalSettings
       -save: 'true'
       -settings: '{
           "store_password": "true"
       }'
   /
   ```

1. Create a new AWS SCT project\.

   The following code example creates the `oozie` project in the `c:\sct` folder\.

   ```
   CreateProject
       -name: 'oozie'
       -directory: 'c:\sct'
   /
   ```

1. Add the folder with your source Apache Oozie files to the project using the `AddSource` command\. Make sure that you use the `APACHE_OOZIE` value for the `vendor` parameter\. Also, provide values for the following required parameters: `name` and `mappingsFolder`\.

   The following code example adds Apache Oozie as a source in your AWS SCT project\. This example creates a source object with the name `OOZIE`\. Use this object name to add mapping rules\. After you run this code example, AWS SCT uses the `c:\oozie` folder to load your source files in the project\.

   ```
   AddSource
       -name: 'OOZIE'
       -vendor: 'APACHE_OOZIE'
       -mappingsFolder: 'c:\oozie'
   /
   ```

   You can use this example and the following examples in Windows\.

1. Connect to your source Apache Oozie files using the `ConnectSource` command\. Use the name of your source object that you defined in the previous step\.

   ```
   ConnectSource
       -name: 'OOZIE'
       -mappingsFolder: 'c:\oozie'
   /
   ```

1. Save your CLI script\. Next, add the connection information for your AWS Step Functions service\.

## Permissions for using AWS Lambda functions in the extension pack<a name="CHAP_Source.Oozie.TargetPrerequisites"></a>

For the source functions that AWS Step Functions doesn't support, AWS SCT creates an extension pack\. This extension pack includes AWS Lambda functions, which emulate your source functions\.

To use this extension pack, create an AWS Identity and Access Management \(IAM\) role with the following permissions\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "lambda",
            "Effect": "Allow",
            "Action": [
                "lambda:InvokeFunction"
            ],
            "Resource": [
                "arn:aws:lambda:*:498160209112:function:LoadParameterInitialState:*",
                "arn:aws:lambda:*:498160209112:function:EvaluateJSPELExpressions:*"
            ]
        },
        {
            "Sid": "emr",
            "Effect": "Allow",
            "Action": [
                "elasticmapreduce:DescribeStep",
                "elasticmapreduce:AddJobFlowSteps"
            ],
            "Resource": [
                "arn:aws:elasticmapreduce:*:498160209112:cluster/*"
            ]
        },
        {
            "Sid": "s3",
            "Effect": "Allow",
            "Action": [
                "s3:GetObject"
            ],
            "Resource": [
                "arn:aws:s3:::*/*"
            ]
        }
    ]
}
```

To apply the extension pack, AWS SCT requires an IAM role with the following permissions\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "iam:GetRole",
                "iam:ListRolePolicies",
                "iam:CreateRole",
                "iam:TagRole",
                "iam:PutRolePolicy",
                "iam:DeleteRolePolicy",
                "iam:DeleteRole",
                "iam:PassRole"
            ],
            "Resource": [
                "arn:aws:iam::ACCOUNT_NUMBER:role/sct/*"
            ]
        },
        {
            "Effect": "Allow",
            "Action": [
                "iam:GetRole",
                "iam:ListRolePolicies"
            ],
            "Resource": [
                "arn:aws:iam::ACCOUNT_NUMBER:role/lambda_LoadParameterInitialStateRole",
                "arn:aws:iam::ACCOUNT_NUMBER:role/lambda_EvaluateJSPELExpressionsRole",
                "arn:aws:iam::ACCOUNT_NUMBER:role/stepFunctions_MigratedOozieWorkflowRole"
            ]
        },
        {
            "Effect": "Allow",
            "Action": [
                "lambda:GetFunction",
                "lambda:CreateFunction",
                "lambda:UpdateFunctionCode",
                "lambda:DeleteFunction"
            ],
            "Resource": [
                "arn:aws:lambda:*:ACCOUNT_NUMBER:function:LoadParameterInitialState",
                "arn:aws:lambda:*:ACCOUNT_NUMBER:function:EvaluateJSPELExpressions"
            ]
        }
    ]
}
```

## Connecting to AWS Step Functions as a target<a name="CHAP_Source.Oozie.Target"></a>

Use the following procedure to connect to AWS Step Functions as a target\.

**To connect to AWS Step Functions in the AWS SCT CLI**

1. Open your CLI script which includes the connection information for your Apache Oozie source files\.

1. Add the information about your migration target in the AWS SCT project using the `AddTarget` command\. Make sure that you use the `STEP_FUNCTIONS` value for the `vendor` parameter\. Also, provide values for the following required parameters: `name` and `profile`\.

   The following code example adds AWS Step Functions as a source in your AWS SCT project\. This example creates a target object with the name `AWS_STEP_FUNCTIONS`\. Use this object name when you create mapping rules\. Also, this example uses an AWS SCT service profile that you created in the prerequisites step\. Make sure that you replace *profile\_name* with the name of your profile\.

   ```
   AddTarget
       -name: 'AWS_STEP_FUNCTIONS'
       -vendor: 'STEP_FUNCTIONS'
       -profile: 'profile_name'
   /
   ```

   If you don't use the AWS service profile, make sure that you provide values for the following required parameters: `accessKey`, `secretKey`, `awsRegion`, and `s3Path`\. Use these parameters to specify your AWS secret access key, AWS secret key, AWS Region, and the path to your Amazon S3 bucket\.

1. Connect to AWS Step Functions using the `ConnectTarget` command\. Use the name of your target object that you defined in the previous step\.

   The following code example connects to the `AWS_STEP_FUNCTIONS` target object using your AWS service profile\. Make sure that you replace *profile\_name* with the name of your profile\.

   ```
   ConnectTarget
       -name: 'AWS_STEP_FUNCTIONS'
       -profile: 'profile_name'
   /
   ```

1. Save your CLI script\. Next, add mapping rules and migration commands\. For more information, see [Converting Apache Oozie to AWS Step Functions](big-data-oozie.md)\.