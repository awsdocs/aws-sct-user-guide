# Migrating data from on\-premises databases<a name="agents.oltp"></a>

You can use an AWS SCT agent to extract data from your on\-premises relational database and migrate it to the AWS Cloud\. The agent extracts your data and uploads the data to either Amazon S3 or, for large\-scale migrations, an AWS Snowball Edge device\. You can then use AWS SCT to copy the data to the AWS Cloud\.

## Installing extraction agents<a name="agents.oltp.Installing"></a>

We recommend that you install multiple extraction agents on individual computers, separate from the computer that is running AWS SCT\. The AWS DMS agent is provided as part of [Installing, verifying, and updating AWS SCT](CHAP_Installing.md)\. 

**To install an AWS DMS agent**

1. Make sure that AWS SCT and the AWS DMS agent are installed on separate machines\. Make sure that the AWS DMS agent is installed on the same machine as the Open Database Connectivity \(ODBC\) drivers and, as needed, the Snowball Edge client\. 

1. In the AWS SCT installation directory, locate the RPM Package Manager \(RPM\) file called `aws-schema-conversion-tool-dms-agent-X.X.X-XX.x86_64.rpm`\.

   Copy it to the AWS DMS agent machine\. 

1. On the agent machine, run the following command to install the DMS agent\. To simplify permissions, run this command as the `root` user\.

   ```
   sudo rpm -i aws-schema-conversion-tool-dms-agent-X.X.X-XX.x86_64.rpm
   ```

   This command uses the default installation location of `/opt/amazon/aws-schema-conversion-tool-dms-agent`\. To install the DMS agent to a different location, use the following option\.

   ```
   sudo rpm --prefix installation_directory -i aws-schema-conversion-tool-dms-agent-X.X.X-XX.x86_64.rpm
   ```

1. Run the following command to verify that the DMS agent is running\.

   ```
   ps -ef | grep repctl
   ```

   The output of this command should show two processes running\.

1. Configure the DMS agent as follows:

   1. Run the `configure.sh` script\.

      ```
      sudo /opt/amazon/aws-schema-conversion-tool-dms-agent/bin/configure.sh
      ```

      A password prompt appears\.

   1. Enter a password\. Make sure that your password is 8–20 alphanumeric characters, with at least one digit and one uppercase character\. When prompted, enter the password again to confirm it\. You use the password later to register the DMS agent with AWS SCT, so keep it handy\.

      A port prompt appears\.

   1. Provide a port number\. Choose an unused port number for the DMS agent to listen on for AWS SCT connections\. The default is 3554\. You might have to configure your firewall to allow connectivity\.

The output is as follows, confirming that the service is started\. 

```
Starting service...
/opt/amazon/aws-schema-conversion-tool-dms-agent/bin/repctl:
    /opt/amazon/aws-schema-conversion-tool-dms-agent/lib/libcom_err.so.3: no version
    information available (required by
    /opt/amazon/aws-schema-conversion-tool-dms-agent/lib/libgssapi_krb5.so.2)
/opt/amazon/aws-schema-conversion-tool-dms-agent/bin/repctl:
    /opt/amazon/aws-schema-conversion-tool-dms-agent/lib/libcom_err.so.3: no version
    information available (required by
    /opt/amazon/aws-schema-conversion-tool-dms-agent/lib/libkrb5.so.3)
AWS Schema Conversion Tool DMS Agent was sent a stop signal
AWS Schema Conversion Tool DMS Agent is no longer running
[service command] Succeeded
/opt/amazon/aws-schema-conversion-tool-dms-agent/bin/repctl:
    /opt/amazon/aws-schema-conversion-tool-dms-agent/lib/libcom_err.so.3: no version
    information available (required by
    /opt/amazon/aws-schema-conversion-tool-dms-agent/lib/libgssapi_krb5.so.2)
/opt/amazon/aws-schema-conversion-tool-dms-agent/bin/repctl:
    /opt/amazon/aws-schema-conversion-tool-dms-agent/lib/libcom_err.so.3: no version
    information available (required by
    /opt/amazon/aws-schema-conversion-tool-dms-agent/lib/libkrb5.so.3)
AWS Schema Conversion Tool DMS Agent was started as PID 1608
```

