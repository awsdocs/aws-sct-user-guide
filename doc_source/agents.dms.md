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

   If you don't have an existing source endpoint, choose the plus sign \(![\[Image NOT FOUND\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/add-plus.png)\) on the right side of the dialog box\. For **Endpoint name**, enter the name of your endpoint and choose **OK** to create a new source endpoint\.

1. For **Target endpoint**, choose the target endpoint for data migration\.

   If you don't have an existing target endpoint, choose the plus sign \(![\[Image NOT FOUND\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/add-plus.png)\) on the right side of the dialog box\. For **Endpoint name**, enter the name of your endpoint and choose **OK** to create a new target endpoint\.

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

1. On the **Data migration view** tab, review your data migration tasks\. AWS SCT displays the status of your AWS DMS tasks in the top grid, and the status of subtasks in the bottom grid\.

   Keep in mind that your data migration task can include local and remote subtasks\. Local subtasks run on your local PC and extract data from the source endpoint\. Remote subtasks upload data to Amazon S3 and insert data into the target endpoint\. On the **Data migration view** tab, you can manage only remote subtasks\.

1. Choose a task in the top grid to view task details in the bottom grid\.

1. Choose **Start** for a task to start that task\. 

## Data extraction using an AWS Snowball Edge device<a name="agents.dms.Snowball"></a>

The process of using AWS SCT and AWS Snowball Edge has several steps\. The migration involves a local task, where AWS SCT uses a data extraction agent to move the data to the AWS Snowball Edge device, then an intermediate action where AWS copies the data from the AWS Snowball Edge device to your target database in the AWS cloud\.

The sections following this overview provide a step\-by\-step guide to each of these tasks\. The procedure assumes that you have AWS SCT installed and that you have configured and registered a data extraction agent on a dedicated machine\.

Perform the following steps to migrate data from a local data store to an AWS data store using AWS Snowball Edge\.

1. Create an AWS Snowball Edge job using the AWS Snowball console\.

1. Unlock the AWS Snowball Edge device using the local, dedicated Linux machine\.

1. Create a new project in AWS SCT\.

1. Install the database driver for your source database on the dedicated machine where you installed the data extraction agent\.

1. Create and set permissions for the Amazon S3 bucket to use\.

1. Import an AWS Snowball job to your AWS SCT project\.

1. Create a data migration task in AWS SCT\.

1. Run and monitor the data migration task in AWS SCT\.

### Step\-by\-step procedures for migrating data using AWS SCT and AWS Snowball Edge<a name="agents.dms.Snowball.SBS"></a>

The following sections provide detailed information about the migration steps\.

#### Step 1: Create an AWS Snowball Edge job<a name="agents.dms.Snowball.SBS.OrderSnowball"></a>

