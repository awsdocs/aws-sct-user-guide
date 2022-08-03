# Migrating data from an on\-premises data warehouse to Amazon Redshift<a name="agents.dw"></a>

You can use an AWS SCT agent to extract data from your on\-premises data warehouse and migrate it to Amazon Redshift\. The agent extracts your data and uploads the data to either Amazon S3 or, for large\-scale migrations, an AWS Snowball Edge device\. You can then use AWS SCT to copy the data to Amazon Redshift\.

Amazon S3 is a storage and retrieval service\. To store an object in Amazon S3, you upload the file you want to store to an Amazon S3 bucket\. When you upload a file, you can set permissions on the object and also on any metadata\.

**Large\-scale migrations**

Large\-scale data migrations can include many terabytes of information, and can be slowed by network performance and by the sheer amount of data that has to be moved\. AWS Snowball Edge is an AWS service you can use to transfer data to the cloud at faster\-than\-network speeds using an AWS\-owned appliance\. An AWS Snowball Edge device can hold up to 100 TB of data\. It uses 256\-bit encryption and an industry\-standard Trusted Platform Module \(TPM\) to ensure both security and full chain\-of\-custody for your data\. AWS SCT works with AWS Snowball Edge devices\. 

When you use AWS SCT and an AWS Snowball Edge device, you migrate your data in two stages\. First, you use AWS SCT to process the data locally and then move that data to the AWS Snowball Edge device\. You then send the device to AWS using the AWS Snowball Edge process, and then AWS automatically loads the data into an Amazon S3 bucket\. Next, when the data is available on Amazon S3, you use AWS SCT to migrate the data to Amazon Redshift\. Data extraction agents can work in the background while AWS SCT is closed\.

The following diagram shows the supported scenario\.

