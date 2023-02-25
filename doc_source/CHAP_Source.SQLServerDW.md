# Using Microsoft SQL Server Data Warehouse as a source for AWS SCT<a name="CHAP_Source.SQLServerDW"></a>

You can use AWS SCT to convert schemas, code objects, and application code from Microsoft SQL Server DW to Amazon Redshift or Amazon Redshift and AWS Glue used in combination\. 

## Privileges for Microsoft SQL Server Data Warehouse as a source<a name="CHAP_Source.SQLServerDW.Permissions"></a>

The following privileges are required for using Microsoft SQL Server data warehouse as a source:
+ VIEW DEFINITION 
+ VIEW DATABASE STATE 
+ SELECT ON SCHEMA :: *<schema\_name>* 

In the preceding example, replace the *<source\_schema>* placeholder with the name of the source source\_schema\.

Repeat the grant for each database whose schema you are converting\. 

In addition, grant the following, and run the grant on the master database: 
+ VIEW SERVER STATE 

## Limitations for SQL Server Data Warehouse as a source<a name="CHAP_Source.SQLServerDW.Limitations"></a>

Using Microsoft SQL Server Parallel Data Warehouse \(PDW\) as a source isn't currently supported\.

## Connecting to SQL Server Data Warehouse as a source<a name="CHAP_Source.SQLServerDW.Connecting"></a>

Use the following procedure to connect to your SQL Server Data Warehouse source database with the AWS Schema Conversion Tool\. 

**To connect to a SQL Server Data Warehouse source database**

1. In the AWS Schema Conversion Tool, choose **Add source**\.

1. Choose **Microsoft SQL Server**, then choose **Next**\. 

   The **Add source** dialog box appears\.

1. For **Connection name**, enter a name for your database\. AWS SCT displays this name in the tree in the left panel\. 

1. Use database credentials from AWS Secrets Manager or enter them manually:
   + To use database credentials from Secrets Manager, use the following instructions:

     1. For **AWS Secret**, choose the name of the secret\.

     1. Choose **Populate** to automatically fill in all values in the database connection dialog box from Secrets Manager\.

     For information about using database credentials from Secrets Manager, see [Using AWS Secrets Manager](CHAP_UserInterface.md#CHAP_UserInterface.SecretsManager)\.
   + To enter the Microsoft SQL Server source data warehouse connection information manually, use the following instructions:  
****    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/CHAP_Source.SQLServerDW.html)

1. Choose **Test Connection** to verify that AWS SCT can connect to your source database\. 

1. Choose **Connect** to connect to your source database\.

## SQL Server Data Warehouse to Amazon Redshift conversion settings<a name="CHAP_Source.SQLServerDW.ConversionSettings"></a>

To edit SQL Server Data Warehouse to Amazon Redshift conversion settings, choose **Settings** in AWS SCT, and then choose **Conversion settings**\. From the upper list, choose **Microsoft SQL Server**, and then choose **Microsoft SQL Server – Amazon Redshift**\. AWS SCT displays all available settings for SQL Server Data Warehouse to Amazon Redshift conversion\.

SQL Server Data Warehouse to Amazon Redshift conversion settings in AWS SCT include options for the following:
+ To limit the number of comments with action items in the converted code\.

  For **How detailed should comments be in the converted SQL**, choose the severity of action items\. AWS SCT adds comments in the converted code for action items of the selected severity and higher\.

  For example, to minimize the number of comments in your converted code, choose **Errors only**\. To include comments for all action items in your converted code, choose **All messages**\.
+ To set the maximum number of tables that AWS SCT can apply to your target Amazon Redshift cluster\.

  For **Maximum number of tables for target Amazon Redshift cluster**, choose the number of tables that AWS SCT can apply to your Amazon Redshift cluster\.

  Amazon Redshift has quotas that limit the use tables for different cluster node types\. If you choose **Auto**, AWS SCT determines the number of tables to apply to your target Amazon Redshift cluster depending on the node type\. Optionally, choose the value manually\. For more information, see [Quotas and limits in Amazon Redshift](https://docs.aws.amazon.com/redshift/latest/mgmt/amazon-redshift-limits.html) in the *Amazon Redshift Cluster Management Guide*\.

  AWS SCT converts all your source tables, even if this is more than your Amazon Redshift cluster can store\. AWS SCT stores the converted code in your project and doesn't apply it to the target database\. If you reach the Amazon Redshift cluster quota for the tables when you apply the converted code, then AWS SCT displays a warning message\. Also, AWS SCT applies tables to your target Amazon Redshift cluster until the number of tables reaches the limit\.
+ To migrate partitions of the source table to separate tables in Amazon Redshift\. To do so, select **Use Union all view** and enter the maximum number of target tables that AWS SCT can create for a single source table\.

  Amazon Redshift doesn't support table partitioning\. To emulate this behavior and make queries run faster, AWS SCT can migrate each partition of your source table to a separate table in Amazon Redshift\. Then, AWS SCT creates a view that includes data from all these tables\.

  AWS SCT automatically determines the number of partitions in your source table\. Depending on the type of source table partitioning, this number can exceed the quota for the tables that you can apply to your Amazon Redshift cluster\. To avoid reaching this quota, enter the maximum number of target tables that AWS SCT can create for partitions of a single source table\. The default option is 368 tables, which represents a partition for 366 days of a year and two tables for `NO RANGE` and `UNKNOWN` partitions\.
+ To apply compression to Amazon Redshift table columns\. To do so, select **Use compression encoding**\.

  AWS SCT assigns compression encoding to columns automatically using the default Amazon Redshift algorithm\. For more information, see [Compression encodings](https://docs.aws.amazon.com/redshift/latest/dg/c_Compression_encodings.html) in the *Amazon Redshift Database Developer Guide*\.

  By default, Amazon Redshift doesn't apply compression to columns that are defined as sort and distribution keys\. You can change this behavior and apply compression to these columns\. To do so, select **Use compression encoding for KEY columns**\. You can select this option only when you select the **Use compression encoding** option\.

## SQL Server Data Warehouse to Amazon Redshift conversion optimization settings<a name="CHAP_Source.SQLServerDW.ConversionOptimizationSettings"></a>

To edit SQL Server Data Warehouse to Amazon Redshift conversion optimization settings, choose **Settings** in AWS SCT, and then choose **Conversion settings**\. From the upper list, choose **Microsoft SQL Server**, and then choose **Microsoft SQL Server – Amazon Redshift**\. In the left pane, choose **Optimization strategies**\. AWS SCT displays conversion optimization settings for SQL Server Data Warehouse to Amazon Redshift conversion\.

SQL Server Data Warehouse to Amazon Redshift conversion optimization settings in AWS SCT include options for the following:
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