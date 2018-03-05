# Using Data Extraction Agents<a name="Agents.DW"></a>

You can use data extraction agents to extract data from your on\-premises data warehouse and migrate it to Amazon Redshift\. To manage the data extraction agents, you can use AWS SCT\. Data extraction agents can work in the background while AWS SCT is closed\. After your agents extract your data, they upload the data to Amazon S3 and then copy the data into Amazon Redshift\. 

The following diagram shows the supported scenario\. 

![\[Extraction agent architecture\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/extraction-agents-art.png)

Data extraction agents are currently supported for the following source data warehouses: 

+ Greenplum Database \(version 4\.3 and later\)

+ Microsoft SQL Server \(version 2008 and later\)

+ Netezza \(version 7\.0\.3 and later\)

+ Oracle \(version 10 and later\)

+ Teradata \(version 13 and later\)

+ Vertica \(version 7\.2\.2 and later\)

You can connect to FIPS endpoints for Amazon Redshift if you need to comply with the Federal Information Processing Standard security requirements\. FIPS endpoints are available in the following AWS Regions: 

+ US East \(N\. Virginia\) Region \(redshift\-fips\.us\-east\-1\.amazonaws\.com\)

+ US East \(Ohio\) Region \(redshift\-fips\.us\-east\-2\.amazonaws\.com\)

+ US West \(N\. California\) Region \(redshift\-fips\.us\-west\-1\.amazonaws\.com\)

+ US West \(Oregon\) Region \(redshift\-fips\.us\-west\-2\.amazonaws\.com\)

Use the information in the following topics to learn how to work with data extraction agents\. 


+ [Prerequisite Settings for Amazon S3 and Security for Data Extraction Agents](#Agents.DW.PreReqSettings)
+ [Installing Extraction Agents](#Agents.DW.Installing)
+ [Registering Extraction Agents with the AWS Schema Conversion Tool](#Agents.DW.Using)
+ [Hiding and Recovering Information for an AWS SCT Agent](#Agents.DW.Recovering)
+ [Creating Data Extraction Filters in the AWS Schema Conversion Tool](#Agents.DW.Filtering)
+ [Sorting Data Before Migrating Using AWS SCT](#Agents.DW.Sorting)
+ [Creating, Running, and Monitoring an AWS SCT Data Extraction Task](#Agents.DW.Tasks)
+ [Data Extraction Task Output](#Agents.DW.MovingData)
+ [Using Virtual Partitioning with AWS Schema Conversion Tool](#Agents.DW.VirtualPartitioning)
+ [Migrating LOBs to Amazon Redshift](#Agents.DW.LOBs)
+ [Best Practices and Troubleshooting for Data Extraction Agents](#Agents.DW.BestPractices)

## Prerequisite Settings for Amazon S3 and Security for Data Extraction Agents<a name="Agents.DW.PreReqSettings"></a>

Before you work with data extraction agents, store your Amazon S3 bucket information and set up your Secure Sockets Layer \(SSL\) trust and key store\. 

### Amazon S3 Settings<a name="Agents.DW.S3Credentials"></a>

After your agents extract your data, they upload it to your Amazon S3 bucket\. Before you continue, you must provide the credentials to connect to your AWS account and your Amazon S3 bucket\. You store your credentials and bucket information in a profile in the global application settings, and then associate the profile with your AWS SCT project\. If necessary, choose **Global Settings** to create a new profile\. For more information, see [Using AWS Service Profiles in the AWS Schema Conversion Tool](CHAP_SchemaConversionTool.UI.md#CHAP_SchemaConversionTool.Profiles)\. 

### Security Settings<a name="Agents.DW.Installing.Security"></a>

The AWS Schema Conversion Tool and the extraction agents can communicate through Secure Sockets Layer \(SSL\)\. To enable SSL, set up a trust store and key store\. 

**To set up secure communication with your extraction agent**

1. Start the AWS Schema Conversion Tool\.

1. Open the **Settings** menu, and then choose **Global Settings**\. The **Global settings** dialog box appears\. 

   Choose the **Security** tab as shown following\.   
![\[The Security tab on the Global Settings dialog box\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/SecuritySettings.png)

1. Choose **Generate Trust and Key Store**, or choose **Select existing Trust and Key Store**\. 

   If you choose **Generate Trust and Key Store**, you then specify the name and password for the trust and key stores, and the path to the location for the generated files\. You use these files in later steps\. 

   If you choose **Select existing Trust and Key Store**, you then specify the password and file name for the trust and key stores\. You use these files in later steps\. 

1. After you have specified the trust store and key store, choose **OK** to close the **Global Settings** dialog box\. 

## Installing Extraction Agents<a name="Agents.DW.Installing"></a>

We recommend that you install multiple extraction agents on individual computers, separate from the computer that is running the AWS Schema Conversion Tool\. 

Extraction agents are currently supported on the following operating systems: 

+ macOS

+ Microsoft Windows

+ Red Hat Enterprise Linux \(RHEL\) 6\.0

+ Ubuntu Linux \(version 14\.04 and later\)

Use the following procedure to install extraction agents\. Repeat this procedure for each computer that you want to install an extraction agent on\. 

**To install an extraction agent**

1. If you have not already downloaded the AWS SCT installer file, follow the instructions at [Installing, Verifying, and Updating the AWS Schema Conversion Tool](CHAP_SchemaConversionTool.Installing.md) to download it\. The \.zip file that contains the AWS SCT installer file also contains the extraction agent installer file\. 

1. Locate the installer file for your extraction agent in a subfolder named agents\. For each computer operating system, the correct file to install the extraction agent is shown following\.   
****    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/Agents.DW.html)

1. To install the extraction agent on a separate computer, copy the installer file to the new computer\. 

1. Run the installer file\. Use the instructions for your operating system, shown following\.   
****    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/Agents.DW.html)

1. Install the Java Database Connectivity \(JDBC\) drivers for your source database engine\. For instructions and download links, see [Installing the Required Database Drivers](CHAP_SchemaConversionTool.Installing.md#CHAP_SchemaConversionTool.Installing.JDBCDrivers)\. Follow the instructions for your source database engine only, not your target database engine\. 

1. Copy the SSL trust and key stores \(\.zip or individual files\) that you generated in an earlier procedure\. If you copy the \.zip file to a new computer, extract the individual files from the \.zip file on the new computer\. 

   You can put the files anywhere you want\. However, note the locations because in a later procedure you tell the agent where to find the files\. 

Continue installing your extraction agent by completing the procedure in the following section\. 

### Configuring Extraction Agents<a name="Agents.DW.Installing.AgentSettings"></a>

Use the following procedure to configure extraction agents\. Repeat this procedure on each computer that has an extraction agent installed\. 

**To configure your extraction agent**

+ From the location where you installed the agent, run the setup program\. For RHEL and Ubuntu, the file is named `sct-extractor-setup.sh`\. For macOS and Microsoft Windows, the file is named `AWS SCT Data Extractor Agent`, and you can double\-click the file to run it\. 

  The setup program prompts you for information\. For each prompt, a default value appears\. You can accept the default value, or type a new value\. You specify the following information: 

  + The data warehouse engine\.

  + The port number the agent listens on\.

  + The location where you installed the JDBC drivers\.

  + The working folder\. Your extracted data goes into a subfolder of this location\. The working folder can be on a different computer from the agent, and a single working folder can be shared by multiple agents on different computers\. 

  + The location of the key store file\.

  + The password for the key store\.

  + The location of the trust store file\.

  + The password for the trust store\.

The setup program updates the settings file for the extraction agent\. The settings file is named `Settings.properties`, and is located where you installed the extraction agent\. The following is a sample settings file\. 

```
 1. port=8888
 2. vendor=ORACLE
 3. driver.jars=<driver path>/Install/Drivers/ojdbc7.jar
 4. location=<output path>/dmt/8888/out
 5. extractor.log.folder=<log path>/dmt/8888/log
 6. extractor.storage.folder=<storage path>/dmt/8888/storage
 7. extractor.start.fetch.size=20000
 8. extractor.out.file.size=10485760
 9. ssl.option=OFF
10. #ssl.option=ON
11. #ssl.keystore.path=<key store path>/dmt/8888/vault/keystore
12. #ssl.truststore.path=<trust store path>/dmt/8888/vault/truststore
```

### Starting Extraction Agents<a name="Agents.DW.Installing.AgentStart"></a>

Use the following procedure to start extraction agents\. Repeat this procedure on each computer that has an extraction agent installed\. 

Extraction agents act as listeners\. When you start an agent with this procedure, the agent starts listening for instructions\. You send the agents instructions to extract data from your data warehouse in a later section\. 

**To start your extraction agent**

+ On the computer that has the extraction agent installed, run the command listed following for your operating system\.   
****    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/Agents.DW.html)

To check the status of the agent, run the same command but replace `start` with `status`\. 

To stop an agent, run the same command but replace `start` with `stop`\. 

## Registering Extraction Agents with the AWS Schema Conversion Tool<a name="Agents.DW.Using"></a>

You manage your extraction agents by using AWS SCT\. The extraction agents act as listeners\. When they receive instructions from AWS SCT, they extract data from your data warehouse\. 

Use the following procedure to register extraction agents with your AWS SCT project\. 

**To register an extraction agent**

1. Start the AWS Schema Conversion Tool, and open a project\. 

   1. Open an existing or create a new project\. For more information, see [ Creating an AWS Schema Conversion Tool Project](CHAP_SchemaConversionTool.GettingStarted.md#CHAP_SchemaConversionTool.GettingStarted.Project)\. 

   1. Connect to your source database\. For more information, see [ Connecting to Your Source Database](CHAP_SchemaConversionTool.GettingStarted.md#CHAP_SchemaConversionTool.Converting.CreateProject)\. 

   1. Connect to your target database\. For more information, see [ Connecting to Your Target Database](CHAP_SchemaConversionTool.GettingStarted.md#CHAP_SchemaConversionTool.GettingStarted.Target)\. 

   1. Convert your schema\. For more information, see [ Converting Data Warehouse Schemas to Amazon Redshift by Using the AWS Schema Conversion Tool](CHAP_SchemaConversionTool.Converting.DW.md)\. 

   1. Apply your schema\. For more information, see [ Saving and Applying Your Converted Schema in the AWS Schema Conversion Tool](CHAP_SchemaConversionTool.DW.SaveAndApply.md)\. 

1. Open the **View** menu, and then choose **Data Migration View**\. The **Agents** tab appears\. If you have previously registered agents, they appear in a grid at the top of the tab as shown following\.   
![\[Agents grid\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/AgentsGrid.png)

1. Choose **Register**\. The **New Agent Registration** dialog box appears\. 
**Note**  
After you register an agent with an AWS SCT project, you can't register the same agent with a different project\. If you're no longer using an agent in an AWS SCT project, you can unregister it\. You can then register it with a different project\. 

1. Enter your information in the **New Agent Registration** dialog box: 

   1. For **Description**, type a description of the agent\. 

   1. For **Host Name**, type the host name or IP address of the computer of the agent\. 

   1. For **Port**, type the port number that the agent is listening on\. 

   1. Choose **Register** to register the agent with your AWS SCT project\. 

1. Repeat the previous steps to register multiple agents with your AWS SCT project\. 

## Hiding and Recovering Information for an AWS SCT Agent<a name="Agents.DW.Recovering"></a>

An AWS SCT agent encrypts a significant amount of information, for example passwords to user key\-trust stores, database accounts, AWS account information, and similar items\. It does so using a special file called `seed.dat`\. By default, the agent creates this file in the working folder of the user who first configures the agent\.

Because different users can configure and run the agent, the path to `seed.dat` is stored in the `{extractor.private.folder}` parameter of the `settings.properties` file\. When the agent starts, it can use this path to find the `seed.dat` file to access the key\-trust store information for the database it acts on\.

You might need to recover passwords that an agent has stored in these cases:

+ If the user loses the `seed.dat` file and the AWS SCT agent's location and port didn't change\.

+ If the user loses the `seed.dat` file and the AWS SCT agent's location and port has changed\. In this case, the change usually occurs because the agent was migrated to another host or port and the information in the `seed.dat` file is no longer valid\.

In these cases, if an agent is started without SSL, it starts and then accesses the previously created agent storage\. It then goes to the **Waiting for recovery** state\. 

However, in these cases, if an agent is started with SSL you can't restart it\. This is because the agent can't decrypt the passwords to certificates stored in the `settings.properties` file\. In this type of startup, the agent fails to start\. An error similar to the following is written in the log: "The agent could not start with SSL mode enabled\. Please reconfigure the agent\. Reason: The password for keystore is incorrect\." 

To fix this, create a new agent and configure the agent to use the existing passwords for accessing the SSL certificates\. To do so, use the following procedure\. 

After you perform this procedure, the agent should run and go to the **Waiting for recovery** state\. AWS SCT automatically sends the needed passwords to an agent in the **Waiting for recovery** state\. When the agent has the passwords, it restarts any tasks\. No further user action is required on the SCT side\.

**To reconfigure the agent and restore passwords for accessing SSL certificates**

1. Install a new AWS SCT agent and run configuration\. 

1. Change the `agent.name` property in the `instance.properties` file to the name of the agent the storage was created for, to have the new agent work with existing agent storage\. 

   The `instance.properties` file is stored in the agent's private folder, which is named using the following convention: `{output.folder}\dmt\{hostName}_{portNumber}\`\. 

1. Change the name of `{output.folder}` to that of the previous agent's output folder\.

   At this point, AWS SCT is still trying to access the old extractor at the old host and port\. As a result, the inaccessible extractor gets the status FAILED\. You can then change the host and port\.

1. Modify the host, port, or both for the old agent by using the Modify command to redirect the request flow to the new agent\. 

When AWS SCT can ping the new agent, AWS SCT receives the status **Waiting for recovery** from the agent\. AWS SCT then automatically recovers the passwords for the agent\.

Each agent that works with the agent storage updates a special file called `storage.lck` located at `{output.folder}\{agentName}\storage\`\. This file contains the agent's network ID and the time until which the storage is locked\. When the agent works with the agent storage, it updates the `storage.lck` file and extends the lease of the storage by 10 minutes every 5 minutes\. No other instance can work with this agent storage before the lease expires\.

## Creating Data Extraction Filters in the AWS Schema Conversion Tool<a name="Agents.DW.Filtering"></a>

Before you extract your data with the AWS Schema Conversion Tool \(AWS SCT\), you can set up filters that reduce the amount of data that you extract\. You can create data extraction filters by using `WHERE` clauses to reduce the data that you extract\. For example, you can write a `WHERE` clause that selects data from a single table\. 

You can create data extraction filters and save the filters as part of your project\. With your project open, use the following procedure to create data extraction filters\. 

**To create data extraction filters**

1. On the **Settings** menu, choose **Mapping Rules**\. The **Mapping Rules** dialog box appears\. The top pane contains transformation rules, and the bottom pane contains filtering rules\. 

1. In the **Filtering Rules** pane, choose **Add new rule**\. 

1. Configure your filter: 

   1. For **Name**, type a name for your filter\. 

   1. For **Where schema name like**, type a filter to apply to schemas\. In this filter, a `WHERE` clause is evaluated by using a `LIKE` clause\. You can enter an exact name to choose one schema, or you can enter a pattern to choose multiple schemas\. 

   1. For **table name like**, type a filter to apply to tables\. In this filter, a `WHERE` clause is evaluated by using a `LIKE` clause\. You can enter an exact name to choose one table, or you can enter a pattern to choose multiple tables\. 

   1. For **Where clause**, type a `WHERE` clause to filter data\. 

1. After you have configured your filter, choose **Save** to save your filter, or **Cancel** to cancel your changes\. 

1. After you are done adding, editing, and deleting filters, choose **Save All** to save all your changes, and then choose **Close**\. 

To turn off a filter without deleting it, use the toggle icon\. To duplicate an existing filter, use the copy icon\. To delete an existing filter, use the delete icon\. To save any changes you make to your filters, choose **Save All**\. 

## Sorting Data Before Migrating Using AWS SCT<a name="Agents.DW.Sorting"></a>

Sorting your data before migration with AWS SCT provides some benefits\. If you sort data first, AWS SCT can restart the extraction agent at the last saved point after a failure\. Also, if you are migrating data to Amazon Redshift and you sort data first, AWS SCT can insert data into to Amazon Redshift faster\. 

These benefits have to do with how AWS SCT creates data extraction queries\. In some cases, AWS SCT uses the DENSE\_RANK analytic function in these queries\. However, DENSE\_RANK can use lots of time and server resources to sort the dataset that results from extraction, so if AWS SCT can work without it, it does\.

**To sort data before migrating using AWS SCT**

1. Open an AWS SCT project\.

1. Open the context \(right\-click\) menu for the object, and then choose **Create Local Task**\.

1. Choose the **Advanced** tab, and for **Sorting Strategy**, choose an option:

   + **Never use sorting** – The extraction agent doesn't use the DENSE\_RANK analytic function and restarts from the beginning if a failure occurs\.

   + **Use sorting if possible** – The extraction agent uses DENSE\_RANK if the table has a primary key or a unique constraint\.

   + **Use sorting after first fail \(recommended\)** – The extraction agent first tries to get the data without using DENSE\_RANK\. If the first attempt fails, the extraction agent rebuilds the query using DENSE\_RANK and preserves its location in case of failure\.  
![\[The Security tab on the Global Settings dialog box\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/local-task-sorting.png)

1.  Set additional parameters as described following, and then choose **Create **to create your data extraction task\. 

## Creating, Running, and Monitoring an AWS SCT Data Extraction Task<a name="Agents.DW.Tasks"></a>

Use the following procedures to create, run, and monitor data extraction tasks\. 

**To assign tasks to agents and migrate data**

1. In the AWS Schema Conversion Tool, after you have converted your schema, choose one or more tables from the left panel of your project\. 

   You can choose all tables, but we recommend against that for performance reasons\. We recommend that you create multiple tasks for multiple tables based on the size of the tables in your data warehouse\. 

1. Open the context \(right\-click\) menu for each table, and then choose **Create Task**\. The **Create Local Task** dialog box opens, as shown following\.   
![\[Task dialog box\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/TaskDialog.png)

1. For **Task Name**, type a name for the task\. 

1. For **Migration Mode**, choose one of the following: 

   + **Extract Only** – Extract your data, and save the data to your local working folders\. 

   + **Extract and Upload** – Extract your data, and upload your data to Amazon S3\. 

   + **Extract, Upload and Copy** – Extract your data, upload your data to Amazon S3, and copy it into your Amazon Redshift data warehouse\. 

1. Choose **Extract LOBs** to extract large objects\. If you don't need to extract large objects, you can clear the check box\. Doing this reduces the amount of data that you extract\. 

1. If you want to see detailed information about a task, choose **Enable Task Logging**\. You can use the task log to debug problems\. 

   If you enable task logging, choose the level of detail that you want to see\. The levels are the following, with each level including all messages from the previous level: 

   + `ERROR` – The smallest amount of detail\.

   + `WARNING`

   + `INFO`

   + `DEBUG`

   + `TRACE` – The largest amount of detail\.

1. Choose **Test Task** to verify that you can connect to your working folder, Amazon S3 bucket, and Amazon Redshift data warehouse\. The verification depends on the migration mode you chose\. 

1. Choose **Create** to create the task\.

1. Repeat the previous steps to create tasks for all the data that you want to migrate\. 

**To run and monitor tasks**

1. For **View**, choose **Data Migration View**\. The **Agents** tab appears\. 

1. Choose the **Tasks** tab\. Your tasks appear in the grid at the top as shown following\. You can see the status of a task in the top grid, and the status of its subtasks in the bottom grid\.   
![\[Tasks grid\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/TasksGrid.png)

1. Choose a task in the top grid and expand it\. Depending on the migration mode you chose, you see the task divided into **Extract**, **Upload**, and **Copy**\. 

1. Choose **Start** for a task to start that task\. You can monitor the status of your tasks while they work\. The subtasks run in parallel\. The extract, upload, and copy also run in parallel\. 

1. If you enabled logging when you set up the task, you can view the log: 

   1. Choose **Download Log**\. A message appears with the name of the folder that contains the log file\. Dismiss the message\. 

   1. A link appears in the **Task details** tab\. Choose the link to open the folder that contains the log file\. 

You can close AWS SCT, and your agents and tasks continue to run\. You can reopen AWS SCT later to check the status of your tasks and view the task logs\. 

## Data Extraction Task Output<a name="Agents.DW.MovingData"></a>

After your migration tasks complete, your data is ready\. Use the following information to determine how to proceed based on the migration mode you chose and the location of your data\. 


****  

| Migration Mode | Data Location | 
| --- | --- | 
|  **Extract, Upload and Copy**  |  The data is already in your Amazon Redshift data warehouse\. You can verify that the data is there, and start using it\. For more information, see [Connecting to Clusters From Client Tools and Code](http://docs.aws.amazon.com/redshift/latest/mgmt/connecting-via-client-tools.html)\.   | 
|  **Extract and Upload**  |  The extraction agents saved your data as files in your Amazon S3 bucket\. You can use the Amazon Redshift COPY command to load your data to Amazon Redshift\. For more information, see [Loading Data from Amazon S3](http://docs.aws.amazon.com/redshift/latest/dg/t_Loading-data-from-S3.html) in the Amazon Redshift documentation\.  There are multiple folders in your Amazon S3 bucket, corresponding to the extraction tasks that you set up\. When you load your data to Amazon Redshift, specify the name of the manifest file created by each task\. The manifest file appears in the task folder in your S3 bucket as shown following\.  ![\[File list in S3 bucket\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/S3FileList.png)  | 
|  **Extract Only**  |  The extraction agents saved your data as files in your working folder\. Manually copy your data to your Amazon S3 bucket, and then proceed with the instructions for **Extract and Upload**\.  | 

## Using Virtual Partitioning with AWS Schema Conversion Tool<a name="Agents.DW.VirtualPartitioning"></a>

You can often best manage large nonpartitioned tables by creating subtasks that create virtual partitions of the table data using filtering rules\. In AWS SCT, you can create virtual partitions for your migrated data\. There are three partition types, which work with specific data types:

+ The RANGE partition type works with numeric and date and time data types\.

+ The LIST partition type works with numeric, character, and date and time data types\.

+ The DATE AUTO SPLIT partition type works with date and time data types\.

AWS SCT validates the values you provide for creating a partition\. For example, if you attempt to partition a column with data type NUMERIC but you provide values of a different data type, AWS SCT throws an error\.

### Limits When Creating Virtual Partitioning<a name="Agents.DW.VirtualPartitioning.Limits"></a>

These are limitations to creating a virtual partition:

+ You can only use virtual partitioning only for nonpartitioned tables\.

+ You can use virtual partitioning only in the data migration view\.

+ You can't use the option UNION ALL VIEW with virtual partitioning\.

### RANGE Partition Type<a name="Agents.DW.VirtualPartitioning.Range"></a>

The RANGE partition type partitions data based on a range of column values for numeric and date and time data types\. This partition type creates a `WHERE` clause, and you provide the range of values for each partition\. You specify a list of values for the partitioned column in the box **Values**\. You can load value information by using a \.csv file\.

For example, you can create multiple partitions based on a value range you provide\. In the following example, the partitioning values for LO\_TAX are specified to create multiple partitions\.

```
Partition1: WHERE LO_TAX <= 10000.9
Partition2: WHERE LO_TAX > 10000.9 AND LO_TAX <= 15005.5
Partition3: WHERE LO_TAX > 15005.5 AND LO_TAX <= 25005.95
```

**To create a RANGE virtual partition**

1. Open the AWS SCT application\.

1. Choose **Data Migration View** mode\.

1. Choose the table where you want to set up virtual partitioning\. Open the context \(right\-click\) menu for the table, and choose **Add Virtual Partitioning**\.

1. In the **Add Virtual Partitioning** dialog box, enter the information as follows\.  
****    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/Agents.DW.html)

1. Choose **OK**\.

### LIST Partition Type<a name="Agents.DW.VirtualPartitioning.List"></a>

The LIST partition type partitions data based on column values for numeric, character, and date and time data types\. This partition type creates a `WHERE` clause, and you provide the values for each partition\. You specify a list of values for the partitioned column in the field **Values**\. You can load value information by using a \.csv file\.

For example, you can create multiple partitions based on a value you provide\. In the following example, the partitioning values for LO\_ORDERKEY are specified to create multiple partitions\.

```
Partition1: WHERE LO_ORDERKEY = 1
Partition2: WHERE LO_ORDERKEY = 2
Partition3: WHERE LO_ORDERKEY = 3
…
PartitionN: WHERE LO_ORDERKEY = USER_VALUE_N
```

You can also create a default partition for values not included in the ones specified\.

**To create a LIST virtual partition**

1. Open the AWS SCT application\.

1. Choose **Data Migration View** mode\.

1. Choose the table where you want to set up virtual partitioning\. Open the context \(right\-click\) menu for the table, and choose **Add Virtual Partitioning**\.

1. In the **Add Virtual Partitioning** dialog box, enter the information as follows\.  
****    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/Agents.DW.html)

1. Choose **OK**\.

### DATE AUTO SPLIT Partition Type<a name="Agents.DW.VirtualPartitioning.DateAutoSplit"></a>

The DATE AUTO SPLIT partition type partitions data of date and time data types based on a specified interval between a given start date and end date\. You specify the data range and interval \(day, week, month, or year\)\. If you don't specify a start date or end date, these values default to the current date\.

For example, you can create multiple partitions based on a date range you provide\. In the following example, the partitioning value range for LO\_ORDERDATE is specified to create multiple partitions\.

```
Partition1: WHERE LO_ORDERDATE >= ‘1954-10-10’ AND LO_ORDERDATE < ‘1954-10-24’
Partition2: WHERE LO_ORDERDATE >= ‘1954-10-24’ AND LO_ORDERDATE < ‘1954-11-06’
Partition3: WHERE LO_ORDERDATE >= ‘1954-11-06’ AND LO_ORDERDATE < ‘1954-11-20’
…
PartitionN: WHERE LO_ORDERDATE >= USER_VALUE_N AND LO_ORDERDATE <= ‘2017-08-13’
```

**To create a DATE AUTO SPLIT virtual partition**

1. Open the AWS SCT application\.

1. Choose **Data Migration View** mode\.

1. Choose the table where you want to set up virtual partitioning\. Open the context \(right\-click\) menu for the table, and choose **Add Virtual Partitioning**\.

1. In the **Add Virtual Partitioning** dialog box, enter information as follows\.  
****    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/Agents.DW.html)

1. Choose **OK**\.

## Migrating LOBs to Amazon Redshift<a name="Agents.DW.LOBs"></a>

Amazon Redshift doesn't support storing large binary objects \(LOBs\)\. However, if you need to migrate one or more LOBs to Amazon Redshift, AWS SCT can perform the migration\. To do so, AWS SCT uses an Amazon S3 bucket to store the LOBs and writes the URL for the S3 bucket into the migrated data stored in Amazon Redshift\.

**To migrate LOBs to Amazon Redshift**

1. Open an AWS SCT project\.

1. For **Actions**, choose **Create Local Task**\.

1. Choose the **Advanced** tab\.

1. For **S3 bucket LOBs folder**, type the name of the folder in an S3 bucket where you want the LOBs stored\.  
![\[LOBs in Local Settings dialog box\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/S3LOBs.png)

1. Choose **Create** to create the task\.

## Best Practices and Troubleshooting for Data Extraction Agents<a name="Agents.DW.BestPractices"></a>

The following are some best practices and troubleshooting suggestions for using extraction agents\. 


****  

| Issue | Troubleshooting Suggestions | 
| --- | --- | 
|  Performance is slow  |  To improve performance, we recommend the following:  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/Agents.DW.html)  | 
|  Contention delays  |  Avoid having too many agents accessing your data warehouse at the same time\.   | 
|  An agent goes down temporarily  |  If an agent is down, the status of each of its tasks appears as failed in AWS SCT\. If you wait, in some cases the agent can recover\. In this case, the status of its tasks updates in AWS SCT\.   | 
|  An agent goes down permanently  |  If the computer running an agent goes down permanently, and that agent is running a task, you can substitute a new agent to continue the task\. You can substitute a new agent only if the working folder of the original agent was not on the same computer as the original agent\. To substitute a new agent, do the following:  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/Agents.DW.html)  | 