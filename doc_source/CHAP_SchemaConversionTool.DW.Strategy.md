# Choosing Optimization Strategies and Rules for Use with the AWS Schema Conversion Tool<a name="CHAP_SchemaConversionTool.DW.Strategy"></a>

To optimize how the AWS Schema Conversion Tool \(AWS SCT\) converts your data warehouse schema, you can choose the strategies and rules you want the tool to use\. After converting your schema, and reviewing the suggested keys, you can adjust your rules or change your strategy to get the results you want\. 

**To choose your optimization strategies and rules**

1. Choose **Settings**, and then choose **Project Settings**\. The **Current project settings** dialog box appears\. 

1. In the left pane, choose **Optimization Strategies**\. The optimization strategies appear in the right pane with the defaults selected\. 

1. For **Strategy Sector**, choose the optimization strategy you want to use\. You can choose from the following: 

   + **Use metadata, ignore statistical information** – In this strategy, only information from the metadata is used for optimization decisions\. For example, if there is more than one index on a source table, the source database sort order is used, and the first index becomes a distribution key\. 

      

   + **Ignore metadata, use statistical information** – In this strategy, optimization decisions are derived from statistical information only\. This strategy applies only to tables and columns for which statistics are provided\. For more information, see [ Collecting or Uploading Statistics for the AWS Schema Conversion Tool](CHAP_SchemaConversionTool.DW.Statistics.md)\. 

      

   + **Use metadata and use statistical information** – In this strategy, both metadata and statistics are used for optimization decisions\. 

      

1. After you choose your optimization strategy, you can choose the rules you want to use\. You can choose from the following: 

   + **Choose Distribution Key and Sort Keys using metadata**

   + **Choose fact table and appropriate dimension for collation**

   + **Analyze cardinality of indexes' columns**

   + **Find the most used tables and columns from QueryLog table**

   For each rule, you can enter a weight for the sort key and a weight for the distribution key\. AWS SCT uses the weights you choose when it converts your schema\. Later, when you review the suggested keys, if you are not satisfied with the results, you can return here and change your settings\. For more information, see [ Managing and Customizing Keys in the AWS Schema Conversion Tool](CHAP_SchemaConversionTool.DW.Keys.md)\. 

## Related Topics<a name="w3ab1c17c25b7"></a>

+ [Choose the Best Sort Key](http://docs.aws.amazon.com/redshift/latest/dg/c_best-practices-sort-key.html)

+ [Choose the Best Distribution Style](http://docs.aws.amazon.com/redshift/latest/dg/c_best-practices-best-dist-key.html)