Create an AWS Snowball job by following the steps outlined in the section [Creating an AWS Snowball Edge Job](https://docs.aws.amazon.com/snowball/latest/developer-guide/create-job-common.html) in the *AWS Snowball Edge Developer Guide*\.

#### Step 2: Unlock the AWS Snowball Edge device<a name="agents.dms.Snowball.SBS.UnlockSnowball"></a>

Run the commands that unlock and provide credentials to the Snowball Edge device from the machine where you installed the AWS DMS agent\. By running these commands, you can be sure that the AWS DMS agent call connects to the AWS Snowball Edge device\. For more information about unlocking the AWS Snowball Edge device, see [Unlocking the Snowball Edge](https://docs.aws.amazon.com/snowball/latest/developer-guide/unlockdevice.html)\.

For example, the following command lists the Amazon S3 bucket used by the device\.

```
aws s3 ls s3://<bucket-name> --profile <Snowball Edge profile> --endpoint http://<Snowball IP>:8080 --recursive 
```

#### Step 3: Create a new AWS SCT project<a name="agents.dms.Snowball.SBS.NewSCTProject"></a>

Next, create a new AWS SCT project\.

**To create a new project in AWS SCT**

1. Start the AWS Schema Conversion Tool\. On the **File** menu, choose **New project**\. The **New project** dialog box appears\. 

1.  Enter a name for your project, which is stored locally on your computer\.

1. Enter the location for your local project file\.

1. Choose **OK** to create your AWS SCT project\.

1. Choose **Add source** to add a new source database to your AWS SCT project\.

1. Choose **Add target** to add a new target database in your AWS SCT project\.

1. Choose the source database schema in the left panel\.

1. In the right panel, specify the target database platform for the selected source schema\.

1. Choose **Create mapping**\. This button becomes active after you choose the source database schema and the target database\.

#### Step 4: Install the source database driver for the AWS DMS agent on the Linux computer<a name="agents.dms.Snowball.SBS.SourceDriver"></a>

For the migration to succeed, the AWS DMS agent must be able to connect to the source database\. To make this possible, you install the database driver for your source database\. The required driver varies by database\.

To restart the AWS DMS agent after database driver installation, change the working directory to `<product_dir>/bin` and use the steps listed following for each source database\.

```
cd <product_dir>/bin
./arep.ctl stop
./arep.ctl start
```

**To install on Oracle**  
Install Oracle Instant Client for Linux \(x86\-64\) version 11\.2\.0\.3\.0 or later\.   
In addition, if one isn't already included in your system, you need to create a symbolic link in the $ORACLE\_HOME\\lib directory\. This link should be called libclntsh\.so, and should point to a specific version of this file\. For example, on an Oracle 12c client, use the following\.  

```
lrwxrwxrwx 1 oracle oracle 63 Oct 2 14:16 libclntsh.so -> /u01/app/oracle/home/lib/libclntsh.so.12.1
```
In addition, the LD\_LIBRARY\_PATH environment variable should be appended with the Oracle lib directory and added to the site\_arep\_login\.sh script under the lib folder of the installation\. Add this script if it doesn't exist\.  

```
vi cat <product dir>/bin/site_arep_login.sh
```

```
export ORACLE_HOME=/usr/lib/oracle/12.2/client64; export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$ORACLE_HOME/lib
```

**To install on Microsoft SQL Server**  
Install the Microsoft ODBC Driver\.  
Update the `site_arep_login.sh` with the following code\.  

```
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/opt/microsoft/msodbcsql/lib64/
```
**Simba ODBC Driver **  
 Install the Microsoft ODBC Driver\.  
 Edit the `simba.sqlserverodbc.ini` file as follows\.  

```
DriverManagerEncoding=UTF-16
ODBCInstLib=libodbcinst.so
```

**To install on SAP ASE**  
Install the SAP ASE ODBC 64\-bit client\.  
If the installation directory is `/opt/sap`, update the `site_arep_login.sh` with the following\.  

```
export SYBASE_HOME=/opt/sap
export                          
LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$SYBASE_HOME/
   DataAccess64/ODBC/lib:$SYBASE_HOME/DataAccess/ODBC/
   lib:$SYBASE_HOME/OCS-16_0/lib:$SYBASE_HOME/OCS-16_0/
   lib3p64:$SYBASE_HOME/OCS-16_0/lib3p
```
Make sure that the `/etc/odbcinst.ini` file includes the following entries\.  

```
[Sybase]
Driver=/opt/sap/DataAccess64/ODBC/lib/libsybdrvodb.so
Description=Sybase ODBC driver
```

**To install on MySQL**  
Install MySQL Connector/ODBC for Linux, version 5\.2\.6 or later\.  
 Make sure that the `/etc/odbcinst.ini` file contains an entry for MySQL, as in the following example\.  

```
[MySQL ODBC 5.2.6 Unicode Driver]
Driver = /usr/lib64/libmyodbc5w.so 
UsageCount = 1
```

**To install on PostgreSQL**  
Install `postgresql94-9.4.4-1PGDG.<OS Version>.x86_64.rpm`\. This package contains the psql executable\.  
For example, the `postgresql94-9.4.4-1PGDG.rhel7.x86_64.rpm` package is required for Red Hat 7\.  
Install the ODBC driver `postgresql94-odbc-09.03.0400-1PGDG.<OS version>.x86_64` or higher for Linux, where `<OS version>` is the OS of the agent machine\.  
For example, the `postgresql94-odbc-09.03.0400-1PGDG.rhel7.x86_64` client is required for Red Hat 7\.  
Make sure that the `/etc/odbcinst.ini` file contains an entry for PostgreSQL, as in the following example\.  

```
[PostgreSQL]
Description = PostgreSQL ODBC driver
Driver = /usr/pgsql-9.4/lib/psqlodbc.so
Setup = /usr/pgsql-9.4/lib/psqlodbcw.so
Debug = 0
CommLog = 1
UsageCount = 2
```

#### Step 5: Configure AWS SCT to access the Amazon S3 bucket<a name="agents.dms.Snowball.SBS.ConfigureS3"></a>

For information on configuring an Amazon S3 bucket, see [Buckets overview](https://docs.aws.amazon.com/AmazonS3/latest/user-guide/UsingBucket.html) in the *Amazon Simple Storage Service User Guide*\.

#### Step 6: Import an AWS Snowball job to your AWS SCT project<a name="agents.dms.Snowball.SBS.Import"></a>

To connect your AWS SCT project with your AWS Snowball Edge device, import your AWS Snowball job\.

**To import your AWS Snowball job**

1. Open the **Settings** menu, and then choose **Global settings**\. The **Global settings** dialog box appears\.

1. Choose **AWS service profiles**, and then choose **Import job**\.

1. Choose your AWS Snowball job\.

1. Enter your **AWS Snowball IP**\. For more information, see [Changing Your IP Address](https://docs.aws.amazon.com/snowball/latest/ug/using-device.html#snowballnetwork) in the *AWS Snowball User Guide*\.

1. Enter your AWS Snowball **Port**\. For more information, see [Ports Required to Use AWS Services on an AWS Snowball Edge Device](https://docs.aws.amazon.com/snowball/latest/developer-guide/port-requirements.html) in the *AWS Snowball Edge Developer Guide*\.

1. Enter your **AWS Snowball access key** and **AWS Snowball secret key**\. For more information, see [Authorization and Access Control in AWS Snowball](https://docs.aws.amazon.com/snowball/latest/ug/auth-access-control.html) in the *AWS Snowball User Guide*\.

1. Choose **Apply**, and then choose **OK**\.

#### Step 7: Creating a Local & AWS DMS task<a name="agents.dms.Snowball.SBS.CreateLocalRemoteTask"></a>

Next, you create the end\-to\-end migration task\. The task includes two subtasks\. One subtask migrates data from the source database to the AWS Snowball Edge appliance\. The other subtask takes the data that the appliance loads into an Amazon S3 bucket and migrates it to the target database\.

**To create the end\-to\-end migration task**

1. Start AWS SCT, choose **View**, and then choose **Database Migration View \(Local & DMS\)**\.

1. On the **View** menu, choose **Data Migration view \(other\)**\. The **Agents** tab appears\. If you have previously registered agents, AWS SCT displays them in a grid at the top of the tab\.

1. Choose **Register**\.

   After you register an agent with an AWS SCT project, you can't register the same agent with a different project\. If you're no longer using an agent in an AWS SCT project, you can unregister it\. You can then register it with a different project\.

1. Choose **DMS data agent**, and then choose **OK**\.

1. Enter your information on the **Connection** tab of the dialog box:

   1. For **Description**, enter a description of the agent\. 

   1. For **Host Name**, enter the host name or IP address of the computer of the agent\.

   1. For **Port**, enter the port number that the agent is listening on\.

   1. For **Password**, enter the password for your agent\.

   1. Choose **Register** to register the DMS agent with your AWS SCT project\.

1. On the **View** menu, choose **Main view**\. 

1. In the left panel that displays the schema from your source database, select database objects to migrate\. Open the context \(right\-click\) menu for the schema, and then choose **Create Local & DMS task**\.

1. Add your task information\.    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/agents.dms.html)

1. Choose **Create** to create the task\.

#### Step 8: Running and monitoring the AWS SCT task<a name="agents.dms.Snowball.SBS.RunMonitorLocalTask"></a>

You can start the Local & DMS Task when all connections to endpoints are successful\. Make sure that your AWS DMS agent can connect to the source database, the staging Amazon S3 bucket, and the AWS Snowball device\.

You can monitor the AWS DMS agent logs by choosing **Show log**\. The log details include agent server \(**Agent log**\) and local running task \(**Task log**\) logs\. Because the endpoint connectivity is done by the server \(since the local task is not running and there are no task logs\), connection issues are listed under the **Agent log** tab\.

## Permissions for running AWS DMS tasks<a name="agents.dms.Permissions"></a>

To create, run, and manage AWS DMS tasks in AWS SCT, make sure that you grant the following required permissions to your user:
+ `dms:CreateEndpoint` – to create an endpoint using the provided settings\.
+ `dms:CreateReplicationTask` – to create a replication task using the specified parameters\.
+ `dms:DeleteReplicationTask` – to delete the specified replication task\.
+ `dms:DescribeConnections` – to see the the status of the connections that have been made between the replication instance and an endpoint\.
+ `dms:DescribeReplicationInstances` – to see the information about replication instances for your account in the current region\.
+ `dms:DescribeReplicationTasks` – to see the information about replication tasks for your account in the current region\.
+ `dms:DescribeEndpointTypes` – to see the information about the type of available endpoints\.
+ `dms:DescribeEndpoints` – to see the information about the endpoints for your account in the current region\.
+ `dms:DescribeTableStatistics` – to see the table statistics on the database migration task, including table name, rows inserted, rows updated, and rows deleted\.
+ `dms:StartReplicationTask` – to start the replication task\.
+ `dms:StopReplicationTask` – to stop the replication task\.
+ `dms:TestConnection` – to test the connection between the replication instance and the endpoint\.
+ `logs:DescribeLogGroups` – to see the list of the the specified log groups\.
+ `logs:DescribeLogStreams` – to see the list of the log streams for the specified log group\.
+ `logs:FilterLogEvents` – to filter the log events from the specified log group\.
+ `logs:GetLogEvents` – to see the log events from the specified log group\.

The following code example shows you how to grant these permissions to your user\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "dms:CreateEndpoint",
                "dms:CreateReplicationTask",
                "dms:DeleteReplicationTask",
                "dms:DescribeConnections",
                "dms:DescribeReplicationInstances",
                "dms:DescribeReplicationTasks",
                "dms:DescribeEndpointTypes",
                "dms:DescribeEndpoints",
                "dms:DescribeTableStatistics",
                "dms:StartReplicationTask",
                "dms:StopReplicationTask",
                "dms:TestConnection",
                "logs:DescribeLogGroups",
                "logs:DescribeLogStreams",
                "logs:FilterLogEvents",
                "logs:GetLogEvents"
            ],
            "Resource": [
                "*"
            ]
        }
    ]
}
```