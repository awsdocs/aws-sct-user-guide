# Optimizing Amazon Redshift by Using the AWS Schema Conversion Tool<a name="CHAP_SchemaConversionTool.RedshiftOpt"></a>

You can use the AWS Schema Conversion Tool \(AWS SCT\) to optimize your Amazon Redshift database\. Using your Amazon Redshift database as a source, and a test Amazon Redshift database as the target, AWS SCT recommends sort keys and distribution keys to optimize your database\. 

## Before You Begin<a name="CHAP_SchemaConversionTool.RedshiftOpt.Before"></a>

Almost all work you do with AWS SCT starts with the same three steps\. Complete the following steps before you optimize your Amazon Redshift database: 

1. Create an AWS SCT project\. For more information, see [ Creating an AWS Schema Conversion Tool Project](CHAP_SchemaConversionTool.GettingStarted.md#CHAP_SchemaConversionTool.GettingStarted.Project)\. 

1. Connect to your source database\. For more information, see [Connecting to an Amazon Redshift Source Database](CHAP_SchemaConversionTool.GettingStarted.Source.Redshift.md)\. 

1. Connect to your target database\. For more information, see [ Connecting to Your Target Database](CHAP_SchemaConversionTool.GettingStarted.md#CHAP_SchemaConversionTool.GettingStarted.Target)\. 
**Important**  
Don't use the same cluster for both the source and target of your optimization\. 

Before you optimize your Amazon Redshift database, you should also choose your optimization strategies\. For more information, see [Choosing Optimization Strategies and Rules for Use with the AWS Schema Conversion Tool](CHAP_SchemaConversionTool.DW.Strategy.md)\. 

## Optimizing Your Amazon Redshift Database<a name="CHAP_SchemaConversionTool.RedshiftOpt.Opt"></a>

Use the following procedure to optimize your Amazon Redshift database\.

**To optimize your Amazon Redshift database**

1. Take a manual snapshot of your Amazon Redshift cluster as a backup\. You can delete the snapshot after you are done optimizing your Amazon Redshift cluster and testing any changes that you make\. For more information, see [Amazon Redshift Snapshots](http://docs.aws.amazon.com/redshift/latest/mgmt/working-with-snapshots.html)\. 

1. Choose a schema object to convert from the left panel of your project\. Open the context \(right\-click\) menu for the object, and then choose **Collect Statistics**\. 

   AWS SCT uses the statistics to make suggestions for sort keys and distribution keys\. 

1. Choose a schema object to optimize from the left panel of your project\. Open the context \(right\-click\) menu for the object, and then choose **Run Optimization**\. 

   AWS SCT makes suggestions for sort keys and distribution keys\. 

1. To review the suggestions, expand the tables node under your schema in the left panel of your project, and then choose a table\. Choose the **Key Management** tab as shown following\.   
![\[Key management tab\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/key-management.png)

   The left pane contains key suggestions, and includes the confidence rating for each suggestion\. You can choose one of the suggestions, or you can customize the key by editing it in the right pane\. 

1. You can create a report that contains the optimization suggestions\. To create the report, do the following: 

   1. Choose a schema object that you optimized from the left panel of your project\. Open the context \(right\-click\) menu for the object, and then choose **Create Report**\. 

      The report opens in the main window, and the **Summary** tab appears\. The number of objects with optimization suggestions appears in the report\. 

   1. Choose the **Action Items** tab to see the key suggestions in a report format\. 

   1. You can save a local copy of the optimization report as either a PDF file or a comma\-separated values \(CSV\) file\. The CSV file contains only action item information\. The PDF file contains both the summary and action item information\. 

1. To apply suggested optimizations to your database, choose an object in the right panel of your project\. Open the context \(right\-click\) menu for the object, and then choose **Apply to database**\. 