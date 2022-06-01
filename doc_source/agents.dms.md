# Migrating data from on\-premises databases using AWS DMS tasks<a name="agents.dms"></a>

You can use an AWS Database Migration Service \(AWS DMS\) task to migrate data from your on\-premises relational database to the AWS Cloud\. You can create, run, and monitor these AWS DMS tasks from AWS SCT\.

## Creating AWS DMS tasks from AWS SCT<a name="agents.dms.Creating"></a>

Use the following procedure to create an AWS DMS task in AWS SCT\.

**To create a data migration task**

1. In AWS SCT, after you have converted your schema, choose one or more tables from the left panel of your project\. 

   For performance reasons, AWS recommends that you create multiple tasks for multiple tables\.

1. Open the context \(right\-click\) menu for your database schema, which includes tables to migrate, and then choose **Create DMS task**\.

   The **Create DMS task** dialog box opens\.

1. For **Task name**, enter a name for the task\. 

1. For **Replication instance**, choose your replication instance from the AWS DMS console\.

   Make sure that you configured the replication instance in the AWS DMS console for the same AWS profile that you use in AWS SCT\. Also, make sure that the major version of the AWS DMS task matches the version of the replication instance\.

1. For **Source endpoint**, choose the source endpoint for data migration\.

1. For **Target endpoint**, choose the target endpoint for data migration\.

1. For **Migration type**, choose one of the following: 
   + **Migrate existing data** – Migrate your data to the target database\. 
   + **Migrate existing data and replicate ongoing changes** – Migrate your data to the target database and set up ongoing replication or change data capture \(CDC\)\. 
   + **Replicate data changes only** – Set up ongoing replication or CDC\. 

1. For **Target table preparation mode**, choose one of the following:
   + **Do nothing** – Leave data in the target database tables\. 
   + **Drop tables on target** – Drop tables in the target database and create new tables before data migration\. 
   + **Truncate** – Remove data from the target database tables before data migration\. 

1. For **Include LOB columns in replication**, choose one of the following:
   + **Don't include LOB columns** – Skip large object \(LOB\) columns during data migration\. 
   + **Full LOB mode** – Migrate LOB columns\. For this option, enter the LOB chunk size in KB\. 
   + **Limited LOB mode** – Migrate LOB columns\. For this option, enter the maximum size of LOB in KB\. 

1. For **Logging**, choose **Enable** to see detailed information about your task\. You can use the task log to debug problems\.

1. Choose **Create** to create the task\.

Or you can create and configure your data migration task in the AWS DMS console\. For more information, see [Creating a task](https://docs.aws.amazon.com/dms/latest/userguide/CHAP_Tasks.Creating.html) in the *AWS Database Migration Service User Guide*\.

## Managing AWS DMS tasks from AWS SCT<a name="agents.dms.Managing"></a>

Use the following procedures to manage AWS DMS tasks in AWS SCT\.

**To manage data migration tasks**

1. On the **View** menu, choose **Data migration view \(standard DMS\)**\.

1. On the **Tasks** tab, review your data migration tasks\. AWS SCT displays the status of your AWS DMS tasks in the top grid, and the status of subtasks in the bottom grid\.

1. Choose a task in the top grid and expand it\.

1. Choose **Start** for a task to start that task\. 