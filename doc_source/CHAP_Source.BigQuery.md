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