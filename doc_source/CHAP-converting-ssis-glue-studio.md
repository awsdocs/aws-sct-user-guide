# Converting SSIS to AWS Glue Studio with AWS SCT<a name="CHAP-converting-ssis-glue-studio"></a>

You can use AWS SCT to convert Microsoft SQL Server Integration Services \(SSIS\) packages to AWS Glue Studio\.

An *SSIS package* includes the necessary components, such as the connection manager, tasks, control flow, data flow, parameters, event handlers, and variables, to run a specific extract, transform, and load \(ETL\) task\. AWS SCT converts SSIS packages to a format compatible with AWS Glue Studio\. After you migrate your source database to the AWS Cloud, you can run these converted AWS Glue Studio jobs to perform ETL tasks against the new database\.

To convert Microsoft SSIS packages to AWS Glue Studio, make sure that you use AWS SCT version 1\.0\.661 or later\.

## Adding SSIS packages to your AWS SCT project<a name="CHAP-converting-ssis-glue-studio-create"></a>

You can add multiple SSIS packages to a single AWS SCT project\.

**To add an SSIS package to your AWS SCT project**

1. Create a new project in AWS SCT or open an existing project\. For more information, see [Creating an AWS SCT project](CHAP_UserInterface.md#CHAP_UserInterface.Project)\. 

1. Choose **Add source** from the menu, and then choose **SQL Server Integration Services**\.

1. For **Connection name**, enter a name for your SSIS package\. AWS SCT displays this name in the tree in the left panel\.

1. For **SSIS packages folder**, enter the path to the folder with source SSIS packages\.

1. Choose **Add target** from the menu, and then choose **AWS Glue Studio**\.

   To connect to AWS Glue Studio, AWS SCT uses your AWS profile\. For more information, see [Storing AWS service profiles in the AWS SCT](CHAP_UserInterface.md#CHAP_UserInterface.Profiles)\.

1. Create a mapping rule, which includes your source SSIS package and your AWS Glue Studio target\. For more information, see [Creating mapping rules in AWS SCT](CHAP_Mapping.md)\.

1. Create AWS Glue Studio connections in the AWS Glue Studio console\. For more information, see [Creating connections for connectors](https://docs.aws.amazon.com/glue/latest/ug/connectors-chapter.html#creating-connections)\.  

1. Choose **Connection managers** in the left tree, open the context \(right\-click\) menu, and then choose **Configure connections**\.

   AWS SCT displays the **Configure connections** window\.

1. For each source SSIS connection, choose an AWS Glue Studio connection\.

## Converting SSIS packages to AWS Glue Studio with AWS SCT<a name="CHAP-converting-ssis-glue-studio-convert"></a>

Following, find how to convert SSIS packages to AWS Glue Studio using AWS SCT\.

**To convert an SSIS package to AWS Glue Studio**

1. Add your SSIS package to your AWS SCT project\. For more information, see [Adding SSIS packages to your AWS SCT project](#CHAP-converting-ssis-glue-studio-create)\.

1. In the left panel, expand the **ETL** and **SSIS** nodes\.

1. Choose **Packages**, open the context \(right\-click\) menu, and then choose **Convert package**\.

   AWS SCT converts your selected SSIS packages to JSON files\. These JSON objects represent a node in a directed acyclic graph \(DAG\)\. Find your converted files in the **Package DAGs** node in the right tree\.

1. Choose **Package DAGs**, open the context \(right\-click\) menu, and then choose **Save to Amazon S3**\.

   Now you can use these scripts to create jobs in the AWS Glue Studio\.

## Creating AWS Glue Studio jobs using the converted code<a name="CHAP-converting-ssis-glue-studio-jobs"></a>

After you convert your source SSIS packages, you can use the converted JSON files to create AWS Glue Studio jobs\.

**To create an AWS Glue Studio job**

1. Choose **Package DAGs** in the right tree, open the context \(right\-click\) menu, and then choose **Configure AWS Glue Studio job**\.

1. \(Optional\) Apply the extension pack that emulates SSIS functions in AWS Glue Studio\.

1. The **Configure AWS Glue Studio job** window opens\.

   Complete the **Basic job properties** section:
   + **Name** – Enter a name of your AWS Glue Studio job\.
   + **Script file name** – Enter a name of your job script\.
   + **Job parameters** – Add parameters and enter their values\.

   Choose **Next**\.

1. Complete the **Advanced job properties** section:
   + **IAM Role** – Choose the IAM role that is used for authorization to AWS Glue Studio and access data stores\.
   + **Script file S3 path** – Enter the Amazon S3 path to your converted script\.
   + **Temporary directory** – Enter the Amazon S3 path to a temporary directory for intermediate results\. AWS Glue Studio uses this directory to read or write to Amazon Redshift\.
   + AWS SCT automatically generates the path for Python libraries\. You can review this path in **Generated python library path**\. You can't edit this automatically generated path\. To use additional Python libraries, enter the path in **User python library path**\. 
   + **User python library path** – Enter the paths for additional user Python libraries\. Separate Amazon S3 paths with commas\.
   + **Dependent jars path** – Enter the paths for dependent `*.jar` files\. Separate Amazon S3 paths with commas\.
   + **Referenced files path** – Enter the paths for additional files, such as configuration files, that are required by your script\. Separate Amazon S3 paths with commas\.
   + **Worker type** – Choose `G.1X` or `G.2X`\.

     When you choose `G.1X` each worker maps to 1 DPU \(4 vCPU, 16 GB of memory, and 64 GB disk\)\.

     When you choose `G.2X` each worker maps to 2 DPU \(8 vCPU, 32 GB of memory, and 128 GB disk\)\.
   + **Requested number of workers** – Enter the number of workers that are allocated when the job runs\.
   + **Max concurrency** – Enter the maximum number of concurrent runs that are allowed for this job\. The default is 1\. AWS Glue returns an error when this threshold is reached\.
   + **Job timeout \(minutes\)** – Enter the timeout value on your ETL job as a safeguard against runaway jobs\. The default is 2,880 minutes \(48 hours\) for batch jobs\. If the job exceeds this limit, the job run state changes to `TIMEOUT`\.
   + **Delay notification threshold \(minutes\)** – Enter the threshold in minutes before AWS SCT sends a delay notification\.
   + **Number of retries** – Enter the number of times \(0–10\) that AWS Glue should automatically restart the job if it fails\. Jobs that reach the timeout limit aren't restarted\. The default is 0\.

   Choose **Finish**\.

   AWS SCT configures your selected AWS Glue Studio jobs\. 

1. Find your configured jobs under **ETL jobs** in the right tree\. Choose your configured job, open the context \(right\-click\) menu, and then choose **Create AWS Glue Studio job**\.

1. Choose **Apply status** and make sure that the **Status** value for your job is **Success**\.

1. Open the AWS Glue Studio console, choose **Refresh**, and choose your job\. Then choose **Run**\.

## Creating an assessment report for an SSIS package with AWS SCT<a name="CHAP-converting-ssis-glue-studio-assessment"></a>

The *ETL migration assessment report* provides information about converting your SSIS packages to a format compatible with AWS Glue Studio\. The assessment report includes action items for the components of your SSIS packages\. These action items show which components AWS SCT can't automatically convert\.  

**To create an ETL migration assessment report**

1. Expand the **SSIS** node under **ETL** in the left panel\.

1. Choose **Packages**, open the context \(right\-click\) menu, and then choose **Create report**\.

1. View the **Summary** tab\. Here, AWS SCT displays the executive summary information from the ETL migration assessment report\. It includes conversion results for all components of your SSIS packages\.

1. \(Optional\) Save a local copy of the ETL migration assessment report as either a PDF file or a comma\-separated values \(CSV\) file:
   + To save the ETL migration assessment report as a PDF file, choose **Save to PDF** at upper right\.

      The PDF file contains the executive summary, action items, and recommendations for scripts conversion\.
   + To save the ETL migration assessment report as a CSV file, choose **Save to CSV ** at upper right\.

     AWS SCT creates three CSV files\. These files contain action items, recommended actions, and an estimated complexity of manual effort required to convert the scripts\.

1. Choose the **Action items** tab\. This tab contains a list of items that require manual conversion to AWS Glue Studio\. When you choose an action item from the list, AWS SCT highlights the item from your source SSIS package that the action item applies to\.