# Migrating Apache Hadoop to Amazon EMR with the AWS Schema Conversion Tool<a name="big-data-hadoop"></a>

To migrate Apache Hadoop clusters, make sure that you use AWS SCT version 1\.0\.670 or later\. Also, familiarize yourself with the command line interface \(CLI\) of AWS SCT\. For more information, see [AWS SCT CLI Reference](CHAP_Reference.md)\.

**Topics**
+ [Migration overview](#big-data-hadoop-migration-overview)
+ [Step 1: Connect to your Hadoop clusters](#big-data-hadoop-connect-to-databases)
+ [Step 2: Set up the mapping rules](#big-data-hadoop-mapping-rules)
+ [Step 3: Create an assessment report](#big-data-hadoop-assessment-report)
+ [Step 4: Migrate your Apache Hadoop cluster to Amazon EMR with AWS SCT](#big-data-hadoop-migrate)
+ [Running your CLI script](#big-data-hadoop-run-migration)
+ [Managing your big data migration project](#big-data-hadoop-manage-project)

## Migration overview<a name="big-data-hadoop-migration-overview"></a>

The following image shows the architecture diagram of the migration from Apache Hadoop to Amazon EMR\.

![\[The architecture diagram of the Hadoop migration\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/hadoop-migration-architecture-diagram.png)

AWS SCT migrates data and metadata from your source Hadoop cluster to an Amazon S3 bucket\. Next, AWS SCT uses your source Hive metadata to create database objects in the target Amazon EMR Hive service\. Optionally, you can configure Hive to use the AWS Glue Data Catalog as its metastore\. In this case, AWS SCT migrates your source Hive metadata to the AWS Glue Data Catalog\.

Then, you can use AWS SCT to migrate the data from an Amazon S3 bucket to your target Amazon EMR HDFS service\. Alternatively, you can leave the data in your Amazon S3 bucket and use it as a data repository for your Hadoop workloads\.

To start the Hapood migration, you create and run your AWS SCT CLI script\. This script includes the complete set of commands to run the migration\. You can download and edit a template of the Hadoop migration script\. For more information, see [Getting CLI scenarios](CHAP_Reference.md#CHAP_Reference.Scenario)\.

Make sure that your script includes the following steps so that you can run your migration from Apache Hadoop to Amazon S3 and Amazon EMR\.

## Step 1: Connect to your Hadoop clusters<a name="big-data-hadoop-connect-to-databases"></a>

To start the migration of your Apache Hadoop cluster, create a new AWS SCT project\. Next, connect to your source and target clusters\. Make sure that you create and provision your target AWS resources before you start the migration\.

In this step, you use the following AWS SCT CLI commands\.
+ `CreateProject` – to create a new AWS SCT project\.
+ `AddSourceCluster` – to connect to the source Hadoop cluster in your AWS SCT project\.
+ `AddSourceClusterHive` – to connect to the source Hive service in your project\.
+ `AddSourceClusterHDFS` – to connect to the source HDFS service in your project\.
+ `AddTargetCluster` – to connect to the target Amazon EMR cluster in your project\.
+ `AddTargetClusterS3` – to add the Amazon S3 bucket to your project\.
+ `AddTargetClusterHive` – to connect to the target Hive service in your project
+ `AddTargetClusterHDFS` – to connect to the target HDFS service in your project

For examples of using these AWS SCT CLI commands, see [Using Apache Hadoop as a source](CHAP_Source.Hadoop.md)\.

When you run the command that connects to a source or target cluster, AWS SCT tries to establish the connection to this cluster\. If the connection attempt fails, then AWS SCT stops running the commands from your CLI script and displays an error message\.

## Step 2: Set up the mapping rules<a name="big-data-hadoop-mapping-rules"></a>

After you connect to your source and target clusters, set up the mapping rules\. A mapping rule defines the migration target for a source cluster\. Make sure that you set up mapping rules for all source clusters that you added in your AWS SCT project\. For more information about mapping rules, see [Creating mapping rules in AWS SCT](CHAP_Mapping.md)\.

In this step, you use the `AddServerMapping` command\. This command uses two parameters, which define the source and target clusters\. You can use the `AddServerMapping` command with the explicit path to your database objects or with an object names\. For the first option, you include the type of the object and its name\. For the second option, you include only the object names\.
+ `sourceTreePath` – the explicit path to your source database objects\.

  `targetTreePath` – the explicit path to your target database objects\.
+ `sourceNamePath` – the path that includes only the names of your source objects\.

  `targetNamePath` – the path that includes only the names of your target objects\.

The following code example creates a mapping rule using explicit paths for the source `testdb` Hive database and the target EMR cluster\.

```
AddServerMapping
	-sourceTreePath: 'Clusters.HADOOP_SOURCE.HIVE_SOURCE.Databases.testdb'
	-targetTreePath: 'Clusters.HADOOP_TARGET.HIVE_TARGET'
/
```

You can use this example and the following examples in Windows\. To run the CLI commands in Linux, make sure that you updated the file paths appropriately for your operating system\.

The following code example creates a mapping rule using the paths that include only the object names\.

```
AddServerMapping
	-sourceNamePath: 'HADOOP_SOURCE.HIVE_SOURCE.testdb'
	-targetNamePath: 'HADOOP_TARGET.HIVE_TARGET'
/
```

You can choose Amazon EMR or Amazon S3 as a target for your source object\. For each source object, you can choose only one target in a single AWS SCT project\. To change the migration target for a source object, delete the existing mapping rule and then create a new mapping rule\. To delete a mapping rule, use the `DeleteServerMapping` command\. This command uses one of the two following parameters\.
+ `sourceTreePath` – the explicit path to your source database objects\.
+ `sourceNamePath` – the path that includes only the names of your source objects\.

For more information about the `AddServerMapping` and `DeleteServerMapping` commands, see the [AWS Schema Conversion Tool CLI Reference](https://s3.amazonaws.com/publicsctdownload/AWS+SCT+CLI+Reference.pdf)\.

## Step 3: Create an assessment report<a name="big-data-hadoop-assessment-report"></a>

Before you start the migration, we recommend to create an assessment report\. This report summarizes all of the migration tasks and details the action items that will emerge during the migration\. To make sure that your migration doesn't fail, view this report and address the action items before the migration\. For more information, see [Migration assessment reports](CHAP_AssessmentReport.md)\.

In this step, you use the `CreateMigrationReport` command\. This command uses two parameters\. The `treePath` parameter is mandatory, and the `forceMigrate` parameter is optional\.
+ `treePath` – the explicit path to your source database objects for which you save a copy of the assessment report\.
+ `forceMigrate` – when set to `true`, AWS SCT continues the migration even if your project includes an HDFS folder and Hive table that refer to the same object\. The default value is `false`\.

You can then save a copy of the assessment report as a PDF or comma\-separated value \(CSV\) files\. To do so, use the `SaveReportPDF` or `SaveReportCSV` command\.

The `SaveReportPDF` command saves a copy of your assessment report as a PDF file\. This command uses four parameters\. The `file` parameter is mandatory, other parameters are optional\.
+ `file` – the path to the PDF file and its name\.
+ `filter` – the name of the filter that you created before to define the scope of your source objects to migrate\.
+ `treePath` – the explicit path to your source database objects for which you save a copy of the assessment report\.
+ `namePath` – the path that includes only the names of your target objects for which you save a copy of the assessment report\.

The `SaveReportCSV` command saves your assessment report in three CSV files\. This command uses four parameters\. The `directory` parameter is mandatory, other parameters are optional\.
+ `directory` – the path to the folder where AWS SCT saves the CSV files\.
+ `filter` – the name of the filter that you created before to define the scope of your source objects to migrate\.
+ `treePath` – the explicit path to your source database objects for which you save a copy of the assessment report\.
+ `namePath` – the path that includes only the names of your target objects for which you save a copy of the assessment report\.

The following code example saves a copy of the assessment report in the `c:\sct\ar.pdf` file\.

```
SaveReportPDF
	-file:'c:\sct\ar.pdf'
/
```

The following code example saves a copy of the assessment report as CSV files in the `c:\sct` folder\.

```
SaveReportCSV
	-file:'c:\sct'
/
```

For more information about the `SaveReportPDF` and `SaveReportCSV` commands, see the [AWS Schema Conversion Tool CLI Reference](https://s3.amazonaws.com/publicsctdownload/AWS+SCT+CLI+Reference.pdf)\.

## Step 4: Migrate your Apache Hadoop cluster to Amazon EMR with AWS SCT<a name="big-data-hadoop-migrate"></a>

After you configure your AWS SCT project, start the migration of your on\-premises Apache Hadoop cluster to the AWS Cloud\.

In this step, you use the `Migrate`, `MigrationStatus`, and `ResumeMigration` commands\.

The `Migrate` command migrates your source objects to the target cluster\. This command uses four parameters\. Make sure that you specify the `filter` or `treePath` parameter\. Other parameters are optional\.
+ `filter` – the name of the filter that you created before to define the scope of your source objects to migrate\.
+ `treePath` – the explicit path to your source database objects for which you save a copy of the assessment report\.
+ `forceLoad` – when set to `true`, AWS SCT automatically loads database metadata trees during migration\. The default value is `false`\.
+ `forceMigrate` – when set to `true`, AWS SCT continues the migration even if your project includes an HDFS folder and Hive table that refer to the same object\. The default value is `false`\.

The `MigrationStatus` command returns the information about the migration progress\. To run this command, enter the name of your migration project for the `name` parameter\. You specified this name in the `CreateProject` command\.

The `ResumeMigration` command resumes the interrupted migration that you launched using the `Migrate` command\. The `ResumeMigration` command doesn't use parameters\. To resume the migration, you must connect to your source and target clusters\. For more information, see [Managing your migration project](#big-data-hadoop-manage-project)\.

The following code example migrates data from your source HDFS service to Amazon EMR\.

```
Migrate
	-treePath: 'Clusters.HADOOP_SOURCE.HDFS_SOURCE'
	-forceMigrate: 'true'
/
```

## Running your CLI script<a name="big-data-hadoop-run-migration"></a>

After you finish editing your AWS SCT CLI script, save it as a file with the `.scts` extension\. Now, you can run your script from the `app` folder of your AWS SCT installation path\. To do so, use the following command\.

```
RunSCTBatch.cmd --pathtoscts "C:\script_path\hadoop.scts"
```

In the preceding example, replace *script\_path* with the path to your file with the CLI script\. For more information about running CLI scripts in AWS SCT, see [Script mode](CHAP_Reference.md#CHAP_Reference.ScriptMode)\.

## Managing your big data migration project<a name="big-data-hadoop-manage-project"></a>

After you complete the migration, you can save and edit your AWS SCT project for the future use\.

To save your AWS SCT project, use the `SaveProject` command\. This command doesn't use parameters\.

The following code example saves your AWS SCT project\.

```
SaveProject
/
```

To open your AWS SCT project, use the `OpenProject` command\. This command uses one mandatory parameter\. For the `file` parameter, enter the path to your AWS SCT project file and its name\. You specified the project name in the `CreateProject` command\. Make sure that you add the `.scts` extension to the name of your project file to run the `OpenProject` command\.

The following code example opens the `hadoop_emr` project from the `c:\sct` folder\.

```
OpenProject
	-file: 'c:\sct\hadoop_emr.scts'
/
```

After you open your AWS SCT project, you don't need to add the source and target clusters because you have already added them to your project\. To start working with your source and target clusters, you must connect to them\. To do so, you use the `ConnectSourceCluster` and `ConnectTargetCluster` commands\. These commands use the same parameters as the `AddSourceCluster` and `AddTargetCluster` commands\. You can edit your CLI script and replace the name of these commands leaving the list of parameters without changes\.

The following code example connects to the source Hadoop cluster\.

```
ConnectSourceCluster
    -name: 'HADOOP_SOURCE'
    -vendor: 'HADOOP'
    -host: 'hadoop_address'
    -port: '22'
    -user: 'hadoop_user'
    -password: 'hadoop_password'
    -useSSL: 'true'
    -privateKeyPath: 'c:\path\name.pem'
    -passPhrase: 'hadoop_passphrase'
/
```

The following code example connects to the target Amazon EMR cluster\.

```
ConnectTargetCluster
	-name: 'HADOOP_TARGET'
	-vendor: 'AMAZON_EMR'
	-host: 'ec2-44-44-55-66.eu-west-1.EXAMPLE.amazonaws.com'
	-port: '22'
	-user: 'emr_user'
	-password: 'emr_password'
	-useSSL: 'true'
	-privateKeyPath: 'c:\path\name.pem'
	-passPhrase: '1234567890abcdef0!'
	-s3Name: 'S3_TARGET'
	-accessKey: 'AKIAIOSFODNN7EXAMPLE'
	-secretKey: 'wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY'
	-region: 'eu-west-1'
	-s3Path: 'doc-example-bucket/example-folder'
/
```

In the preceding example, replace *hadoop\_address* with the IP address of your Hadoop cluster\. If needed, configure the value of the port variable\. Next, replace *hadoop\_user* and *hadoop\_password* with the name of your Hadoop user and the password for this user\. For *path\\name*, enter the name and path to the PEM file for your source Hadoop cluster\. For more information about adding your source and target clusters, see [Using Apache Hadoop as a source for AWS SCT](CHAP_Source.Hadoop.md)\.

After you connect to your source and target Hadoop clusters, you must connect to your Hive and HDFS services, as well as to your Amazon S3 bucket\. To do so, you use the `ConnectSourceClusterHive`, `ConnectSourceClusterHdfs`, `ConnectTargetClusterHive`, `ConnectTargetClusterHdfs`, and `ConnectTargetClusterS3` commands\. These commands use the same parameters as the commands that you used to add Hive and HDFS services, and the Amazon S3 bucket to your project\. Edit the CLI script to replace the `Add` prefix with `Connect` in the command names\.