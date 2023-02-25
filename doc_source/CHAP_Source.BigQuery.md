# Using BigQuery as a source for AWS SCT<a name="CHAP_Source.BigQuery"></a>

You can use AWS SCT to convert schemas, code objects, and application code from BigQuery to Amazon Redshift\. 

## Privileges for BigQuery as a source<a name="CHAP_Source.BigQuery.Permissions"></a>

To use a BigQuery data warehouse as a source in AWS SCT, create a service account\. In Google Cloud, applications use service accounts to make authorized API calls\. Service accounts differ from user accounts\. For more information, see [Service accounts](https://cloud.google.com/iam/docs/service-accounts) in the Google Cloud Identity and Access Management documentation\.

Make sure that you grant the following roles to your service account:
+ `BigQuery Admin`
+ `Storage Admin`

The `BigQuery Admin` role provides permissions to manage all resources within the project\. AWS SCT uses this role to load your BigQuery metadata in the migration project\.

The `Storage Admin` role grants full control of data objects and buckets\. You can find this role under `Cloud Storage`\. AWS SCT uses this role to extract your data from BigQuery and then load it into Amazon Redshift\.

**To create a service account key file**

1. Sign in to the Google Cloud management console at [https://console\.cloud\.google\.com/](https://console.cloud.google.com/)\.

1. On the [BigQuery API](https://console.cloud.google.com/apis/library/bigquery.googleapis.com) page, choose **Enable**\. Skip this step if you see **API Enabled**\.

1. On the [Service accounts](https://console.cloud.google.com/iam-admin/serviceaccounts) page, choose your project, and then choose **Create service account**\.

1. On the **Service account details** page, enter a descriptive value for **Service account name**\. Choose **Create and continue**\. The **Grant this service account access to the project** page opens\. 

1. For **Select a role**, choose **BigQuery**, and then choose **BigQuery Admin**\. 

1. Choose **Add another role**\. For **Select a role**, choose **Cloud Storage**, and then choose **Storage Admin**\. 

1. Choose **Continue**, and then choose **Done**\. 

1. On the [Service accounts](https://console.cloud.google.com/iam-admin/serviceaccounts) page, choose the service account that you created\.

1. Choose **Keys**, and then choose **Create new key** for **Add key**\.

1. Choose **JSON**, and then choose **Create**\. Choose the folder to save your private key or select the default folder for downloads in your browser\.

To extract data from a BigQuery data warehouse, AWS SCT uses the Google Cloud Storage bucket folder\. Create this bucket before you start data migration\. Enter the path to your Google Cloud Storage bucket folder in the **Create Local task** dialog box\. For more information, see [Creating, running, and monitoring an AWS SCT task](agents.dw.md#agents.Tasks)\.

## Connecting to BigQuery as a source<a name="CHAP_Source.BigQuery.Connecting"></a>

Use the following procedure to connect to your source BigQuery project with the AWS Schema Conversion Tool\.

**To connect to a BigQuery source data warehouse**

1. In the AWS Schema Conversion Tool, choose **Add source**\.

1. Choose **BigQuery**, then choose **Next**\.

   The **Add source** dialog box appears\.

1. For **Connection name**, enter a name for your BigQuery project\. AWS SCT displays this name in the tree in the left panel\.

1. For **Key path**, enter the path to the service account key file\. For more information about creating this file, see [Privileges for BigQuery as a source](#CHAP_Source.BigQuery.Permissions)\. 

1. Choose **Test Connection** to verify that AWS SCT can connect to your source BigQuery project\. 

1. Choose **Connect** to connect to your source BigQuery project\.

## Limitations on using BigQuery as a source for AWS SCT<a name="CHAP_Source.BigQuery.Limitations"></a>

The following limitations apply when using BigQuery as a source for AWS SCT:
+ AWS SCT doesn't support the conversion of subqueries in analytic functions\.
+ You can't use AWS SCT to convert BigQuery `SELECT AS STRUCT` and `SELECT AS VALUE` statements\.
+ AWS SCT doesn't support the conversion of the following types of functions:
  + Approximate aggregate
  + Bit
  + Debugging
  + Federated query
  + Geography
  + Hash
  + Mathematical
  + Net
  + Statistical aggregate
  + UUID
+ AWS SCT provides limited support for the conversion of string functions\.  
+ AWS SCT doesn't support the conversion of `UNNEST` operators\.
+ You can't convert correlated join operations in AWS SCT\.
+ AWS SCT doesn't support the conversion of `QUALIFY`, `WINDOW`, `LIMIT`, and `OFFSET` clauses\.
+ You can't use AWS SCT to convert recursive common table expressions\.
+ AWS SCT doesn't support the conversion of `INSERT` statements with subqueries inside `VALUES` clauses\.
+ AWS SCT doesn't support the conversion of `UPDATE` statements for nested fields and repeated records\.
+ You can't use AWS SCT to convert `STRUCT` and `ARRAY` data types\.

## BigQuery to Amazon Redshift conversion settings<a name="CHAP_Source.BigQuery.ConversionSettings"></a>

To edit BigQuery to Amazon Redshift conversion settings, choose **Settings** in AWS SCT, and then choose **Conversion settings**\. From the upper list, choose **Google BigQuery**, and then choose **Google BigQuery – Amazon Redshift**\. AWS SCT displays all available settings for BigQuery to Amazon Redshift conversion\.

BigQuery to Amazon Redshift conversion settings in AWS SCT include options for the following:
+ To limit the number of comments with action items in the converted code\.

  For **How detailed should comments be in the converted SQL**, choose the severity of action items\. AWS SCT adds comments in the converted code for action items of the selected severity and higher\.

  For example, to minimize the number of comments in your converted code, choose **Errors only**\. To include comments for all action items in your converted code, choose **All messages**\.
+ To set the maximum number of tables that AWS SCT can apply to your target Amazon Redshift cluster\.

  For **Maximum number of tables for target Amazon Redshift cluster**, choose the number of tables that AWS SCT can apply to your Amazon Redshift cluster\.

  Amazon Redshift has quotas that limit the use tables for different cluster node types\. If you choose **Auto**, AWS SCT determines the number of tables to apply to your target Amazon Redshift cluster depending on the node type\. Optionally, choose the value manually\. For more information, see [Quotas and limits in Amazon Redshift](https://docs.aws.amazon.com/redshift/latest/mgmt/amazon-redshift-limits.html) in the *Amazon Redshift Cluster Management Guide*\.

  AWS SCT converts all your source tables, even if this is more than your Amazon Redshift cluster can store\. AWS SCT stores the converted code in your project and doesn't apply it to the target database\. If you reach the Amazon Redshift cluster quota for the tables when you apply the converted code, then AWS SCT displays a warning message\. Also, AWS SCT applies tables to your target Amazon Redshift cluster until the number of tables reaches the limit\.
+ To apply compression to Amazon Redshift table columns\. To do so, select **Use compression encoding**\.

  AWS SCT assigns compression encoding to columns automatically using the default Amazon Redshift algorithm\. For more information, see [Compression encodings](https://docs.aws.amazon.com/redshift/latest/dg/c_Compression_encodings.html) in the *Amazon Redshift Database Developer Guide*\.

  By default, Amazon Redshift doesn't apply compression to columns that are defined as sort and distribution keys\. You can change this behavior and apply compression to these columns\. To do so, select **Use compression encoding for KEY columns**\. You can select this option only when you select the **Use compression encoding** option\.

## BigQuery to Amazon Redshift conversion optimization settings<a name="CHAP_Source.BigQuery.ConversionOptimizationSettings"></a>

To edit BigQuery to Amazon Redshift conversion optimization settings, choose **Settings** in AWS SCT, and then choose **Conversion settings**\. From the upper list, choose **Google BigQuery**, and then choose **Google BigQuery – Amazon Redshift**\. In the left pane, choose **Optimization strategies**\. AWS SCT displays conversion optimization settings for BigQuery to Amazon Redshift conversion\.

BigQuery to Amazon Redshift conversion optimization settings in AWS SCT include options for the following:
+ To work with automatic table optimization\. To do so, select **Use Amazon Redshift automatic table tuning**\.

  Automatic table optimization is a self\-tuning process in Amazon Redshift that automatically optimizes the design of tables\. For more information, see [Working with automatic table optimization](https://docs.aws.amazon.com/redshift/latest/dg/t_Creating_tables.html) in the *Amazon Redshift Database Developer Guide*\.

  To rely only on the automatic table optimization, choose **None** for **Initial key selection strategy**\.
+ To choose sort and distribution keys using your strategy\.

  You can choose sort and distribution keys using Amazon Redshift metadata, statistical information, or both these options\. For **Initial key selection strategy** on the **Optimization strategies** tab, choose one of the following options:
  + Use metadata, ignore statistical information
  + Ignore metadata, use statistical information
  + Use metadata and statistical information

  Depending on the option that you choose, you can select optimization strategies\. Then, for each strategy, enter the value \(0–100\)\. These values define the weight of each strategy\. Using these weight values, AWS SCT defines how each rule influences on the choice of distribution and sort keys\. The default values are based on the AWS migration best practices\.

  You can define the size of small tables for the **Find small tables** strategy\. For **Min table row count** and **Max table row count**, enter the minimum and maximum number of rows in a table to define it as a small table\. AWS SCT applies the `ALL` distribution style to small tables\. In this case, a copy of the entire table is distributed to every node\.
+ To configure strategy details\.

  In addition to defining the weight for each optimization strategy, you can configure the optimization settings\. To do so, choose **Conversion optimization**\. 
  + For **Sort key columns limit**, enter the maximum number of columns in the sort key\.
  + For **Skewed threshold value**, enter the percentage \(0–100\) of a skewed value for a column\. AWS SCT excludes columns with the skew value greater than the threshold from the list of candidates for the distribution key\. AWS SCT defines the skewed value for a column as the percentage ratio of the number of occurrences of the most common value to the total number of records\.
  + For **Top N queries from the query history table**, enter the number \(1–100\) of the most frequently used queries to analyze\.
  + For **Select statistics user**, choose the database user for which you want to analyze the query statistics\.

  Also, on the **Optimization strategies** tab, you can define the size of small tables for the **Find small tables** strategy\. For **Min table row count** and **Max table row count**, enter the minimum and maximum number of rows in a table to consider it as a small table\. AWS SCT applies the `ALL` distribution style to small tables\. In this case, a copy of the entire table is distributed to every node\.