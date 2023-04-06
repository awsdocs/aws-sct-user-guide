# Using Snowflake as a source for AWS SCT<a name="CHAP_Source.Snowflake"></a>

You can use AWS SCT to convert schemas, code objects, and application code from Snowflake to Amazon Redshift\.

## Privileges for Snowflake as a source database<a name="CHAP_Source.Snowflake.Permissions"></a>

You can create a role with privileges and grant this role the name of a user by using the `SECURITYADMIN` role and the `SECURITYADMIN` session context\.

The example following creates minimal privileges and grants them to the `min_privs` user\. 

```
create role role_name;
grant role role_name to role sysadmin;
grant usage on database db_name to role role_name;
grant usage on schema db_name.schema_name to role role_name;             
grant usage on warehouse datawarehouse_name to role role_name;
grant monitor on database db_name to role role_name;
grant monitor on warehouse datawarehouse_name to role role_name;
grant select on all tables in schema db_name.schema_name to role role_name;
grant select on future tables in schema db_name.schema_name to role role_name;
grant select on all views in schema db_name.schema_name to role role_name;
grant select on future views in schema db_name.schema_name to role role_name;
grant select on all external tables in schema db_name.schema_name to role role_name;
grant select on future external tables in schema db_name.schema_name to role role_name;
grant usage on all sequences in schema db_name.schema_name to role role_name;
grant usage on future sequences in schema db_name.schema_name to role role_name;
grant usage on all functions in schema db_name.schema_name to role role_name;
grant usage on future functions in schema db_name.schema_name to role role_name;
grant usage on all procedures in schema db_name.schema_name to role role_name;
grant usage on future procedures in schema db_name.schema_name to role role_name;
create user min_privs password='real_user_password'  
DEFAULT_ROLE = role_name DEFAULT_WAREHOUSE = 'datawarehouse_name';
grant role role_name to user min_privs;
```

In the preceding example, replace placeholders as following:
+ Replace *`role_name`* with the name of a role with read\-only privileges\.
+ Replace `db_name` with the name of the source database\.
+ Replace `schema_name` with the name of the source schema\.
+ Replace *`datawarehousename`* with the name of a required data warehouse\.
+ Replace `min_privs` with the name of a user that has minimal privileges\.

The `DEFAULT_ROLE` and `DEFAULT_WAREHOUSE` parameters are key\-sensitive\.

## Configuring secure access to Amazon S3<a name="CHAP_Source.Snowflake.IAM"></a>

Security and access management policies for an Amazon S3 bucket allow Snowflake to access, read data from, and write data to the S3 bucket\. You can configure secure access to a private Amazon S3 bucket using the Snowflake `STORAGE INTEGRATION` object type\. A Snowflake storage integration object delegates authentication responsibility to a Snowflake identity and access management entity\.

