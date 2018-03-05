# Managing and Customizing Keys in the AWS Schema Conversion Tool<a name="CHAP_SchemaConversionTool.DW.Keys"></a>

After you convert your schema with the AWS Schema Conversion Tool \(AWS SCT\), you can manage and edit your keys\. Key management is the heart of a data warehouse conversion\. 

To manage keys, select a table in your target database, and then choose the **Key Management** tab as shown following\. 

![\[Key management tab\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/key-management.png)

The left pane contains key suggestions, and includes the confidence rating for each suggestion\. You can choose one of the suggestions, or you can customize the key by editing it in the right pane\. 

If the choices for the key don't look like what you expected, you can edit your edit your optimization strategies, and then retry the conversion\. For more information, see [Choosing Optimization Strategies and Rules for Use with the AWS Schema Conversion Tool](CHAP_SchemaConversionTool.DW.Strategy.md)\. 