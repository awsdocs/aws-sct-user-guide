# Best practices for AWS SCT<a name="CHAP_BestPractices"></a>

Find information on best practices and options for using the AWS Schema Conversion Tool \(AWS SCT\)\. 

## Configuring additional memory<a name="CHAP_BestPractices.JVM"></a>

To convert large database schemas, such as a database with 3,500 stored procedures, you can configure the amount of memory available to the AWS Schema Conversion Tool\. 

**To modify the amount of memory that AWS SCT consumes**

1. On the **Settings** menu, choose **Global settings**, and then choose **JVM options**\.

1. Choose **Edit config file** and choose the text editor to open the configuration file\.

1. Edit the `JavaOptions` section to set the minimum and maximum memory available\. The following example sets the minimum to four GB and the maximum to 40 GB\.

   ```
   1. [JavaOptions]
   2. -Xmx40960M
   3. -Xms4096M
   ```

   We recommend that you set the minimum memory available to at least four GB\.

1. Save the configuration file, choose **OK**, and restart AWS SCT to apply changes\.

## Configuring the default project folder<a name="CHAP_BestPractices.Path"></a>

AWS SCT uses the project folder to store the project files, save assessment reports, and store converted code\. By default, AWS SCT stores all files in the application folder\. You can specify another folder as the default project folder\.

**To change the default project folder**

1. On the **Settings** menu, choose **Global settings**, and then choose **File path**\.

1. For **Default project file path**, enter the path to the default project folder\.

1. Choose **Apply**, and then choose **OK**\.

## Increasing the data migration speed<a name="CHAP_BestPractices.Extractors"></a>

To migrate large data sets, such as a set of tables with more than 1 TB of data, you might want to increase the migration speed\. When you use data extraction agents, the speed of data migrations depends on various factors\. These factors include the number of slices in your target Amazon Redshift cluster, size of a chunk file in your migration task, available RAM on the PC where you run your data extraction agents, and so on\.

To increase the data migration speed, we recommend running several test migration sessions with small data sets of your production data\. Also, we recommend that you run your data extraction agents on a PC with an SSD that has at least 500 GB of size\. During these test sessions, change different migration parameters monitor your disk utilization to find out the configuration that ensures the maximum data migration speed\. Then, use this configuration to migrate your whole data set\.

## Increasing logging information<a name="CHAP_BestPractices.Logging"></a>

You can increase the logging information produced by AWS SCT when converting your databases, scripts, and application SQL\. Although increasing logging information might slow conversion, the changes can help you provide robust information to AWS Support if errors arise\.

AWS SCT stores logs in your local environment\. You can view these log files and share them with AWS Support or AWS SCT developers for troubleshooting\.

**To change logging settings**

1. On the **Settings** menu, choose **Global settings**, and then choose **Logging**\. 

1. For **Log folder path**, enter the folder to store logs from the user interface\.

1. For **Console log folder path**, enter the folder to store logs of the AWS SCT command line interface \(CLI\)\.

1. For **Maximum log file size \(MB\)**, enter the size, in MB, of a single log file\. After your file reaches this limit, AWS SCT creates a new log file\.

1. For **Maximum number of log files**, enter the number of log files to store\. After the number of log files in the folder reaches this limit, AWS SCT deletes the oldest log file\.

1. For **Extractors log download path**, enter the folder to store data extraction agents logs\.

1. For **Cassandra extractor log path**, enter the folder to store Apache Cassandra data extraction agents logs\.

1. Select **Ask for a path before loading** to make sure that AWS SCT asks where to store logs every time you use data extraction agents\.

1. For **Debug mode**, choose **True**\. Use this option to log additional information when standard AWS SCT logs don't include any issues\.

1. Choose key application modules to increase the logging information\. You can increase the logging information for the following application modules:
   + **General**
   + **Loader**
   + **Parser**
   + **Printer**
   + **Resolver**
   + **Telemetry**
   + **Converter**
   + **Type mapping**
   + **User interface**
   + **Controller**
   + **Compare schema**
   + **Clone data center**
   + **Application analyzer**

   For each of the preceding application modules, choose one of the following logging levels:
   + **Trace** – Most detailed information\.
   + **Debug** – Detailed information on the flow through the system\.
   + **Info** – Runtime events, such as startup or shutdown\.
   + **Warning** – Use of deprecated APIs, poor use of API, other runtime situations that are undesirable or unexpected\.
   + **Error** – Runtime errors or unexpected conditions\.
   + **Critical** – Errors that lead to the application shutting down\.
   + **Mandatory** – The highest possible level of errors\.

   By default, after you turn on **Debug mode**, AWS SCT sets the **Info** logging level for all application modules\.

   For example, to help with key problem areas during conversion, set **Parser**, **Type mapping**, and **User interface** to **Trace**\.

If information becomes too verbose for the file system where logs are streaming, change to a location with sufficient space to capture logs\.

To transmit logs to AWS Support, go to the directory where the logs are stored, and compress all the files into a manageable single \.zip file\. Then upload the \.zip file with your support case\. When the initial analysis is completed and ongoing development resumes, return **Debug mode** to **false** to eliminate the verbose logging\. Then increase conversion speed\.

**Tip**  
To manage the log size and streamline reporting issues, remove the logs or move them to another location after a successful conversion\. Doing this task ensures that only the relevant errors and information are transmitted to AWS Support and keeps the log file system from filling\.