For more information, see [Configuring a Snowflake Storage Integration to Access Amazon S3](https://docs.snowflake.com/en/user-guide/data-load-s3-config-storage-integration.html) in the Snowflake documentation\.

## Connecting to Snowflake as a source<a name="CHAP_Source.Snowflake.Connecting"></a>

Use the following procedure to connect to your source database with the AWS Schema Conversion Tool\. 

**To connect to an Snowflake source database**

1. In the AWS Schema Conversion Tool, choose **Add source**\. 

1. Choose **Snowflake**, then choose **Next**\. 

   The **Add source** dialog box appears\.

1. For **Connection name**, enter a name for your database\. AWS SCT displays this name in the tree in the left panel\. 

1. Use database credentials from AWS Secrets Manager or enter them manually:
   + To use database credentials from Secrets Manager, use the following instructions:

     1. For **AWS Secret**, choose the name of the secret\.

     1. Choose **Populate** to automatically fill in all values in the database connection dialog box from Secrets Manager\.

     For information about using database credentials from Secrets Manager, see [Using AWS Secrets Manager](CHAP_UserInterface.md#CHAP_UserInterface.SecretsManager)\.
   + To enter the Snowflake source data warehouse connection information manually, use the following instructions:  
****    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/CHAP_Source.Snowflake.html)

1. Choose **Test Connection** to verify that AWS SCT can connect to your source database\. 

1. Choose **Connect** to connect to your source database\.

## Limitations for Snowflake as a source<a name="CHAP_Source.Snowflake.Limitations"></a>

The following are limitations when using Snowflake as a source for AWS SCT:
+ Object identifiers must be unique within the context of the object type and the parent object:  
**Database**  
Schema identifiers must be unique within a database\.  
**Schemas**  
Objects identifiers such as for tables and views must be unique within a schema\.  
**Tables/Views**  
Column identifiers must be unique within a table\.
+ The maximum number of tables for large and xlarge cluster node types is 9,900\. For 8xlarge cluster node types, the maximum number of tables is 100,000\. The limit includes temporary tables, both user\-defined and created by Amazon Redshift during query processing or system maintenance\. For more information, see [Amazon Redshift quotas](https://docs.aws.amazon.com/redshift/latest/mgmt/amazon-redshift-limits.html) in the *Amazon Redshift Cluster Management Guide*\.
+ For stored procedures, the maximum number of input and output arguments is 32\.

## Source data types for Snowflake<a name="CHAP_Source.Snowflake.DataTypes"></a>

Following, you can find the Snowflake source data types that are supported when using AWS SCT and the default mapping to an Amazon Redshift target\.


| Snowflake data types | Amazon Redshift data types | 
| --- | --- | 
|  NUMBER  |  NUMERIC\(38\)  | 
|  NUMBER\(p\)  |  If p is =< 4, then SMALLINT If p is => 5 and =< 9, then INTEGER If p is => 10 and =< 18, then BIGINT If p is => 19 then NUMERIC\(p\)   | 
|  NUMBER\(p, 0\)  |  If p is =< 4, then SMALLINT If p is => 5 and =< 9, then INTEGER If p is => 10 and =< 18, then BIGINT If p is => 19 then: NUMERIC\(p,0\)  | 
|  NUMBER\(p, s\)  |  If p is => 1 and =< 38, and if s is => 1 and =< 37, then NUMERIC\(p,s\)   | 
|  FLOAT  | FLOAT | 
|  TEXT Unicode characters up to 16,777,216 bytes; up to 4 bytes per character\.  |  VARCHAR\(MAX\)  | 
|  TEXT\(p\) Unicode characters up to 65,535 bytes; up to 4 bytes per character\.  |  If p is =< 65,535 then, VARCHAR\(p\)  | 
|  TEXT\(p\) Unicode characters up to 16,777,216 bytes; up to 4 bytes per character\.  |  If p is => 65,535 and =< 16,777,216 then, VARCHAR\(MAX\)  | 
|  BINARY Single\-byte characters up to 8,388,608 bytes; 1 byte per character\.  | VARCHAR\(MAX\) | 
|  BINARY\(p\) Single\-byte characters up to 65,535 bytes; 1 byte per character\.  | VARCHAR\(p\) | 
|  BINARY\(p\) Single\-byte characters up to 8,388,608 bytes; 1 byte per character\.  | VARCHAR\(MAX\) | 
|  BOOLEAN  | BOOLEAN | 
|  DATE  | DATE | 
|  TIME Time values between 00:00:00 and 23:59:59\.999999999\.  | VARCHAR\(18\) | 
|  TIME\(f\) Time values between 00:00:00 and 23:59:59\.9\(f\)\.   | VARCHAR\(n\) – 9 \+ dt\-attr\-1 | 
|  TIMESTAMP\_NTZ  | TIMESTAMP | 
|  TIMESTAMP\_TZ  | TIMESTAMPTZ | 

## Snowflake to Amazon Redshift conversion settings<a name="CHAP_Source.Snowflake.ConversionSettings"></a>

To edit Snowflake to Amazon Redshift conversion settings, choose **Settings** in AWS SCT, and then choose **Conversion settings**\. From the upper list, choose **Snowflake**, and then choose **Snowflake – Amazon Redshift**\. AWS SCT displays all available settings for Snowflake to Amazon Redshift conversion\.

Snowflake to Amazon Redshift conversion settings in AWS SCT include options for the following:
+ To limit the number of comments with action items in the converted code\.

  For **Add comments in the converted code for the action items of selected severity and higher**, choose the severity of action items\. AWS SCT adds comments in the converted code for action items of the selected severity and higher\.

  For example, to minimize the number of comments in your converted code, choose **Errors only**\. To include comments for all action items in your converted code, choose **All messages**\.
+ To set the maximum number of tables that AWS SCT can apply to your target Amazon Redshift cluster\.

  For **The maximum number of tables for the target Amazon Redshift cluster**, choose the number of tables that AWS SCT can apply to your Amazon Redshift cluster\.

  Amazon Redshift has quotas that limit the use tables for different cluster node types\. If you choose **Auto**, AWS SCT determines the number of tables to apply to your target Amazon Redshift cluster depending on the node type\. Optionally, choose the value manually\. For more information, see [Quotas and limits in Amazon Redshift](https://docs.aws.amazon.com/redshift/latest/mgmt/amazon-redshift-limits.html) in the *Amazon Redshift Cluster Management Guide*\.

  AWS SCT converts all your source tables, even if this is more than your Amazon Redshift cluster can store\. AWS SCT stores the converted code in your project and doesn't apply it to the target database\. If you reach the Amazon Redshift cluster quota for the tables when you apply the converted code, then AWS SCT displays a warning message\. Also, AWS SCT applies tables to your target Amazon Redshift cluster until the number of tables reaches the limit\.
+ To apply compression to Amazon Redshift table columns\. To do so, select **Use compression encoding**\.

  AWS SCT assigns compression encoding to columns automatically using the default Amazon Redshift algorithm\. For more information, see [Compression encodings](https://docs.aws.amazon.com/redshift/latest/dg/c_Compression_encodings.html) in the *Amazon Redshift Database Developer Guide*\.

  By default, Amazon Redshift doesn't apply compression to columns that are defined as sort and distribution keys\. You can change this behavior and apply compression to these columns\. To do so, select **Use compression encoding for KEY columns**\. You can select this option only when you select the **Use compression encoding** option\.

## Snowflake to Amazon Redshift conversion optimization settings<a name="CHAP_Source.Snowflake.ConversionOptimizationSettings"></a>

To edit Snowflake to Amazon Redshift conversion optimization settings, choose **Settings** in AWS SCT, and then choose **Conversion settings**\. From the upper list, choose **Snowflake**, and then choose **Snowflake – Amazon Redshift**\. In the left pane, choose **Optimization strategies**\. AWS SCT displays conversion optimization settings for Snowflake to Amazon Redshift conversion\.

Snowflake to Amazon Redshift conversion optimization settings in AWS SCT include options for the following:
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