![\[Extraction agent architecture\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/extraction-agents-art.png)

Data extraction agents are currently supported for the following source data warehouses:
+ Greenplum Database \(version 4\.3\)
+ Microsoft SQL Server \(version 2008 and later\)
+ Netezza \(version 7\.0\.3 and later\)
+ Oracle \(version 10 and later\)
+ Teradata \(version 13 and later\)
+ Vertica \(version 7\.2\.2 and later\)
+ Azure SQL Data Warehouse \(Azure Synapse\)

You can connect to FIPS endpoints for Amazon Redshift if you need to comply with the Federal Information Processing Standard \(FIPS\) security requirements\. FIPS endpoints are available in the following AWS Regions: 
+ US East \(N\. Virginia\) Region \(redshift\-fips\.us\-east\-1\.amazonaws\.com\)
+ US East \(Ohio\) Region \(redshift\-fips\.us\-east\-2\.amazonaws\.com\)
+ US West \(N\. California\) Region \(redshift\-fips\.us\-west\-1\.amazonaws\.com\)
+ US West \(Oregon\) Region \(redshift\-fips\.us\-west\-2\.amazonaws\.com\)

Use the information in the following topics to learn how to work with data extraction agents\. 

**Topics**
+ [Prerequisites for using data extraction agents](#agents.PreReqSettings)
+ [Installing extraction agents](#agents.Installing)
+ [Registering extraction agents with the AWS Schema Conversion Tool](#agents.Using)
+ [Hiding and recovering information for an AWS SCT agent](#agents.Recovering)
+ [Creating data migration rules in AWS SCT](#agents.Filtering)
+ [Changing extractor and copy settings from project settings](#agents.ProjectSettings)
+ [Sorting data before migrating using AWS SCT](#agents.Sorting)
+ [Creating, running, and monitoring an AWS SCT data extraction task](#agents.Tasks)
+ [Exporting and importing an AWS SCT data extraction task](#agents.ExportImportTasks)
+ [Data extraction using an AWS Snowball Edge device](#agents.Snowball)
+ [Data extraction task output](#agents.MovingData)
+ [Using virtual partitioning with AWS Schema Conversion Tool](#agents.VirtualPartitioning)
+ [Migrating LOBs to Amazon Redshift](#agents.LOBs)
+ [Best practices and troubleshooting for data extraction agents](#agents.BestPractices)

## Prerequisites for using data extraction agents<a name="agents.PreReqSettings"></a>

Before you work with data extraction agents, store your Amazon S3 bucket information and set up your Secure Sockets Layer \(SSL\) trust and key store\.

### Amazon S3 settings<a name="agents.S3Credentials"></a>

After your agents extract your data, they upload it to your Amazon S3 bucket\. Before you continue, you must provide the credentials to connect to your AWS account and your Amazon S3 bucket\. You store your credentials and bucket information in a profile in the global application settings, and then associate the profile with your AWS SCT project\. If necessary, choose **Global settings** to create a new profile\. For more information, see [Storing AWS service profiles in the AWS SCT](CHAP_UserInterface.md#CHAP_UserInterface.Profiles)\. 

### Assuming IAM roles<a name="agents.PreReqSettings.IAMroles"></a>

For additional security, you can use AWS Identity and Access Management \(IAM\) roles to access your Amazon S3 bucket\. To do so, create an IAM user for your data extraction agents without any permissions\. Then, create an IAM role that enables Amazon S3 access, and specify the list of services and users that can assume this role\. For more information, see [IAM roles](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles.html) in the *IAM User Guide*\. 

**To configure IAM roles to access your Amazon S3 bucket**

1. Create a new IAM user\. For user credentials, choose **Programmatic access** type\.

1. Configure the host environment so that your data extraction agent can assume the role that AWS SCT provides\. Make sure that the user that you configured in the previous step enables data extraction agents to use the credential provider chain\. For more information, see [Using credentials](https://docs.aws.amazon.com/sdk-for-java/latest/developer-guide/credentials.html) in the *AWS SDK for Java Developer Guide*\.

1. Create a new IAM role that has access to your Amazon S3 bucket\.

1. Modify the trust section of this role to trust the user that you created before to assume the role\. In the following example, replace `111122223333:user/DataExtractionAgentName` with the name of your IAM user\.

   ```
   {
       "Effect": "Allow",
       "Principal": {
           "AWS": "arn:aws:iam::111122223333:user/DataExtractionAgentName"
       },
       "Action": "sts:AssumeRole"
   }
   ```

1. Modify the trust section of this role to trust `redshift.amazonaws.com` to assume the role\.

   ```
   {
       "Effect": "Allow",
       "Principal": {
           "Service": [
               "redshift.amazonaws.com"
           ]
       },
       "Action": "sts:AssumeRole"
   }
   ```

1. Attach this role to your Amazon Redshift cluster\.

Now, you can run your data extraction agent in AWS SCT\.

When you use IAM role assuming, the data migration works the following way\. The data extraction agent starts and gets the user credentials using the credential provider chain\. Next, you create a data migration task in AWS SCT, then specify the IAM role for data extraction agents to assume, and start the task\. AWS Security Token Service \(AWS STS\) generates temporary credentials to access Amazon S3\. The data extraction agent uses these credentials to upload data to Amazon S3\.

Then, AWS SCT provides Amazon Redshift with the IAM role\. In turn, Amazon Redshift gets new temporary credentials from AWS STS to access Amazon S3\. Amazon Redshift uses these credentials to copy data from Amazon S3 to your Amazon Redshift table\.

### Security settings<a name="agents.Installing.Security"></a>

The AWS Schema Conversion Tool and the extraction agents can communicate through Secure Sockets Layer \(SSL\)\. To enable SSL, set up a trust store and key store\. 

**To set up secure communication with your extraction agent**

1. Start the AWS Schema Conversion Tool\.

1. Open the **Settings** menu, and then choose **Global settings**\. The **Global settings** dialog box appears\. 

   Choose the **Security** tab as shown following\.   
![\[The Security tab on the Global Settings dialog box\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/SecuritySettings.png)

1. Choose **Generate trust and key store**, or choose **Select existing trust store**\. 

   If you choose **Generate trust and key store**, you then specify the name and password for the trust and key stores, and the path to the location for the generated files\. You use these files in later steps\. 

   If you choose **Select existing trust store**, you then specify the password and file name for the trust and key stores\. You use these files in later steps\. 

1. After you have specified the trust store and key store, choose **OK** to close the **Global settings** dialog box\. 

## Installing extraction agents<a name="agents.Installing"></a>

We recommend that you install multiple extraction agents on individual computers, separate from the computer that is running the AWS Schema Conversion Tool\.

Extraction agents are currently supported on the following operating systems:
+ Microsoft Windows
+ Red Hat Enterprise Linux \(RHEL\) 6\.0
+ Ubuntu Linux \(version 14\.04 and later\)

Use the following procedure to install extraction agents\. Repeat this procedure for each computer that you want to install an extraction agent on\.

**To install an extraction agent**

1. If you have not already downloaded the AWS SCT installer file, follow the instructions at [Installing, verifying, and updating AWS SCT](CHAP_Installing.md) to download it\. The \.zip file that contains the AWS SCT installer file also contains the extraction agent installer file\.

1. Download and install the latest version of Amazon Corretto 11\. For more information, see [Downloads for Amazon Corretto 11](https://docs.aws.amazon.com/corretto/latest/corretto-11-ug/downloads-list.html) in the *Amazon Corretto 11 User Guide*\.

1. Locate the installer file for your extraction agent in a subfolder named agents\. For each computer operating system, the correct file to install the extraction agent is shown following\.  
****    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/agents.dw.html)

1. Install the extraction agent on a separate computer by copying the installer file to the new computer\. 

1. Run the installer file\. Use the instructions for your operating system, shown following\.   
****    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/agents.dw.html)

1. Choose **Next**, accept the license agreement, and choose **Next**\.

1. Enter the path to install the AWS SCT data extraction agent, and choose **Next**\.

1. Choose **Install** to install your data extraction agent\.

   AWS SCT installs your data extraction agent\. To complete the installation, configure your data extraction agent\. AWS SCT automatically launches the configuration setup program\. For more information, see [Configuring extraction agents](#agents.Installing.AgentSettings)\. 

1. Choose **Finish** to close the installation wizard after you configure your data extraction agent\.

### Configuring extraction agents<a name="agents.Installing.AgentSettings"></a>

Use the following procedure to configure extraction agents\. Repeat this procedure on each computer that has an extraction agent installed\. 

**To configure your extraction agent**

1. Launch the configuration setup program: 
   + On Microsoft Windows, AWS SCT launches the configuration setup program automatically during the installation of a data extraction agent\. 

     As needed, launch the setup program manually on Windows using the following command\.

     ```
     cd path/AWSSchemaConversionTool-Extractor.jar
     java -jar AWSSchemaConversionTool-Extractor.jar -config
     ```

     In the preceding example, `path` is the path where you installed the AWS SCT data extraction agent\.
   + On RHEL and Ubuntu, run the `sct-extractor-setup.sh` file from the location where you installed the agent\. 

   The setup program prompts you for information\. For each prompt, a default value appears\.

1. Accept the default value at each prompt, or enter a new value\. 

   Specify the following information: 
   + For **Listening port**, enter the port number the agent listens on\.
   + For **Add a source vendor**, enter **yes**, and then enter your source data warehouse platform\.
   + For **JDBC driver**, enter the location where you installed the JDBC drivers\.
   + For **Working folder**, enter the path where the AWS SCT data extraction agent will store the extracted data\. The working folder can be on a different computer from the agent, and a single working folder can be shared by multiple agents on different computers\.
   + For **Enable SSL communication**, enter **yes**\.
   + For **Key store**, enter the location of the key store file\.
   + For **Key store password**, enter the password for the key store\.
   + For **Enable client SSL authentication**, enter **yes**\.
   + For **Trust store**, enter the location of the trust store file\.
   + For **Trust store password**, enter the password for the trust store\.

The setup program updates the settings file for the extraction agent\. The settings file is named `settings.properties`, and is located where you installed the extraction agent\. 

The following is a sample settings file\. 

```
 1. $ cat settings.properties
 2. #extractor.start.fetch.size=20000
 3. #extractor.out.file.size=10485760
 4. #extractor.source.connection.pool.size=20
 5. #extractor.source.connection.pool.min.evictable.idle.time.millis=30000 
 6. #extractor.extracting.thread.pool.size=10
 7. vendor=TERADATA
 8. driver.jars=/usr/share/lib/jdbc/terajdbc4.jar
 9. port=8192
10. redshift.driver.jars=/usr/share/lib/jdbc/RedshiftJDBC42-1.2.43.1067.jar 
11. working.folder=/data/sct
12. extractor.private.folder=/home/ubuntu
13. ssl.option=OFF
```

To change configuration settings, you can edit the `settings.properties` file using a text editor or run the agent configuration again\.

### Installing and configuring extraction agents with dedicated copying agents<a name="agents.Installing.CopyingAgent"></a>

You can install extraction agents in a configuration that has shared storage and a dedicated copying agent\. The following diagram illustrates this scenario\.  

![\[Extractor agents with dedicated copy agent configuration\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/dedicated-copy-agent3.png)

That configuration can be useful when a source database server supports up to 120 connections, and your network has ample storage attached\. Use the procedure following to configure extraction agents that have a dedicated copying agent\.

**To install and configure extraction agents and a dedicated copying agent**

1. Make sure that the working directory of all extracting agents uses the same folder on shared storage\.

1. Install extractor agents by following the steps in [Installing extraction agents](#agents.Installing)\.

1. Configure extraction agents by following the steps in [Configuring extraction agents](#agents.Installing.AgentSettings), but specify only the source JDBC driver\.

1. Configure a dedicated copying agent by following the steps in [Configuring extraction agents](#agents.Installing.AgentSettings), but specify only an Amazon Redshift JDBC driver\.

### Starting extraction agents<a name="agents.Installing.AgentStart"></a>

Use the following procedure to start extraction agents\. Repeat this procedure on each computer that has an extraction agent installed\. 

Extraction agents act as listeners\. When you start an agent with this procedure, the agent starts listening for instructions\. You send the agents instructions to extract data from your data warehouse in a later section\. 

**To start your extraction agent**
+ On the computer that has the extraction agent installed, run the command listed following for your operating system\.   
****    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/agents.dw.html)

To check the status of the agent, run the same command but replace `start` with `status`\. 

To stop an agent, run the same command but replace `start` with `stop`\. 

## Registering extraction agents with the AWS Schema Conversion Tool<a name="agents.Using"></a>

You manage your extraction agents by using AWS SCT\. The extraction agents act as listeners\. When they receive instructions from AWS SCT, they extract data from your data warehouse\. 

Use the following procedure to register extraction agents with your AWS SCT project\. 

**To register an extraction agent**

1. Start the AWS Schema Conversion Tool, and open a project\. 

1. Open the **View** menu, and then choose **Data Migration view \(other\)**\. The **Agents** tab appears\. If you have previously registered agents, AWS SCT displays them in a grid at the top of the tab\. 

1. Choose **Register**\.

   After you register an agent with an AWS SCT project, you can't register the same agent with a different project\. If you're no longer using an agent in an AWS SCT project, you can unregister it\. You can then register it with a different project\. 

1. Choose **Redshift data agent**, and then choose **OK**\.

1. Enter your information on the **Connection** tab of the dialog box: 

   1. For **Description**, enter a description of the agent\. 

   1. For **Host Name**, enter the host name or IP address of the computer of the agent\. 

   1. For **Port**, enter the port number that the agent is listening on\. 

   1. Choose **Register** to register the agent with your AWS SCT project\. 

1. Repeat the previous steps to register multiple agents with your AWS SCT project\. 

## Hiding and recovering information for an AWS SCT agent<a name="agents.Recovering"></a>

An AWS SCT agent encrypts a significant amount of information, for example passwords to user key\-trust stores, database accounts, AWS account information, and similar items\. It does so using a special file called `seed.dat`\. By default, the agent creates this file in the working folder of the user who first configures the agent\.

Because different users can configure and run the agent, the path to `seed.dat` is stored in the `{extractor.private.folder}` parameter of the `settings.properties` file\. When the agent starts, it can use this path to find the `seed.dat` file to access the key\-trust store information for the database it acts on\.

You might need to recover passwords that an agent has stored in these cases:
+ If the user loses the `seed.dat` file and the AWS SCT agent's location and port didn't change\.
+ If the user loses the `seed.dat` file and the AWS SCT agent's location and port has changed\. In this case, the change usually occurs because the agent was migrated to another host or port and the information in the `seed.dat` file is no longer valid\.

In these cases, if an agent is started without SSL, it starts and then accesses the previously created agent storage\. It then goes to the **Waiting for recovery** state\. 

However, in these cases, if an agent is started with SSL you can't restart it\. This is because the agent can't decrypt the passwords to certificates stored in the `settings.properties` file\. In this type of startup, the agent fails to start\. An error similar to the following is written in the log: "The agent could not start with SSL mode enabled\. Please reconfigure the agent\. Reason: The password for keystore is incorrect\." 

To fix this, create a new agent and configure the agent to use the existing passwords for accessing the SSL certificates\. To do so, use the following procedure\. 

After you perform this procedure, the agent should run and go to the **Waiting for recovery** state\. AWS SCT automatically sends the needed passwords to an agent in the **Waiting for recovery** state\. When the agent has the passwords, it restarts any tasks\. No further user action is required on the AWS SCT side\.

**To reconfigure the agent and restore passwords for accessing SSL certificates**

1. Install a new AWS SCT agent and run configuration\. 

1. Change the `agent.name` property in the `instance.properties` file to the name of the agent the storage was created for, to have the new agent work with existing agent storage\. 

   The `instance.properties` file is stored in the agent's private folder, which is named using the following convention: `{output.folder}\dmt\{hostName}_{portNumber}\`\. 

1. Change the name of `{output.folder}` to that of the previous agent's output folder\.

   At this point, AWS SCT is still trying to access the old extractor at the old host and port\. As a result, the inaccessible extractor gets the status FAILED\. You can then change the host and port\.

1. Modify the host, port, or both for the old agent by using the Modify command to redirect the request flow to the new agent\. 

When AWS SCT can ping the new agent, AWS SCT receives the status **Waiting for recovery** from the agent\. AWS SCT then automatically recovers the passwords for the agent\.

Each agent that works with the agent storage updates a special file called `storage.lck` located at `{output.folder}\{agentName}\storage\`\. This file contains the agent's network ID and the time until which the storage is locked\. When the agent works with the agent storage, it updates the `storage.lck` file and extends the lease of the storage by 10 minutes every 5 minutes\. No other instance can work with this agent storage before the lease expires\.

## Creating data migration rules in AWS SCT<a name="agents.Filtering"></a>

Before you extract your data with the AWS Schema Conversion Tool, you can set up filters that reduce the amount of data that you extract\. You can create data migration rules by using `WHERE` clauses to reduce the data that you extract\. For example, you can write a `WHERE` clause that selects data from a single table\. 

You can create data migration rules and save the filters as part of your project\. With your project open, use the following procedure to create data migration rules\. 

**To create data migration rules**

1. Open the **View** menu, and then choose **Data Migration view \(other\)**\.

1.  Choose **Data migration rules**, and then choose **Add new rule**\.

1. Configure your data migration rule: 

   1. For **Name**, enter a name for your data migration rule\. 

   1. For **Where schema name is like**, enter a filter to apply to schemas\. In this filter, a `WHERE` clause is evaluated by using a `LIKE` clause\. To choose one schema, enter an exact schema name\. To choose multiple schemas, use the “%” character as a wildcard to match any number of characters in the schema name\.

   1. For **table name like**, enter a filter to apply to tables\. In this filter, a `WHERE` clause is evaluated by using a `LIKE` clause\. To choose one table, enter an exact name\. To choose multiple tables, use the “%” character as a wildcard to match any number of characters in the table name\.

   1. For **Where clause**, type a `WHERE` clause to filter data\. 

1. After you have configured your filter, choose **Save** to save your filter, or **Cancel** to cancel your changes\. 

1. After you are done adding, editing, and deleting filters, choose **Save all** to save all your changes\. 

To turn off a filter without deleting it, use the toggle icon\. To duplicate an existing filter, use the copy icon\. To delete an existing filter, use the delete icon\. To save any changes you make to your filters, choose **Save all**\. 

## Changing extractor and copy settings from project settings<a name="agents.ProjectSettings"></a>

From the **Project settings** window in AWS SCT, you can choose settings for data extraction agents and the Amazon Redshift `COPY` command\.

To choose these settings, choose **Settings**, **Project settings**, and then choose **Data migration**\. Here, you can edit **Extraction settings**, **Amazon S3 settings**, and **Copy settings**\.

Use the instructions in the following table to provide the information for **Extraction settings**\.


| For this parameter | Do this | 
| --- | --- | 
| **Compression format** | Specify the compression format of the input files\. Choose one of the following options: **GZIP**, **BZIP2**, **ZSTD**, or **No compression**\. | 
| **Delimiter character** | Specify the ASCII character that separates fields in the input files\. Nonprinting characters aren't supported\. | 
| **NULL value as a string** | Turn this option on if your data includes a null terminator\. If this option is turned off, the Amazon Redshift `COPY` command treats null as an end of the record and ends the load process\. | 
| **Sorting strategy** | Use sorting to restart the extraction from the point of failure\. Choose one of the following sorting strategies: **Use sorting after the first fail \(recommended\)**, **Use sorting if possible**, or **Never use sorting**\. For more information, see [Sorting data before migrating using AWS SCT](#agents.Sorting)\. | 
| **Source temp schema** | Enter the name of the schema in the source database, where the extraction agent can create the temporary objects\. | 
| **Out file size \(in MB\)** | Enter the size, in MB, of the files uploaded to Amazon S3\.  | 
| **Snowball out file size \(in MB\)** | Enter the size, in MB, of the files uploaded to AWS Snowball\. Files can be 1–1,000 MB in size\.  | 
| **Use table partitioning if it is supported by DB server and table size \(in MB\) is more than** | Turn this option on to use table partitioning, and then enter the size of tables to partition\. | 
| **Extract LOBs** | Turn this option on to extract large objects \(LOBs\) from your source database\. LOBs include BLOBs, CLOBs, NCLOBs, XML files, and so on\. For every LOB, AWS SCT extraction agents create a data file\. | 
| **Amazon S3 bucket LOBs folder** | Enter the location for AWS SCT extraction agents to store LOBs\. | 
| **Apply RTRIM to string columns** | Turn this option on to trim a specified set of characters from the end of the extracted strings\. | 
| **Keep files locally after upload to Amazon S3** | Turn this option on to keep files on your local machine after data extraction agents upload them to Amazon S3\. | 

Use the instructions in the following table to provide the information for **Amazon S3 settings**\.


| For this parameter | Do this | 
| --- | --- | 
| **Use proxy** | Turn this option on to use a proxy server to upload data to Amazon S3\. Then choose the data transfer protocol, enter the host name, port, user name, and password\. | 
| **Endpoint type** | Choose **FIPS** to use the Federal Information Processing Standard \(FIPS\) endpoint\. Choose **VPCE** to use the virtual private cloud \(VPC\) endpoint\. Then for **VPC endpoint**, enter the Domain Name System \(DNS\) of your VPC endpoint\. | 
| **Keep files on Amazon S3 after copying to Amazon Redshift** | Turn this option on to keep extracted files on Amazon S3 after copying these files to Amazon Redshift\. | 

Use the instructions in the following table to provide the information for **Copy settings**\.


| For this parameter | Do this | 
| --- | --- | 
| **Maximum error count** | Enter the number of load errors\. After the operation reaches this limit, the AWS SCT data extraction agents end the data load process\. The default value is 0, which means that the AWS SCT data extraction agents continue the data load regardless of the failures\. | 
| **Replace not valid UTF\-8 characters** | Turn this option on to replace not valid UTF\-8 characters with the specified character and continue the data load operation\. | 
| **Use blank as null value** | Turn this option on to load blank fields that consist of white space characters as null\. | 
| **Use empty as null value** | Turn this option on to load empty `CHAR` and `VARCHAR` fields as null\. | 
| **Truncate columns** | Turn this option on to truncate data in columns to fit the data type specification\. | 
| **Automatic compression** | Turn this option on to apply compression encoding during a copy operation\. | 
| **Automatic statistics refresh** | Turn this option on to refresh the statistics at the end of a copy operation\. | 
| **Check file before load** | Turn this option on to validate data files before loading them to Amazon Redshift\. | 

## Sorting data before migrating using AWS SCT<a name="agents.Sorting"></a>

Sorting your data before migration with AWS SCT provides some benefits\. If you sort data first, AWS SCT can restart the extraction agent at the last saved point after a failure\. Also, if you are migrating data to Amazon Redshift and you sort data first, AWS SCT can insert data into to Amazon Redshift faster\. 

These benefits have to do with how AWS SCT creates data extraction queries\. In some cases, AWS SCT uses the DENSE\_RANK analytic function in these queries\. However, DENSE\_RANK can use lots of time and server resources to sort the dataset that results from extraction, so if AWS SCT can work without it, it does\.

**To sort data before migrating using AWS SCT**

1. Open an AWS SCT project\.

1. Open the context \(right\-click\) menu for the object, and then choose **Create Local task**\.

1. Choose the **Advanced** tab, and for **Sorting strategy**, choose an option:
   + **Never use sorting** – The extraction agent doesn't use the DENSE\_RANK analytic function and restarts from the beginning if a failure occurs\.
   + **Use sorting if possible** – The extraction agent uses DENSE\_RANK if the table has a primary key or a unique constraint\.
   + **Use sorting after first fail \(recommended\)** – The extraction agent first tries to get the data without using DENSE\_RANK\. If the first attempt fails, the extraction agent rebuilds the query using DENSE\_RANK and preserves its location in case of failure\.  
![\[The Security tab on the Global Settings dialog box\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/local-task-sorting.png)

1.  Set additional parameters as described following, and then choose **Create **to create your data extraction task\. 

## Creating, running, and monitoring an AWS SCT data extraction task<a name="agents.Tasks"></a>

Use the following procedures to create, run, and monitor data extraction tasks\. 

**To assign tasks to agents and migrate data**

1. In the AWS Schema Conversion Tool, after you have converted your schema, choose one or more tables from the left panel of your project\. 

   You can choose all tables, but we recommend against that for performance reasons\. We recommend that you create multiple tasks for multiple tables based on the size of the tables in your data warehouse\. 

1. Open the context \(right\-click\) menu for each table, and then choose **Create task**\. The **Create Local task** dialog box opens, as shown following\.   
![\[Task dialog box\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/TaskDialog.png)

1. For **Task name**, type a name for the task\. 

1. For **Migration mode**, choose one of the following: 
   + **Extract only** – Extract your data, and save the data to your local working folders\. 
   + **Extract and upload** – Extract your data, and upload your data to Amazon S3\. 
   + **Extract, upload and copy** – Extract your data, upload your data to Amazon S3, and copy it into your Amazon Redshift data warehouse\. 

1. For **Encryption type**, choose one of the following: 
   + **NONE** – Turn off data encryption for the entire data migration process\. 
   + **CSE\_SK** – Use client\-side encryption with a symmetric key to migrate data\. AWS SCT automatically generates encryption keys and transmits them to data extraction agents using Secure Sockets Layer \(SSL\)\. AWS SCT doesn't encrypt large objects \(LOBs\) during data migration\. 

1. Choose **Extract LOBs** to extract large objects\. If you don't need to extract large objects, you can clear the check box\. Doing this reduces the amount of data that you extract\. 

1. To see detailed information about a task, choose **Enable task logging**\. You can use the task log to debug problems\. 

   If you enable task logging, choose the level of detail that you want to see\. The levels are the following, with each level including all messages from the previous level: 
   + `ERROR` – The smallest amount of detail\.
   + `WARNING`
   + `INFO`
   + `DEBUG`
   + `TRACE` – The largest amount of detail\.

1. To assume a role to an IAM user that your data extraction agent uses, choose **Amazon S3 settings**\. For **IAM role**, enter the name of the role to use\. For **Region**, choose the AWS Region for this role\.

1. Choose **Test task** to verify that you can connect to your working folder, Amazon S3 bucket, and Amazon Redshift data warehouse\. The verification depends on the migration mode you chose\. 

1. Choose **Create** to create the task\.

1. Repeat the previous steps to create tasks for all the data that you want to migrate\. 

**To run and monitor tasks**

1. For **View**, choose **Data Migration view**\. The **Agents** tab appears\. 

1. Choose the **Tasks** tab\. Your tasks appear in the grid at the top as shown following\. You can see the status of a task in the top grid, and the status of its subtasks in the bottom grid\.   
![\[Tasks grid\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/TasksGrid.png)

1. Choose a task in the top grid and expand it\. Depending on the migration mode you chose, you see the task divided into **Extract**, **Upload**, and **Copy**\. 

1. Choose **Start** for a task to start that task\. You can monitor the status of your tasks while they work\. The subtasks run in parallel\. The extract, upload, and copy also run in parallel\. 

1. If you enabled logging when you set up the task, you can view the log: 

   1. Choose **Download log**\. A message appears with the name of the folder that contains the log file\. Dismiss the message\. 

   1. A link appears in the **Task details** tab\. Choose the link to open the folder that contains the log file\. 

You can close AWS SCT, and your agents and tasks continue to run\. You can reopen AWS SCT later to check the status of your tasks and view the task logs\. 

You can save data extraction tasks to your local disk and restore them to the same or another project by using export and import\. To export a task, make sure that you have at least one extraction task created in a project\. You can import a single extraction task or all of the tasks created in the project\.

When you export an extraction task, AWS SCT creates a separate `.xml` file for that task\. The `.xml` file stores that task's metadata information, such as task properties, description, and subtasks\. The `.xml` file doesn't contain information about processing of an extraction task\. Information like the following is recreated when the task is imported:
+ Task progress
+ Subtask and stage states
+ Distribution of extracting agents by subtasks and stages
+ Task and subtask IDs
+ Task name

## Exporting and importing an AWS SCT data extraction task<a name="agents.ExportImportTasks"></a>

You can quickly save an existing task from one project and restore it in another project \(or the same project\) using AWS SCT export and import\. Use the following procedure to export and import data extraction tasks\.

**To export and import a data extraction task**

1. For **View**, choose **Data Migration view**\. The **Agents** tab appears\. 

1. Choose the **Tasks** tab\. Your tasks are listed in the grid that appears\.

1. Choose the three vertically aligned dots \(ellipsis icon\) located at the lower right corner under the list of tasks\.

1. Choose **Export task** from the pop\-up menu\.

1. Choose the folder where you want AWS SCT to place the task export `.xml` file\. 

   AWS SCT creates the task export file with a file name format of `TASK-DESCRIPTION_TASK-ID.xml`\.

1. Choose the three vertically aligned dots \(ellipsis icon\) at lower right under the list of tasks\.

1. Choose **Import task** from the pop\-up menu\.

   You can import an extraction task to a project connected to the source database, and the project has at least one active registered extraction agent\.

1. Select the `.xml` file for the extraction task you exported\.

   AWS SCT gets the extraction task's parameters from the file, creates the task, and adds the task to the extracting agents\.

1. Repeat these steps to export and import additional data extraction tasks\.

At the end of this process, your export and import are complete and your data extraction tasks are ready for use\.

## Data extraction using an AWS Snowball Edge device<a name="agents.Snowball"></a>

The process of using AWS SCT and AWS Snowball Edge has several steps\. The migration involves a local task, where AWS SCT uses a data extraction agent to move the data to the AWS Snowball Edge device, then an intermediate action where AWS copies the data from the AWS Snowball Edge device to an Amazon S3 bucket\. The process finishes AWS SCT loading the data from the Amazon S3 bucket to Amazon Redshift\.

The sections following this overview provide a step\-by\-step guide to each of these tasks\. The procedure assumes that you have AWS SCT installed and that you have configured and registered a data extraction agent on a dedicated machine\.

The following steps need to occur to migrate data from a local data store to an AWS data store using AWS Snowball Edge\.

1. Create an AWS Snowball Edge job using the AWS Snowball console\. For more information, see [Creating an AWS Snowball Edge Job](https://docs.aws.amazon.com/snowball/latest/developer-guide/create-job-common.html) in the *AWS Snowball Edge Developer Guide*\.

1. Unlock the AWS Snowball Edge device using the local, dedicated Linux machine\.

1. Create a new project in AWS SCT using the registered data extraction agent\.

1. Install the database driver for your source database on the dedicated machine where you installed the data extractor\. 

1. Create and set permissions for the Amazon S3 bucket to use\. 

1. Create **Local & DMS Task** in AWS SCT\.

1. Run and monitor the **Local & DMS Task** in AWS SCT\.

1. Run the AWS SCT task and monitor progress in AWS SCT\.

### Step\-by\-step procedures for migrating data using AWS SCT and AWS Snowball Edge<a name="agents.Snowball.SBS"></a>

The following sections provide detailed information on the migration steps\.

#### Step 1: Create an AWS Snowball Edge job<a name="agents.Snowball.SBS.OrderSnowball"></a>

Create an AWS Snowball job by following the steps outlined in the section [Creating an AWS Snowball Edge Job](https://docs.aws.amazon.com/snowball/latest/developer-guide/create-job-common.html) in the *AWS Snowball Edge Developer Guide*\.

#### Step 2: Unlock the AWS Snowball Edge device<a name="agents.Snowball.SBS.UnlockSnowball"></a>

Run the commands that unlock and provide credentials to the Snowball Edge device from the machine where you installed the AWS DMS agent\. This way, you can be sure that the AWS DMS agent call connects to the AWS Snowball Edge device\. For more information about unlocking the AWS Snowball Edge device, see [Unlocking the Snowball Edge](https://docs.aws.amazon.com/snowball/latest/developer-guide/unlockdevice.html)\.

For example, the following command lists the Amazon S3 bucket used by the device\. 

```
aws s3 ls s3://<bucket-name> --profile <Snowball Edge profile> --endpoint http://<Snowball IP>:8080 --recursive 
```

#### Step 3: Create a new AWS SCT project<a name="agents.Snowball.SBS.NewSCTProject"></a>

Next, create a new AWS SCT project\.

**To create a new project in AWS SCT**

1. Start the AWS Schema Conversion Tool\. On the **File** menu, choose **New project**\. The **New project** dialog box appears\. 

1.  Enter a name for your project, which is stored locally on your computer\. 

1.  Enter the location for your local project file\. 

1. Choose **OK** to create your AWS SCT project\. 

1. Choose **Add source** to add a new source database to your AWS SCT project\. 

1. Choose **Add target** to add a new target platform in your AWS SCT project\. 

1. Choose the source database schema in the left panel\. 

1. In the right panel, specify the target database platform for the selected source schema\. 

1. Choose **Create mapping**\. This button becomes active after you choose the source database schema and the target database platform\. 

#### Step 4: Install the source database driver for the AWS DMS agent on the Linux computer<a name="agents.Snowball.SBS.SourceDriver"></a>

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
lrwxrwxrwx 1 oracle oracle 63 Oct 2 14:16 libclntsh.so ->
                            /u01/app/oracle/home/lib/libclntsh.so.12.1
```
In addition, the LD\_LIBRARY\_PATH environment variable should be appended with the Oracle lib directory and added to the site\_arep\_login\.sh script under the lib folder of the installation\. Add this script if it doesn't exist\.  

```
vi cat <product dir>/bin/site_arep_login.sh
```

```
export ORACLE_HOME=/usr/lib/oracle/12.2/client64; export
                            LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$ORACLE_HOME/lib
```

**To install on Microsoft SQL Server **  
Install the Microsoft ODBC Driver\.  
Update the site\_arep\_login\.sh with the following code\.  

```
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/opt/microsoft/msodbcsql/lib64/
```
**Simba ODBC Driver **  
 Install the Microsoft ODBC Driver\.  
 Edit the simba\.sqlserverodbc\.ini file as follows\.  

```
DriverManagerEncoding=UTF-16
ODBCInstLib=libodbcinst.so
```

**To install on SAP Sybase**  
The SAP Sybase ASE ODBC 64\-bit client should be installed\.  
If the installation directory is /opt/sap, update the site\_arep\_login\.sh with the following\.  

```
export SYBASE_HOME=/opt/sap
export                          
LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$SYBASE_HOME/
   DataAccess64/ODBC/lib:$SYBASE_HOME/DataAccess/ODBC/
   lib:$SYBASE_HOME/OCS-16_0/lib:$SYBASE_HOME/OCS-16_0/
   lib3p64:$SYBASE_HOME/OCS-16_0/lib3p
```
The /etc/odbcinst\.ini should include the following entries\.  

```
[Sybase]
Driver=/opt/sap/DataAccess64/ODBC/lib/libsybdrvodb.so
Description=Sybase ODBC driver
```

**To install on MySQL**  
Install MySQL Connector/ODBC for Linux, version 5\.2\.6 or later\.   
 Make sure that the /etc/odbcinst\.ini file contains an entry for MySQL, as in the following example\.  

```
[MySQL ODBC 5.2.6 Unicode Driver]
Driver = /usr/lib64/libmyodbc5w.so 
UsageCount = 1
```

**To install on PostgreSQL**  
Install postgresql94\-9\.4\.4\-1PGDG\.<OS Version>\.x86\_64\.rpm\. This is the package that contains the psql executable\.  
For example, postgresql94\-9\.4\.4\-1PGDG\.rhel7\.x86\_64\.rpm is the package required for Red Hat 7\.  
Install the ODBC driver postgresql94\-odbc\-09\.03\.0400\-1PGDG\.<OS version>\.x86\_64 or above for Linux, where <OS version> is the OS of the agent machine\.  
For example, postgresql94\-odbc\-09\.03\.0400\-1PGDG\.rhel7\.x86\_64 is the client required for Red Hat 7\.  
Make sure that the /etc/odbcinst\.ini file contains an entry for PostgreSQL, as in the following example\.  

```
[PostgreSQL]
Description = PostgreSQL ODBC driver
Driver = /usr/pgsql-9.4/lib/psqlodbc.so
Setup = /usr/pgsql-9.4/lib/psqlodbcw.so
Debug = 0
CommLog = 1
UsageCount = 2
```

#### Step 5: Configure AWS SCT to access the Amazon S3 bucket<a name="agents.Snowball.SBS.ConfigureS3"></a>

For information on configuring an Amazon S3 bucket, see [Working with Amazon S3 buckets](http://docs.aws.amazon.com/AmazonS3/latest/dev/UsingBucket.html) in the Amazon S3 documentation\.

#### Step 6: Creating a local & AWS DMS task<a name="agents.Snowball.SBS.CreateLocalRemoteTask"></a>

Next, you create the task that is the end\-to\-end migration task\. The task includes two subtasks\. One subtask migrates data from the source database to the AWS Snowball Edge appliance\. The other subtask takes the data that the appliance loads into an Amazon S3 bucket and migrates it to the target database\.

**To create the end\-to\-end migration task**

1. Start AWS SCT, choose **View**, and then choose **Database Migration View \(Local & DMS\)**\.

1. In the left panel that displays the schema from your source database, choose a schema object to migrate\. Open the context \(right\-click\) menu for the object, and then choose **Create Local & DMS Task**\.

   You can't migrate individual tables using AWS DMS and Snowball Edge\.

1. Add your task information\.    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/agents.dw.html)

1. Choose **Create** to create the task\.

#### Step 7: Running and monitoring the AWS SCT task<a name="agents.Snowball.SBS.RunMonitorLocalTask"></a>

You can start the Local & DMS Task when all connections to endpoints are successful\. This means all connections for the Local task, which includes connections from the AWS DMS agent to the source database, the staging Amazon S3 bucket, and the AWS Snowball device, as well as the connections for the DMS task, which includes connections from the staging Amazon S3 bucket to the target database on AWS\.

You can monitor the AWS DMS agent logs by choosing **Show log**\. The log details include agent server \(**Agent log**\) and local running task \(**Task log**\) logs\. Because the endpoint connectivity is done by the server \(since the local task is not running and there are no task logs\), connection issues are listed under the **Agent log** tab\.

![\[Local task completed, waiting for the second task\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/snowball-tasklog.png)

## Data extraction task output<a name="agents.MovingData"></a>

After your migration tasks complete, your data is ready\. Use the following information to determine how to proceed based on the migration mode you chose and the location of your data\. 


****  

| Migration mode | Data location | 
| --- | --- | 
|  **Extract, upload and copy**  |  The data is already in your Amazon Redshift data warehouse\. You can verify that the data is there, and start using it\. For more information, see [Connecting to clusters from client tools and code](https://docs.aws.amazon.com/redshift/latest/mgmt/connecting-via-client-tools.html)\.   | 
|  **Extract and upload**  |  The extraction agents saved your data as files in your Amazon S3 bucket\. You can use the Amazon Redshift COPY command to load your data to Amazon Redshift\. For more information, see [Loading data from Amazon S3](https://docs.aws.amazon.com/redshift/latest/dg/t_Loading-data-from-S3.html) in the Amazon Redshift documentation\.  There are multiple folders in your Amazon S3 bucket, corresponding to the extraction tasks that you set up\. When you load your data to Amazon Redshift, specify the name of the manifest file created by each task\. The manifest file appears in the task folder in your Amazon S3 bucket as shown following\.  ![\[File list in Amazon S3 bucket\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/S3FileList.png)  | 
|  **Extract only**  |  The extraction agents saved your data as files in your working folder\. Manually copy your data to your Amazon S3 bucket, and then proceed with the instructions for **Extract and upload**\.  | 

## Using virtual partitioning with AWS Schema Conversion Tool<a name="agents.VirtualPartitioning"></a>

You can often best manage large non\-partitioned tables by creating subtasks that create virtual partitions of the table data using filtering rules\. In AWS SCT, you can create virtual partitions for your migrated data\. There are three partition types, which work with specific data types:
+ The RANGE partition type works with numeric and date and time data types\.
+ The LIST partition type works with numeric, character, and date and time data types\.
+ The DATE AUTO SPLIT partition type works with numeric, date, and time data types\.

AWS SCT validates the values you provide for creating a partition\. For example, if you attempt to partition a column with data type NUMERIC but you provide values of a different data type, AWS SCT throws an error\.

Also, if you are using AWS SCT to convert data from Netezza to Amazon Redshift, you can use native Netezza partitioning to manage migrating large tables\. For more information, see [Using native Netezza partitioning](#agents.VirtualPartitioning.Netezza)\. 

### Limits when creating virtual partitioning<a name="agents.VirtualPartitioning.Limits"></a>

These are limitations to creating a virtual partition:
+ You can only use virtual partitioning only for nonpartitioned tables\.
+ You can use virtual partitioning only in the data migration view\.
+ You can't use the option UNION ALL VIEW with virtual partitioning\.

### RANGE partition type<a name="agents.VirtualPartitioning.Range"></a>

The RANGE partition type partitions data based on a range of column values for numeric and date and time data types\. This partition type creates a `WHERE` clause, and you provide the range of values for each partition\. To specify a list of values for the partitioned column, use the **Values** box\. You can load value information by using a \.csv file\.

The RANGE partition type creates default partitions at both ends of the partition values\. These default partitions catch any data that is less than or greater than the specified partition values\.

For example, you can create multiple partitions based on a value range that you provide\. In the following example, the partitioning values for LO\_TAX are specified to create multiple partitions\.

```
Partition1: WHERE LO_TAX <= 10000.9
Partition2: WHERE LO_TAX > 10000.9 AND LO_TAX <= 15005.5
Partition3: WHERE LO_TAX > 15005.5 AND LO_TAX <= 25005.95
```

**To create a RANGE virtual partition**

1. Open AWS SCT\.

1. Choose **Data Migration view \(other\)** mode\.

1. Choose the table where you want to set up virtual partitioning\. Open the context \(right\-click\) menu for the table, and choose **Add virtual partitioning**\.

1. In the **Add virtual partitioning** dialog box, enter the information as follows\.  
****    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/agents.dw.html)

1. Choose **OK**\.

### LIST partition type<a name="agents.VirtualPartitioning.List"></a>

The LIST partition type partitions data based on column values for numeric, character, and date and time data types\. This partition type creates a `WHERE` clause, and you provide the values for each partition\. To specify a list of values for the partitioned column, use the **Values** box\. You can load value information by using a \.csv file\.

For example, you can create multiple partitions based on a value you provide\. In the following example, the partitioning values for LO\_ORDERKEY are specified to create multiple partitions\.

```
Partition1: WHERE LO_ORDERKEY = 1
Partition2: WHERE LO_ORDERKEY = 2
Partition3: WHERE LO_ORDERKEY = 3
…
PartitionN: WHERE LO_ORDERKEY = USER_VALUE_N
```

You can also create a default partition for values not included in the ones specified\.

You can use the LIST partition type to filter the source data if you want to exclude particular values from the migration\. For example, suppose that you want to omit rows with `LO_ORDERKEY = 4`\. In this case, don't include the value `4` in the list of partition values and make sure that **Include other values** isn't chosen\.

**To create a LIST virtual partition**

1. Open AWS SCT\.

1. Choose **Data Migration view \(other\)** mode\.

1. Choose the table where you want to set up virtual partitioning\. Open the context \(right\-click\) menu for the table, and choose **Add virtual partitioning**\.

1. In the **Add virtual partitioning** dialog box, enter the information as follows\.  
****    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/agents.dw.html)

1. Choose **OK**\.

### DATE AUTO SPLIT partition type<a name="agents.VirtualPartitioning.DateAutoSplit"></a>

The DATE AUTO SPLIT partition type is an automated way of generating RANGE partitions\. With DATA AUTO SPLIT, you tell AWS SCT the partitioning attribute, where to start and end, and the size of the range between the values\. Then AWS SCT calculates the partition values automatically\.

DATA AUTO SPLIT automates a lot of the work that is involved with creating range partitions\. The tradeoff between using this technique and range partitioning is how much control you need over the partition boundaries\. The automatic split process always creates equal size \(uniform\) ranges\. Range partitioning enables you to vary the size of each range as needed for your particular data distribution\. For example, you can use daily, weekly, biweekly, monthly, and so on\.

```
Partition1: WHERE LO_ORDERDATE >= ‘1954-10-10’ AND LO_ORDERDATE < ‘1954-10-24’
Partition2: WHERE LO_ORDERDATE >= ‘1954-10-24’ AND LO_ORDERDATE < ‘1954-11-06’
Partition3: WHERE LO_ORDERDATE >= ‘1954-11-06’ AND LO_ORDERDATE < ‘1954-11-20’
…
PartitionN: WHERE LO_ORDERDATE >= USER_VALUE_N AND LO_ORDERDATE <= ‘2017-08-13’
```

**To create a DATE AUTO SPLIT virtual partition**

1. Open AWS SCT\.

1. Choose **Data Migration view \(other\)** mode\.

1. Choose the table where you want to set up virtual partitioning\. Open the context \(right\-click\) menu for the table, and choose **Add virtual partitioning**\.

1. In the **Add virtual partitioning** dialog box, enter information as follows\.  
****    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/agents.dw.html)

1. Choose **OK**\.

### Using native Netezza partitioning<a name="agents.VirtualPartitioning.Netezza"></a>

To speed up data migration, you can enable extraction agents to use the physical distribution of tables on a Netezza server\. 

For example, after you create a project, you might collect statistics on a schema and analyze the size of the tables selected for migration\. For tables that exceed the size specified, AWS SCT triggers the native Netezza partitioning mechanism\.

**To use native Netezza partitioning**

1. Open AWS SCT, and choose **New project** for **File**\. The **New project** dialog box appears\.

1. Create a new project and connect to the source and target servers\.

1. Choose **View**, and then choose **Main view**\.

1. In the left panel that displays the schema from your source database, choose a schema\. Open the context \(right\-click\) menu for the object, and chose **Collect statistics**\.

1. Choose each table to be migrated, and analyze the size and number of rows\.

1. For **Current project settings**, choose the **Data migration** tab\. Choose **Use table partitioning … if table is more than**, and enter a table size limit in MB \(for example, 100\)\.

1. Register the required number of agents\. For more information, see [Registering extraction agents with the AWS Schema Conversion Tool](#agents.Using)\. 

1. Create a data extraction task for the selected tables\. For more information, see [Creating, running, and monitoring an AWS SCT data extraction task](#agents.Tasks)\. 

   Check if large tables are split into subtasks, and that each subtask matches the dataset that presents a part of the table located on one Netezza slice\. 

1. Start and monitor the migration process until migration of the selected tables has finished\. 

## Migrating LOBs to Amazon Redshift<a name="agents.LOBs"></a>

Amazon Redshift doesn't support storing large binary objects \(LOBs\)\. However, if you need to migrate one or more LOBs to Amazon Redshift, AWS SCT can perform the migration\. To do so, AWS SCT uses an Amazon S3 bucket to store the LOBs and writes the URL for the Amazon S3 bucket into the migrated data stored in Amazon Redshift\.

**To migrate LOBs to Amazon Redshift**

1. Open an AWS SCT project\.

1. Connect to the source and target databases\. Refresh metadata from the target database, and make sure that the converted tables exist there\.

1. For **Actions**, choose **Create local task**\.

1. For **Migration mode**, choose one of the following: 
   + **Extract and upload** to extract your data, and upload your data to Amazon S3\. 
   + **Extract, upload and copy** to extract your data, upload your data to Amazon S3, and copy it into your Amazon Redshift data warehouse\. 

1. Choose **Amazon S3 settings**\.

1. For **Amazon S3 bucket LOBs folder**, enter the name of the folder in an Amazon S3 bucket where you want the LOBs stored\.

   If you use AWS service profile, this field is optional\. AWS SCT can use the default settings from your profile\. To use another Amazon S3 bucket, enter the path here\.

1. Turn on the **Use proxy** option to use a proxy server to upload data to Amazon S3\. Then choose the data transfer protocol, enter the host name, port, user name, and password\.

1. For **Endpoint type**, choose **FIPS** to use the Federal Information Processing Standard \(FIPS\) endpoint\. Choose **VPCE** to use the virtual private cloud \(VPC\) endpoint\. Then for **VPC endpoint**, enter the Domain Name System \(DNS\) of your VPC endpoint\.

1. Turn on the **Keep files on Amazon S3 after copying to Amazon Redshift** option to keep extracted files on Amazon S3 after copying these files to Amazon Redshift\.

1. Choose **Create** to create the task\.

## Best practices and troubleshooting for data extraction agents<a name="agents.BestPractices"></a>

The following are some best practices and troubleshooting suggestions for using extraction agents\. 


****  

| Issue | Troubleshooting suggestions | 
| --- | --- | 
|  Performance is slow  |  To improve performance, we recommend the following:  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/agents.dw.html)  | 
|  Contention delays  |  Avoid having too many agents accessing your data warehouse at the same time\.   | 
|  An agent goes down temporarily  |  If an agent is down, the status of each of its tasks appears as failed in AWS SCT\. If you wait, in some cases the agent can recover\. In this case, the status of its tasks updates in AWS SCT\.   | 
|  An agent goes down permanently  |  If the computer running an agent goes down permanently, and that agent is running a task, you can substitute a new agent to continue the task\. You can substitute a new agent only if the working folder of the original agent was not on the same computer as the original agent\. To substitute a new agent, do the following:  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/agents.dw.html)  | 