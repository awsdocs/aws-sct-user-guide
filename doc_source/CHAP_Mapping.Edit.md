# Managing mapping rules<a name="CHAP_Mapping.Edit"></a>

You can filter or delete existing mapping rules, and add a new mapping rule in your AWS Schema Conversion Tool \(AWS SCT\) project\.

When you create a mapping rule for the whole source database, AWS SCT creates one mapping rule for each source database schema\. For projects that involve dozens of schemas or even databases, it may be hard to understand, which target is used for a certain schema\. To quickly find a mapping rule for your schema, use one or several of the following filter options in AWS SCT\.

**To filter mapping rules**

1. On the **View** menu, choose **Mapping view**\.

1. For **Source servers**, choose the source database\.

   The filter default is **All**, which means that AWS SCT displays mapping rules for all source databases\.

1. For **Source schema**, enter the source schema name\. Use the percent \(`%`\) as a wildcard to replace any number of any symbols in the schema name\.

   The filter default is the **%** wildcard, which means that AWS SCT displays mapping rules for all source database schema names\.

1. For **Has migration rules**, choose **Yes** to display mapping rules for which the data migration rules are created\. Choose **No** to display mapping rules which don't have data migration rules\. For more information, see [Creating data migration rules in the AWS SCT](agents.dw.md#agents.Filtering)\.

   The filter default is **All**, which means that AWS SCT displays all mapping rules\.

1. For **Target servers**, choose the target database\.

   The filter default is **All**, which means that AWS SCT displays mapping rules for all target databases\.

With your project open, use the following procedure to delete a mapping rule\. For more information on adding mapping rules, see [Adding a new mapping rule](CHAP_Mapping.New.md)\.

**To delete mapping rules**

1.  On the **View** menu, choose **Mapping view**\. 

1. For **Server mappings**, choose the mapping rules to delete\. 

1. Choose **Delete selected mappings**\.

    AWS SCT deletes the selected mapping rules\. 