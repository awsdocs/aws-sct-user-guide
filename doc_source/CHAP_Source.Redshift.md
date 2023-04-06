# Using Amazon Redshift as a source for AWS SCT<a name="CHAP_Source.Redshift"></a>

You can use AWS SCT to optimize your Amazon Redshift cluster\. AWS SCT provides you with recommendations on the selection of distribution and sort keys for your Amazon Redshift cluster\. You can consider the Amazon Redshift optimization project as an AWS SCT project with the source and target pointing to the different Amazon Redshift clusters\.

## Privileges for Amazon Redshift as a source database<a name="CHAP_Source.Redshift.Permissions"></a>

The following privileges are required for using Amazon Redshift as a source:
+ USAGE ON SCHEMA *<schema\_name>* 
+ SELECT ON ALL TABLES IN SCHEMA *<schema\_name>* 
+ SELECT ON PG\_CATALOG\.PG\_STATISTIC 
+ SELECT ON SVV\_TABLE\_INFO 
+ SELECT ON TABLE STV\_BLOCKLIST 
+ SELECT ON TABLE STV\_TBL\_PERM 
+ SELECT ON SYS\_SERVERLESS\_USAGE 
+ SELECT ON PG\_DATABASE\_INFO 
+ SELECT ON PG\_STATISTIC 

In the preceding examples, replace the *<schema\_name>* placeholder with the name of the source schema\.

For the privileges required for Amazon Redshift as a target, see [Privileges for Amazon Redshift as a target](CHAP_Converting.DW.md#CHAP_Converting.DW.ConfigureTarget)\.

## Connecting to Amazon Redshift as a source<a name="CHAP_Source.Redshift.Connecting"></a>

Use the following procedure to connect to your Amazon Redshift source database with the AWS Schema Conversion Tool\. 

**To connect to an Amazon Redshift source database**

1. In the AWS Schema Conversion Tool, choose **Add source**\. 

1. Choose **Amazon Redshift**, then choose **Next**\. 

   The **Add source** dialog box appears\.

1. For **Connection name**, enter a name for your database\. AWS SCT displays this name in the tree in the left panel\. 

1. Use database credentials from AWS Secrets Manager or enter them manually:
   + To use database credentials from Secrets Manager, use the following instructions:

     1. For **AWS Secret**, choose the name of the secret\.

     1. Choose **Populate** to automatically fill in all values in the database connection dialog box from Secrets Manager\.

     For information about using database credentials from Secrets Manager, see [Using AWS Secrets Manager](CHAP_UserInterface.md#CHAP_UserInterface.SecretsManager)\.
   + To enter the connection information for the Amazon Redshift source database, use the following instructions:  
****    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/CHAP_Source.Redshift.html)

1. Choose **Test Connection** to verify that AWS SCT can connect to your source database\. 

1. Choose **Connect** to connect to your source database\.

## Amazon Redshift optimization settings<a name="CHAP_Source.Redshift.ConversionSettings"></a>

To edit Amazon Redshift optimization settings, choose **Settings** in AWS SCT, and then choose **Conversion settings**\. From the upper list, choose **Amazon Redshift**, and then choose **Amazon Redshift – Amazon Redshift**\. AWS SCT displays all available settings for Amazon Redshift optimization\.

Amazon Redshift optimization settings in AWS SCT include options for the following:
+ To limit the number of comments with action items in the converted code\.

  For **Add comments in the converted code for the action items of selected severity and higher**, choose the severity of action items\. AWS SCT adds comments in the converted code for action items of the selected severity and higher\.

  For example, to minimize the number of comments in your converted code, choose **Errors only**\. To include comments for all action items in your converted code, choose **All messages**\.
+ To set the maximum number of tables that AWS SCT can apply to your target Amazon Redshift cluster\.

  For **The maximum number of tables for the target Amazon Redshift cluster**, choose the number of tables that AWS SCT can apply to your Amazon Redshift cluster\.

  Amazon Redshift has quotas that limit the use tables for different cluster node types\. If you choose **Auto**, AWS SCT determines the number of tables to apply to your target Amazon Redshift cluster depending on the node type\. Optionally, choose the value manually\. For more information, see [Quotas and limits in Amazon Redshift](https://docs.aws.amazon.com/redshift/latest/mgmt/amazon-redshift-limits.html) in the *Amazon Redshift Cluster Management Guide*\.

  AWS SCT converts all your source tables, even if the number of tables is more than your Amazon Redshift cluster can store\. AWS SCT stores the converted code in your project and doesn't apply it to the target database\. If you reach the Amazon Redshift cluster quota for the tables when you apply the converted code, then AWS SCT displays a warning message\. Also, AWS SCT applies tables to your target Amazon Redshift cluster until the number of tables reaches the limit\.
+ To choose the migration strategy\.

  AWS recommends using different clusters as a source and target for your optimization project\. Before the start of the Amazon Redshift optimization process, you create a copy of your source Amazon Redshift cluster\. You can include your source data into this copy or create an empty cluster\.

  For **Migration strategy**, choose **Migration to a copy** to include data from your source cluster in the target cluster\.

  For **Migration strategy**, choose **Migration to a clean slate** to review the optimization suggestions\. After you accept these suggestions, migrate your source data to the target cluster\.
+ To apply compression to Amazon Redshift table columns\. To do so, select **Use compression encoding**\.

  AWS SCT assigns compression encoding to columns automatically using the default Amazon Redshift algorithm\. For more information, see [Compression encodings](https://docs.aws.amazon.com/redshift/latest/dg/c_Compression_encodings.html) in the *Amazon Redshift Database Developer Guide*\.

  By default, Amazon Redshift doesn't apply compression to columns that are defined as sort and distribution keys\. You can change this behavior and apply compression to these columns\. To do so, select **Use compression encoding for KEY columns**\. You can select this option only when you selected the **Use compression encoding** option\.
+ To work with automatic table optimization\.

  Automatic table optimization is a self\-tuning process in Amazon Redshift that automatically optimizes the design of tables\. For more information, see [Working with automatic table optimization](https://docs.aws.amazon.com/redshift/latest/dg/t_Creating_tables.html) in the *Amazon Redshift Database Developer Guide*\.

  To use only on the automatic table optimization, choose **Optimization strategies** in the left pane\. Then select **Use Amazon Redshift automatic table tuning**, and choose **None** for **Initial key selection strategy**\.
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
  + For **Skewed threshold value**, enter the percentage \(0–100\) of a skewed value for a column\. AWS SCT excludes columns with a skew value greater than the threshold from the list of candidates for the distribution key\. AWS SCT defines the skewed value for a column as the percentage ratio of the number of occurrences of the most common value to the total number of records\.
  + For **Top N queries from the query history table**, enter the number \(1–100\) of the most frequently used queries to analyze\.
  + For **Select statistics user**, choose the database user whose query statistics you want to analyze\.