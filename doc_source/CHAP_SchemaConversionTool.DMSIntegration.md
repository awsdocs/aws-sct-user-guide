# Working with the AWS Database Migration Service Using the AWS Schema Conversion Tool<a name="CHAP_SchemaConversionTool.DMSIntegration"></a>

AWS Database Migration Service \(AWS DMS\) is a web service that you can use to migrate data to and from most widely used commercial and open\-source databases\. You can use the AWS Schema Conversion Tool \(AWS SCT\) to create AWS DMS endpoints and tasks\. You can run and monitor the tasks from AWS SCT\. For more information about AWS DMS, see [What Is AWS Database Migration Service?](http://docs.aws.amazon.com/dms/latest/userguide/Welcome.html) in the *AWS DMS User Guide\.*\. 

## Before You Begin<a name="CHAP_SchemaConversionTool.DMSIntegration.Before"></a>

Almost all work you do with AWS SCT starts with the following three steps: 

1. Create an AWS SCT project\.

1. Connect to your source database\.

1. Connect to your target database\.

If you have not created an AWS SCT project yet, see [Getting Started with the AWS Schema Conversion Tool](CHAP_SchemaConversionTool.GettingStarted.md)\. 

Because AWS DMS interacts with the target schema, you need to convert your database schema before you can integrate with AWS DMS\. To convert your database schema, see [Converting Database Schema to Amazon RDS by Using the AWS Schema Conversion Tool](CHAP_SchemaConversionTool.Converting.md)\. 

## Credentials for Working with AWS DMS<a name="CHAP_SchemaConversionTool.DMSIntegration.Credentials"></a>

To create AWS DMS tasks, AWS SCT must connect to AWS DMS with your credentials\. You can use credentials that you previously stored in a profile in the global application settings and associated with the project\. For more information, see [Using AWS Service Profiles in the AWS Schema Conversion Tool](CHAP_SchemaConversionTool.Profiles.md)\. 

## Creating an AWS DMS Task<a name="CHAP_SchemaConversionTool.DMSIntegration.Create"></a>

After you use AWS SCT to convert your database schema, you can create AWS DMS tasks\. Use the following procedure to create an AWS DMS task\. 

**To create an AWS DMS task**

1. In the AWS Schema Conversion Tool, choose a database or a schema object from the left panel of your project\. Open the context \(right\-click\) menu for the object, and then choose **Create DMS Task**\. 

    The **Create DMS task** dialog box appears\. 

1. For **Task name**, type a name for your task\. 

1. For **Replication instance**, choose the replication instance that you want to use\. For more information, see [Replication Instances for AWS Database Migration Service](http://docs.aws.amazon.com/dms/latest/userguide/CHAP_Introduction.ReplicationInstance.html)\. 

1. For **Source endpoint**, choose an existing endpoint\. You can also choose **Create new** to create a new endpoint\. When you choose **Create new**, a new endpoint is created for you by using the current connection information\. You can verify the connection information and give the endpoint a name before it is created\. 

1. For **Target endpoint**, choose an existing endpoint\. You can also choose **Create new** to create a new endpoint\. When you choose **Create new**, a new endpoint is created for you by using the current connection information\. You can verify the connection information and give the endpoint a name before it is created\. 

1. For **Include LOB columns in replication**, choose **Don’t include LOB columns**, **Full LOB mode**, or **Limited LOB mode**\. For more information, see [LOB Support for Source Databases](http://docs.aws.amazon.com/dms/latest/userguide/CHAP_Introduction.LOBSupport.html)\. 

1. For **LOB chunk size \(kb\)**, type the LOB chunk size in kilobytes\. 

1. Select **Enable logging** to turn on logging for the task\. 

1. Choose **Preview JSON** to see the JSON that is created for the task\. 

1. Choose **Save JSON** to save a copy of the JSON that is created for the task\. 

1. After you have configured your task, choose **Create** to save your task\. You can also choose **Close** to cancel your changes\. 

## Running and Monitoring an AWS DMS Task<a name="CHAP_SchemaConversionTool.DMSIntegration.Run"></a>

After you create AWS DMS tasks, you can run and monitor them in the data migration view\. Use the following procedure to run and monitor your AWS DMS tasks\. 

**To run and monitor your AWS DMS tasks**

1. Open the **View** menu, and then choose **Data Migration View**\. 

1. In the list of tasks, choose the task you want to run\. Choose **Start** to run the task\. The **Status** column shows the status of the task\. 

1. When you have a running task, you can choose the following actions: 

   + Choose **Stop** to stop a task\. 

   + Choose **Resume** to resume a task\. 

1. Choose **Delete** to delete a task\. 

1. Choose **Refresh** to refresh the task list\. The **Status** column shows the current status of all tasks\. 

1. Choose **Show Log** to see the task log\. If you selected **Enable logging** when you created the task, the task log shows log information\. 

## Related Topics<a name="CHAP_SchemaConversionTool.DMSIntegration.Related"></a>

+ [What Is the AWS Schema Conversion Tool?](Welcome.md)

+ [Working with AWS Database Migration Service Replication Tasks](http://docs.aws.amazon.com/dms/latest/userguide/CHAP_Tasks.html)

+ [Monitoring AWS Database Migration Service Tasks](http://docs.aws.amazon.com/dms/latest/userguide/CHAP_Monitoring.html)