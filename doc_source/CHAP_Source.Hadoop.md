# Using Apache Hadoop as a source for AWS SCT<a name="CHAP_Source.Hadoop"></a>

You can use the AWS SCT command line interface \(CLI\) to migrate from Apache Hadoop to Amazon EMR\. AWS SCT uses your Amazon S3 bucket as a temporary storage for your data during migration\.

AWS SCT supports as a source Apache Hadoop version 2\.2\.0 and later\. Also, AWS SCT supports Apache Hive version 0\.13\.0 and later\.

AWS SCT supports as a target Amazon EMR version 6\.3\.0 and later\. Also, AWS SCT supports as a target Apache Hadoop version 2\.6\.0 and later, and Apache Hive version 0\.13\.0 and later\.

**Topics**
+ [Prerequisites for using Apache Hadoop as a source](#CHAP_Source.Hadoop.Prerequisites)
+ [Permissions for using Hive as a source](#CHAP_Source.Hadoop.Permissions)
+ [Permissions for using HDFS as a source](#CHAP_Source.Hadoop.PermissionsHDFS)
+ [Permissions for using HDFS as a target](#CHAP_Source.Hadoop.PermissionsHDFSTarget)
+ [Connecting to Apache Hadoop as a source](#CHAP_Source.Hadoop.Connecting)
+ [Connecting to your source Hive and HDFS services](#CHAP_Source.Hadoop.Hive)
+ [Connecting to Amazon EMR as a target](#CHAP_Source.Hadoop.Target)

## Prerequisites for using Apache Hadoop as a source<a name="CHAP_Source.Hadoop.Prerequisites"></a>

The following prerequisites are required to connect to Apache Hadoop with the AWS SCT CLI\.
+ Create an Amazon S3 bucket to store data during the migration\. You can then copy data to Amazon EMR HDFS or use Amazon S3 as a data repository for your Hadoop workloads\. For more information, see [Creating a bucket](https://docs.aws.amazon.com/AmazonS3/latest/userguide/create-bucket-overview.html) in the *Amazon S3 User Guide*\.
+ Create an AWS Identity and Access Management \(IAM\) role with the `AmazonS3FullAccess` policy\. AWS SCT uses this IAM role to access your Amazon S3 bucket\.
+ Take a note of your AWS secret key and AWS secret access key\. For more information about AWS access keys, see [Managing access keys](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html) in the *IAM User Guide*\.
+ Create and configure a target Amazon EMR cluster\. For more information, see [Getting started with Amazon EMR](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-gs.html) in the *Amazon EMR Management Guide*\.
+ Install the `distcp` utility on your source Apache Hadoop cluster\. Also, install the `s3-dist-cp` utility on your target Amazon EMR cluster\. Make sure that your database users have permissions to run these utilities\.
+ Configure the `core-site.xml` file in your source Hadoop cluster to use the s3a protocol\. To do so, set the `fs.s3a.aws.credentials.provider` parameter to one of the following values\.
  + `org.apache.hadoop.fs.s3a.TemporaryAWSCredentialsProvider`
  + `org.apache.hadoop.fs.s3a.SimpleAWSCredentialsProvider`
  + `org.apache.hadoop.fs.s3a.AnonymousAWSCredentialsProvider`
  + `org.apache.hadoop.fs.s3a.auth.AssumedRoleCredentialProvider`

  You can add the following code example into the `core-site.xml` file\.

  ```
  <property>
    <name>fs.s3a.aws.credentials.provider</name>
    <value>org.apache.hadoop.fs.s3a.SimpleAWSCredentialsProvider</value>
  </property>
  ```

  The preceding example shows one of the four options from the preceding list of options\. If you don't set the `fs.s3a.aws.credentials.provider` parameter in the `core-site.xml` file, AWS SCT chooses the provider automatically\.

## Permissions for using Hive as a source<a name="CHAP_Source.Hadoop.Permissions"></a>

The permissions required for a Hive source user are as follows:
+ `READ` access to the source data folders and to the source Amazon S3 bucket
+ `READ+WRITE` access to the intermediate and target Amazon S3 buckets

To increase the migration speed, we recommend that you run compaction for ACID\-transactional source tabes\.

The permissions required for an Amazon EMR Hive target user are as follows:
+ `READ` access to the target Amazon S3 bucket
+ `READ+WRITE` access to the intermediate Amazon S3 bucket
+ `READ+WRITE` access to the target HDFS folders

## Permissions for using HDFS as a source<a name="CHAP_Source.Hadoop.PermissionsHDFS"></a>

The permissions required for HDFS as a source are as follows:
+ `EXECUTE` for the NameNode
+ `EXECUTE+READ` for all source folders and files that you include in the migration project
+ `READ+WRITE` for the `tmp` directory in the NameNode to run Spark jobs and store files before the migration to Amazon S3

In HDFS, all operations require traversal access\. Traversal access demands the `EXECUTE` permission on all existing components of the path, except for the final path component\. For example, for any operation accessing `/foo/bar/baz`, your user must have `EXECUTE` permission on `/`, `/foo`, and `/foo/bar`\.

The following code example demonstrates how to grant `EXECUTE+READ` permissions for your source folders and files, and `READ+WRITE` permissions for the `tmp` directory\.

```
hadoop fs –chmod –R 744 /user/hdfs-data
hadoop fs –chmod –R 766 /tmp
```

## Permissions for using HDFS as a target<a name="CHAP_Source.Hadoop.PermissionsHDFSTarget"></a>

The permissions required for Amazon EMR HDFS as a target are as follows:
+ `EXECUTE` for the NameNode of the target Amazon EMR cluster
+ `READ+WRITE` for the target HDFS folders where you will store data after migration

## Connecting to Apache Hadoop as a source<a name="CHAP_Source.Hadoop.Connecting"></a>

You can use Apache Hadoop as a source in AWS SCT version 1\.0\.670 or higher\. You can migrate Hadoop clusters to Amazon EMR only in the AWS SCT command line interface \(CLI\)\. Before you start, familiarize yourself with the command line interface of AWS SCT\. For more information, see [AWS SCT CLI Reference](CHAP_Reference.md)\.

**To connect to Apache Hadoop in the AWS SCT CLI**

1. Create a new AWS SCT CLI script or edit an existing scenario template\. For example, you can download and edit the `HadoopMigrationTemplate.scts` template\. For more information, see [Getting CLI scenarios](CHAP_Reference.md#CHAP_Reference.Scenario)\.

1. Configure the AWS SCT application settings such as the driver location and log folder\.

   Download the required JDBC driver and specify the location where you store the file\. For more information, see [Downloading the required database drivers](CHAP_Installing.md#CHAP_Installing.JDBCDrivers)\.

   The following code example shows you how to add the path to the Apache Hive driver\. After you run this code example, AWS SCT stores log files in the `c:\sct` folder\.

   ```
   SetGlobalSettings
       -save: 'true'
       -settings: '{
           "hive_driver_file": "c:\\sct\\HiveJDBC42.jar",
           "log_folder": "c:\\sct",
           "console_log_folder": "c:\\sct"
       }'
   /
   ```

   You can use this example and the following examples in Windows\.

1. Create a new AWS SCT project\.

   The following code example creates the `hadoop_emr` project in the `c:\sct` folder\.

   ```
   CreateProject
       -name: 'hadoop_emr'
       -directory: 'c:\sct'
   /
   ```

1. Add your source Hadoop cluster to the project\.

   Use the `AddSourceCluster` command to connect to the source Hadoop cluster\. Make sure that you provide values for the following mandatory parameters: `name`, `host`, `port`, and `user`\. Other parameters are optional\.

   The following code example adds the source Hadoop cluster\. This example sets `HADOOP_SOURCE` as a name of the source cluster\. Use this object name to add Hive and HDFS services to the project and create mapping rules\.

   ```
   AddSourceCluster
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

   In the preceding example, replace *hadoop\_address* with the IP address of your Hadoop cluster\. If needed, configure the value of the port option\. Next, replace *hadoop\_user* and *hadoop\_password* with the name of your Hadoop user and the password for this user\. For *path\\name*, enter the name and path to the PEM file for your source Hadoop cluster\.

1. Save your CLI script\. Next, add the connection information for your Hive and HDFS services\.

## Connecting to your source Hive and HDFS services<a name="CHAP_Source.Hadoop.Hive"></a>

You can connect to your source Hive and HDFS services with the AWS SCT CLI\. To connect to Apache Hive, use the Hive JDBC driver version 2\.3\.4 or higher\. For more information, see [Downloading the required database drivers](CHAP_Installing.md#CHAP_Installing.JDBCDrivers)\.

AWS SCT connects to Apache Hive with the `hadoop` cluster user\. To do so, use the `AddSourceClusterHive` and `AddSourceClusterHDFS` commands\. You can use one of the following approaches\.
+ Create a new SSH tunnel\.

  For `createTunnel`, enter **true**\. For `host`, enter the internal IP address of your source Hive or HDFS service\. For `port`, enter the service port of your Hive or HDFS service\.

  Next, enter your Hive or HDFS credentials for `user` and `password`\. For more information about SSH tunnels, see [Set up an SSH tunnel to the primary node using local port forwarding](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-ssh-tunnel-local.html) in the Amazon EMR Management Guide\.
+ Use an existing SSH tunnel\.

  For `host`, enter **localhost**\. For `port`, enter the local port from the SSH tunnel parameters\.
+ Connect to your Hive and HDFS services directly\.

  For `host`, enter the IP address or hostname of your source Hive or HDFS service\. For `port`, enter the service port of your Hive or HDFS service\. Next, enter your Hive or HDFS credentials for `user` and `password`\.

**To connect to Hive and HDFS in the AWS SCT CLI**

1. Open your CLI script which includes the connection information for your source Hadoop cluster\. Make sure that you use the name of the Hadoop cluster that you defined in the previous step\.

1. Add your source Hive service to the project\.

   Use the `AddSourceClusterHive` command to connect the source Hive service\. Make sure that you provide values for the following mandatory parameters: `user`, `password`, `cluster`, `name`, and `port`\. Other parameters are optional\.

   The following code example creates a tunnel for AWS SCT to work with your Hive service\. This source Hive service runs on the same PC as AWS SCT\. This example uses the `HADOOP_SOURCE` source cluster from the previous example\.

   ```
   AddSourceClusterHive
       -cluster: 'HADOOP_SOURCE'
       -name: 'HIVE_SOURCE'
       -host: 'localhost'
       -port: '10005'
       -user: 'hive_user'
       -password: 'hive_password'
       -createTunnel: 'true'
       -localPort: '10005'
       -remoteHost: 'hive_remote_address'
       -remotePort: 'hive_port'
   /
   ```

   The following code example connects to your Hive service without a tunnel\.

   ```
   AddSourceClusterHive
       -cluster: 'HADOOP_SOURCE'
       -name: 'HIVE_SOURCE'
       -host: 'hive_address'
       -port: 'hive_port'
       -user: 'hive_user'
       -password: 'hive_password'
   /
   ```

   In the preceding examples, replace *hive\_user* and *hive\_password* with the name of your Hive user and the password for this user\.

   Next, replace *hive\_address* and *hive\_port* with the NameNode IP address and port of your source Hadoop cluster\.

   For *hive\_remote\_address*, you might use the default value `127.0.0.1` or the NameNode IP address of your source Hive service\.

1. Add your source HDFS service to the project\.

   Use the `AddSourceClusterHDFS` command to connect the source HDFS service\. Make sure that you provide values for the following mandatory parameters: `user`, `password`, `cluster`, `name`, and `port`\. Other parameters are optional\.

   Make sure that your user has the required permissions to migrate data from your source HDFS service\. For more information, see [Permissions for using Hive as a source](#CHAP_Source.Hadoop.Permissions)\.

   The following code example creates a tunnel for AWS SCT to work with your Apache HDFS service\. This example uses the `HADOOP_SOURCE` source cluster that you created before\.

   ```
   AddSourceClusterHDFS
       -cluster: 'HADOOP_SOURCE'
       -name: 'HDFS_SOURCE'
       -host: 'localhost'
       -port: '9005'
       -user: 'hdfs_user'
       -password: 'hdfs_password'
       -createTunnel: 'true'
       -localPort: '9005'
       -remoteHost: 'hdfs_remote_address'
       -remotePort: 'hdfs_port'
   /
   ```

   The following code connects to your Apache HDFS service without a tunnel\.

   ```
   AddSourceClusterHDFS
       -cluster: 'HADOOP_SOURCE'
       -name: 'HDFS_SOURCE'
       -host: 'hdfs_address'
       -port: 'hdfs_port'
       -user: 'hdfs_user'
       -password: 'hdfs_password'
   /
   ```

   In the preceding examples, replace *hdfs\_user* and *hdfs\_password* with the name of your HDFS user and the password for this user\.

   Next, replace *hdfs\_address* and *hdfs\_port* with the NameNode IP address and port of your source Hadoop cluster\.

   For *hdfs\_remote\_address*, you might use the default value `127.0.0.1` or the NameNode IP address of your source Hive service\.

1. Save your CLI script\. Next, add the connection information for your target Amazon EMR cluster, and the migration commands\.

## Connecting to Amazon EMR as a target<a name="CHAP_Source.Hadoop.Target"></a>

You can connect to your target Amazon EMR cluster with the AWS SCT CLI\. To do so, you authorize inbound traffic and use SSH\. In this case, AWS SCT has all required permissions to work with your Amazon EMR cluster\. For more information, see [Before you connect](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-connect-ssh-prereqs.html) and [Connect to the primary node using SSH](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-connect-master-node-ssh.html) in the Amazon EMR Management Guide\.

AWS SCT connects to Amazon EMR Hive with the `hadoop` cluster user\. To connect to Amazon EMR Hive, use the Hive JDBC driver version 2\.6\.2\.1002 or higher\. For more information, see [Downloading the required database drivers](CHAP_Installing.md#CHAP_Installing.JDBCDrivers)\.

**To connect to Amazon EMR in the AWS SCT CLI**

1. Open your CLI script which includes the connection information for your source Hadoop cluster\. Add the target Amazon EMR credentials into this file\.

1. Add your target Amazon EMR cluster to the project\.

   The following code example adds the target Amazon EMR cluster\. This example sets `HADOOP_TARGET` as a name of the target cluster\. Use this object name to add your Hive and HDFS services and an Amazon S3, bucket folder to the project and create mapping rules\.

   ```
   AddTargetCluster
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

   In the preceding example, enter your AWS resource names and Amazon EMR connection information\. This includes the IP address of your Amazon EMR cluster, AWS access key, AWS secret access key, and Amazon S3 bucket\. If needed, configure the value of the port variable\. Next, replace *emr\_user* and *emr\_password* with the name of your Amazon EMR user and the password for this user\. For *path\\name*, enter the name and path to the PEM file for your target Amazon EMR cluster\. For more information, see [Download PEM File for EMR Cluster Access](https://docs.aws.amazon.com/whitepapers/latest/teaching-big-data-skills-with-amazon-emr/download-pem-file-for-emr-cluster-access.html)\.

1. Add your target Amazon S3 bucket to the project\.

   The following code example adds the target Amazon S3 bucket\. This example uses the `HADOOP_TARGET` cluster that you created before\.

   ```
   AddTargetClusterS3
   	-cluster: 'HADOOP_TARGET'
   	-Name: 'S3_TARGET'
   	-accessKey: 'AKIAIOSFODNN7EXAMPLE'
   	-secretKey: 'wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY'
   	-region: 'eu-west-1'
   	-s3Path: 'doc-example-bucket/example-folder'
   /
   ```

   In the preceding example, enter your AWS access key, AWS secret access key, and Amazon S3 bucket\.

1. Add your target Hive service to the project\.

   The following code example creates a tunnel for AWS SCT to work with your target Hive service\. This example uses the `HADOOP_TARGET` target cluster that you created before\.

   ```
   AddTargetClusterHive
       -cluster: 'HADOOP_TARGET'
       -name: 'HIVE_TARGET'
       -host: 'localhost'
       -port: '10006'
       -user: 'hive_user'
       -password: 'hive_password'
       -createTunnel: 'true'
       -localPort: '10006'
       -remoteHost: 'hive_address'
       -remotePort: 'hive_port'
   /
   ```

   In the preceding example, replace *hive\_user* and *hive\_password* with the name of your Hive user and the password for this user\.

   Next, replace *hive\_address* with the default value `127.0.0.1` or with the NameNode IP address of your target Hive service\. Next, replace *hive\_port* with the port of your target Hive service\.

1. Add your target HDFS service to the project\.

   The following code example creates a tunnel for AWS SCT to work with your Apache HDFS service\. This example uses the `HADOOP_TARGET` target cluster that you created before\.

   ```
   AddTargetClusterHDFS
       -cluster: 'HADOOP_TARGET'
       -name: 'HDFS_TARGET'
       -host: 'localhost'
       -port: '8025'
       -user: 'hdfs_user'
       -password: 'hdfs_password'
       -createTunnel: 'true'
       -localPort: '8025'
       -remoteHost: 'hdfs_address'
       -remotePort: 'hdfs_port'
   /
   ```

   In the preceding example, replace *hdfs\_user* and *hdfs\_password* with the name of your HDFS user and the password for this user\.

   Next, replace *hdfs\_address* and *hdfs\_port* with the private IP address and port of the NameNode of your target HDFS service\.

1. Save your CLI script\. Next, add mapping rules and migration commands\. For more information, see [Migrating Apache Hadoop to Amazon EMR](big-data-hadoop.md)\.