# Collecting or Uploading Statistics for the AWS Schema Conversion Tool<a name="CHAP_SchemaConversionTool.DW.Statistics"></a>

To optimize how the AWS Schema Conversion Tool \(AWS SCT\) converts your data warehouse schema, you can provide statistics from your source database that the tool can use\. You can either collect statistics directly from the database, or upload an existing statistics file\. 

**To provide and review statistics**

1. Connect to your source database\. For more information, see [ Connecting to Your Source Database](CHAP_SchemaConversionTool.GettingStarted.md#CHAP_SchemaConversionTool.Converting.CreateProject)\. 

1. Choose a schema object from the left panel of your project, and open the context \(right\-click\) menu for the object\. Choose **Collect Statistics** or **Upload Statistics** as shown following\.   
![\[Context menu with collect statistics\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/collect-statistics.png)

1. Choose a schema object from the left panel of your project, and then choose the **Statistics** tab\. You can review the statistics for the object\.   
![\[Statistics tab\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/statistics.png)

   Later, when you review the suggested keys, if you are not satisfied with the results, you can collect additional statistics and repeat this procedure\. For more information, see [ Managing and Customizing Keys in the AWS Schema Conversion Tool](CHAP_SchemaConversionTool.DW.Keys.md)\. 

## Related Topics<a name="w3ab1c17c27b7"></a>

+ [Choosing Optimization Strategies and Rules for Use with the AWS Schema Conversion Tool](CHAP_SchemaConversionTool.DW.Strategy.md)

+ [Choose the Best Sort Key](http://docs.aws.amazon.com/redshift/latest/dg/c_best-practices-sort-key.html)

+ [Choose the Best Distribution Style](http://docs.aws.amazon.com/redshift/latest/dg/c_best-practices-best-dist-key.html)