We recommend that you install the [AWS Command Line Interface](https://aws.amazon.com/cli/) \(AWS CLI\)\. Using the AWS CLI, you can check the Snowball Edge to see the data files written to the device\. You use the AWS credentials retrieved from the Snowball Edge to access the Snowball Edge device\. For example, you might run the following command\.

```
aws s3 ls --profile SnowballEdge --endpoint https://192.0.2.0 :8080 bucket-name --recursive
```

This command produces the following output\.

```
2018-08-20 10:55:31 53074692 streams/load00000001000573E166ACF4C0/00000001.fcd.gz
2018-08-20 11:14:37 53059667 streams/load00000001000573E166ACF4C0/00000002.fcd.gz
2018-08-20 11:31:42 53079181 streams/load00000001000573E166ACF4C0/00000003.fcd.gz
```

**To start the DMS agent**
+ Run the following command in the `/opt/amazon/aws-schema-conversion-tool-dms-agent/bin` directory\.

  ```
  ./aws-schema-conversion-tool-dms-agent start
  ```

**To stop the DMS agent**
+ Run the following command in the `/opt/amazon/aws-schema-conversion-tool-dms-agent/bin` directory\.

  ```
  ./aws-schema-conversion-tool-dms-agent stop
  ```

## Registering extraction agents<a name="agents.oltp.Registering"></a>

You manage your extraction agents by using AWS SCT\. The extraction agents act as listeners\. When they receive instructions from AWS SCT, they extract data from your database\.

Use the following procedure to register extraction agents with your AWS SCT project\. 

**To register a AWS DMS agent**

1. Start AWS SCT, choose **View**, and then choose **Database Migration view \(standard DMS\)**\.

1. Choose the **Agent** tab, and then choose **Register**\.

1. Enter your information in the **New Agent Registration** dialog box\.    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/agents.oltp.html)

1. Choose **Register** to register the agent with your AWS SCT project\.

## Creating, running, and monitoring an AWS SCT data extraction task<a name="agents.oltp.Tasks"></a>

Use the following procedures to create, run, and monitor data extraction tasks in AWS SCT\.

**To assign tasks to agents and migrate data**

1. In AWS SCT, after you have converted your schema, choose one or more tables from the left panel of your project\. 

   You can choose all tables, but we recommend against that for performance reasons\. We recommend that you create multiple tasks for multiple tables based on the size of the tables in your data warehouse\. 

1. Open the context \(right\-click\) menu for each table, and then choose **Create task**\. The **Create Local task** dialog box opens\. 

1. For **Task name**, enter a name for the task\. 

1. For **Migration mode**, choose one of the following: 
   + **Extract only** – Extract your data, and save the data to your local working folders\. 
   + **Extract and upload** – Extract your data, and upload your data to Amazon S3\. 
   + **Extract, upload and copy** – Extract your data, upload your data to Amazon S3, and copy it into your Amazon Redshift data warehouse\. 

1. Choose **Extract LOBs** to extract large objects\. If you don't need to extract large objects, you can clear the check box\. Doing this reduces the amount of data that you extract\. 

1. \(Optional\) Choose **Enable task logging** to see detailed information about a task\. You can use the task log to debug problems\. 

   If you turn on task logging, choose the level of detail that you want to see\. The levels are the following, with each level including all messages from the previous level: 
   + `ERROR` – The smallest amount of detail\.
   + `WARNING`
   + `INFO`
   + `DEBUG`
   + `TRACE` – The largest amount of detail\.

1. Choose **Test task** to verify that you can connect to your working folder, Amazon S3 bucket, and Amazon Redshift data warehouse\. The verification depends on the migration mode that you chose\. 

1. Choose **Create** to create the task\.

1. Repeat the previous steps to create tasks for all the data that you want to migrate\. 

**To run a task**

1. In AWS SCT, for **View**, choose **Data Migration View \(standard DMS\)**\. The **Agents** tab appears\. 

1. Choose the **Tasks** tab\. Your tasks appear in the grid at the top\. You can see the status of a task in the top grid, and the status of its subtasks in the bottom grid\. 

1. Choose a task in the top grid and expand it\. Depending on the migration mode that you chose, you see the task divided into **Extract**, **Upload**, and **Copy**\. 

1. Choose **Start** for a task to start that task\. 

If you turned on logging when you set up your task, you can monitor the status of your task while it works\. The subtasks run in parallel\. The extract, upload, and copy also run in parallel\.

**To monitor a task**
+ View the log as follows: 

  1. Choose **Download log**\. 

     A message appears with the name of the folder that contains the log file\. Dismiss the message\. A link appears in the **Task details** tab\. 

  1. Choose the link to open the folder that contains the log file\. 

If you close AWS SCT, your agents and tasks continue to run\. You can reopen AWS SCT later to check the status of your tasks and view the task logs\. 

You can save data extraction tasks to your local disk and restore them to the same or another project by using export and import\.

To export a task, make sure that you have at least one extraction task created in a project\. Then choose the vertical ellipsis \( ![\[Image NOT FOUND\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/vertical-ellipsis.png)\) and choose **Export task** or **Export all tasks**\. 

When you export one extraction task, AWS SCT creates a separate `.xml` file for that task\. The `.xml` file stores that task's metadata information, such as task properties, description, and subtasks\. The `.xml` file doesn't contain information about processing of an extraction task\.

When you export all extraction tasks, AWS SCT creates a separate `.xml` file for each task\.

You can import a single extraction task or all of the tasks created in the project\. The following information is recreated when the task is imported:
+ Task progress
+ Subtask and stage states
+ Distribution of extracting agents by subtasks and stages
+ Task and subtask IDs
+ Task name

To import a task, choose the vertical ellipsis \( ![\[Image NOT FOUND\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/vertical-ellipsis.png)\) and choose **Import task**\. 