# Using AWS Service Profiles in the AWS Schema Conversion Tool<a name="CHAP_SchemaConversionTool.Profiles"></a>

You can store your AWS credentials in the AWS Schema Conversion Tool \(AWS SCT\)\. AWS SCT uses your credentials when you use features that integrate with AWS services\. For example, AWS SCT integrates with Amazon S3, AWS Lambda, Amazon Relational Database Service, and AWS Database Migration Service\. 

AWS SCT asks you for your AWS credentials when you access a feature that requires them\. You can store your credentials in the global application settings\. When AWS SCT asks for your credentials, you can select the stored credentials\. 

You can store different sets of AWS credentials in the global application settings\. For example, you can store one set of credentials that you use in test scenarios, and a different set of credentials that you use in production scenarios\. You can also store different credentials for different AWS Regions\. 

## Storing AWS Credentials<a name="CHAP_SchemaConversionTool.Profiles.Storing"></a>

Use the following procedure to store AWS credentials globally\. 

**To store AWS credentials**

1. Start the AWS Schema Conversion Tool\.

1. Open the **Settings Menu**, and then choose **Global Settings**\. The **Global Settings** dialog box appears\. 

   Choose **AWS Service Profiles**, as shown following\.   
![\[The Global Settings dialog box with the AWS Service Profiles tab selected\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/AWSServiceProfileSettings.png)

1. Choose **Add new AWS Service Profile**\. 

1. Enter your AWS information as follows\.     
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/CHAP_SchemaConversionTool.Profiles.html)

   1. For **Profile name**, type a name for your profile\. 

   1. For **AWS Access Key**, type your AWS access key\. 

   1. For **AWS Secret Key**, type your AWS secret key\. 

   1. For **Region**, choose the region for your profile\. 

   1. For **S3 Bucket**, choose the S3 bucket for your profile\. You only need to specify a bucket if you are using a feature that connects to S3\. 

   1. Select **Use FIPS endpoint for S3** if you need to comply with the Federal Information Processing Standard security requirements\. FIPS endpoints are available in the following AWS Regions: 

      + US East \(N\. Virginia\) Region

      + US East \(Ohio\) Region

      + US West \(N\. California\) Region

      + US West \(Oregon\) Region

1. Choose **Test Connection** to verify that your credentials are correct and active\. 

   The **Test Connection** dialog box appears\. You can see the status for each of the services connected to your profile\. **Pass** indicates that the profile can successfully access the service\.   
![\[The Global Settings dialog box with the AWS Service Profiles tab selected\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/AWSServiceProfileSettings-Test.png)

1. After you have configured your profile, choose **Save** to save your profile\. You can also choose **Cancel** to cancel your changes\. 

1. Choose **OK** to close the **Global Settings** dialog box\. 

## Setting the Default Profile for a Project<a name="CHAP_SchemaConversionTool.Profiles.Project"></a>

You can set the default profile for an AWS SCT project\. Doing this associates the AWS credentials stored in the profile with the project\. With your project open, use the following procedure to set the default profile\. 

**To set the default profile for a project**

1. Start the AWS Schema Conversion Tool\.

1. Open the **Settings Menu**, and then choose **Project Settings**\. The **Current project settings** dialog box appears\. 

1. Choose the **Project Environment** tab\. 

1. For **AWS Service Profile**, choose the profile that you want to associate with the project\. 

1. Choose **OK** to close the **Current project settings** dialog box\. You can also choose **Cancel** to cancel your changes\. 