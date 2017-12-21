# Creating Mapping Rules in the AWS Schema Conversion Tool<a name="CHAP_SchemaConversionTool.Mapping"></a>

Before you convert your schema with the AWS Schema Conversion Tool \(AWS SCT\), you can set up rules that change the data type of columns, move objects from one schema to another, and change the names of objects\. For example, if you have a set of tables in your source schema named `test_TABLE_NAME`, you can set up a rule that changes the prefix `test_` to the prefix `demo_` in the target schema\. 

**Note**  
You can only create mapping rules if your source database engine and target database engine are different\. 

You can create mapping rules that perform the following tasks: 

+ Change data type 

+ Move objects 

+ Rename objects 

+ Prefix \- add prefix, remove prefix, replace prefix 

+ Suffix \- add suffix, remove suffix, replace suffix 

You can create mapping rules for the following objects: 

+ Database 

+ Schema 

+ Table 

+ Column 

## Creating Mapping Rules<a name="CHAP_SchemaConversionTool.Mapping.Map"></a>

You can create mapping rules and save the rules as part of your project\. With your project open, use the following procedure to create mapping rules\. 

**To create mapping rules**

1. Choose **Mapping Rules** from the **Settings** menu\. The **Mapping Rules** dialog box appears\.   
![\[The mapping rules dialog box\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/mapping-rules-2.PNG)

1. Choose **Add new rule**\. A new row is added to the list of rules\. 

1. Choose the edit icon to configure your rule\. 

   1. For **Name**, type a name for your rule\. 

   1. For **For**, choose the type of object that the rule applies to\. 

   1. For **where**, type a filter to apply to objects before applying the mapping rule\. The where clause is evaluated by using a like clause\. You can enter an exact name to select one object, or you can enter a pattern to select multiple objects\. 

      The fields available for the **where** clause are different depending on the type of the object\. For example, if the object type is schema there is only one field available, for the schema name\. 

   1. For **Actions**, choose the type of mapping rule you want to create\. 

   1. Depending on the rule type, type one or two additional values\. For example, to rename an object, type the new name of the object\. To replace a prefix, type the old prefix and the new prefix\. 

1. After you have configured your mapping rule, choose **Save** to save your rule\. You can also choose **Cancel** to cancel your changes\. 

1. After you are done adding, editing, and deleting rules, choose **Save All** to save all your changes\. 

1. Choose **Close** to close the **Mapping Rules** dialog box\. 

You can use the toggle icon to turn off a mapping rule without deleting it\. You can use the copy icon to duplicate an existing mapping rule\. You can use the delete icon to delete an existing mapping rule\. To save any changes you make to your mapping rules, choose **Save All**\. 

## Viewing Mapping Rules for Objects<a name="CHAP_SchemaConversionTool.Mapping.View"></a>

After you set up your mapping rules, you can view the effect of the rules on specific objects in your schema before you convert your schema\. In the source schema tree, choose the object you are interested in\. In the main view, choose the **Mapping** tab\. The **Mapping** tab opens and displays a list of all mapping rules that are applied to the object\. You can see the name of the object in the source schema and the new name of the object in the target schema\. If you have data type rules, you also see the data type of the column in the source schema and the new data type of the column in the target schema\. 

## Exporting Mapping Rules<a name="CHAP_SchemaConversionTool.Mapping.Export"></a>

If you use AWS Database Migration Service \(AWS DMS\) to migrate your data from your source database to your target database, you can provide information about your mapping rules to AWS DMS\. For more information about tasks, see [Working with AWS Database Migration Service Replication Tasks](http://docs.aws.amazon.com/dms/latest/userguide/CHAP_Tasks.html)\. 

**To export mapping rules**

1. In the AWS Schema Conversion Tool, in the source schema tree, open the context \(right\-click\) menu and choose **Export script for DMS**\. The save dialog box opens\. 

1. Browse to the location where you want to save your script, and then choose **Save**\. Your mapping rules are saved as a JSON script that can be consumed by AWS DMS\. 