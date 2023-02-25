# Converting Teradata MultiLoad job scripts to Amazon Redshift RSQL with AWS SCT<a name="CHAP-converting-multiload-rsql"></a>

You can use AWS SCT to convert Teradata MultiLoad job scripts to Amazon Redshift RSQL\.

A *Teradata MultiLoad job script* is a set of commands for batch maintenance of your Teradata Database\. A Teradata MultiLoad import task performs a number of different insert, update, and delete operations on up to five different tables and views\. Teradata MultiLoad delete tasks can remove large numbers of rows from a single table\.

AWS SCT converts Teradata MultiLoad commands and SQL statements to a format compatible with Amazon Redshift RSQL\. After you migrate the Teradata database to Amazon Redshift, use these converted scripts to manage data in your Amazon Redshift database\.

**Topics**
+ [Adding MultiLoad job scripts to your AWS SCT project](#CHAP-converting-multiload-rsql-create)
+ [Configuring substitution variables in Teradata MultiLoad job scripts with AWS SCT](#CHAP-converting-multiload-rsql-variables)
+ [Converting Teradata MultiLoad job scripts with AWS SCT](#CHAP-converting-multiload-rsql-convert)
+ [Managing Teradata MultiLoad job scripts with AWS SCT](#CHAP-converting-multiload-rsql-manage)
+ [Creating an assessment report for a Teradata MultiLoad job script conversion with AWS SCT](#CHAP-converting-multiload-rsql-assessment)
+ [Editing and saving your converted Teradata MultiLoad job scripts with AWS SCT](#CHAP-converting-multiload-rsql-save)

## Adding MultiLoad job scripts to your AWS SCT project<a name="CHAP-converting-multiload-rsql-create"></a>

You can add multiple scripts to a single AWS SCT project\.

**To add a MultiLoad job script to your AWS SCT project**

1. Create a new project in AWS SCT or open an existing project\. For more information, see [Creating an AWS SCT project](CHAP_UserInterface.md#CHAP_UserInterface.Project)\. 

1. Choose **Add source** from the menu, and then choose **Teradata** to add your source database to the project\. For more information, see [Using Teradata as a source](CHAP_Source.Teradata.md)\.

1. Choose **Add target** from the menu and to add a target Amazon Redshift database to your AWS SCT project\.

   You can use a virtual Amazon Redshift target database platform\. For more information, see [Using virtual targets](CHAP_Mapping.VirtualTargets.md)\.

1. Create a new mapping rule that includes your source Teradata database and your Amazon Redshift target\. For more information, see [Adding a new mapping rule](CHAP_Mapping.New.md)\. 

1. On the **View** menu, choose **Main view**\.

1. In the left panel, expand the **Scripts** node\.

1.  Choose **MultiLoad**, open the context \(right\-click\) menu, and then choose **Load scripts**\.

1.  Enter the location of your source Teradata MultiLoad job scripts and choose **Select folder**\.

   AWS SCT displays the **Load scripts** window\.

1. Do one of the following:
   + If your Teradata MultiLoad job scripts don't include the substitution variables, choose **No substitution variables**, and then choose **OK** to add scripts to your AWS SCT project\.
   + If your Teradata MultiLoad job scripts include the substitution variables, configure the substitution variables\. For more information, see [Configuring substitution variables in MultiLoad job scripts](#CHAP-converting-multiload-rsql-variables)\.

## Configuring substitution variables in Teradata MultiLoad job scripts with AWS SCT<a name="CHAP-converting-multiload-rsql-variables"></a>

Your Teradata MultiLoad job scripts might include substitution variables\. For example, you can use a single script with substitution variables to load data to different databases\.

Before you run a MultiLoad job script with substitution variables, make sure to assign the values for all variables\. To do this, you can use other tools or applications such as a Bash script, UC4 \(Automic\), and so on\.

AWS SCT can resolve and convert substitution variables only after you assign their values\. Before you start the conversion of your source Teradata MultiLoad job scripts, make sure that you assigned values for all substitution variables\. You can use AWS SCT to configure substitution variables in your Teradata scripts\. 

**To configure substitution variables in your MultiLoad job script**

1. When you add your source Teradata MultiLoad job scripts to your AWS SCT project, choose **Substitution variables are used**\. For more information about adding these scripts, see [Adding MultiLoad job scripts to your AWS SCT project](#CHAP-converting-multiload-rsql-create)\. 

1. For **Define variable format**, enter a regular expression that matches all substitution variables in your script\.

   For example, if the names of your substitution variables start with `${` and end with `}`, use the `\$\{\w+\}` regular expression\. To match substitution variables that start either with a dollar sign or a percent sign, use the `\$\w+|\%\w+` regular expression\.

   Regular expressions in AWS SCT conform to the Java regular expression syntax\. For more information, see [java\.util\.regex Class Pattern](https://docs.oracle.com/javase/6/docs/api/java/util/regex/Pattern.html) in the Java documentation\.

1. Choose **OK** to load scripts to your AWS SCT project, and then choose **OK** to close the **Load scripts** window\.

1. Choose **Variables** to view all discovered substitution variables and their values\.

1. For **Value**, enter the value for the substitution variable\.

## Converting Teradata MultiLoad job scripts with AWS SCT<a name="CHAP-converting-multiload-rsql-convert"></a>

Following, find how to convert Teradata MultiLoad job to Amazon Redshift RSQL using AWS SCT\. 

**To convert a Teradata MultiLoad job script to Amazon Redshift RSQL**

1. Add your MultiLoad job scripts to your AWS SCT project\. For more information, see [Adding MultiLoad job scripts to your AWS SCT project](#CHAP-converting-multiload-rsql-create)\.

1. Configure the substitution variables and enter their values\. For more information, see [Configuring substitution variables in MultiLoad job scripts](#CHAP-converting-multiload-rsql-variables)\.

1. In the left panel, expand the **Scripts** node\.

1. Do one of the following:
   + To convert a single MultiLoad job script, expand the **MultiLoad** node, choose the script to convert, and then choose **Convert script** from the context \(right\-click\) menu\.
   + To covert multiple scripts, make sure that you select all scripts to convert\. Choose **MultiLoad**, open the context \(right\-click\) menu, and then choose **Convert script**\. 

1. Do one of the following:
   + If you store your source data file on Amazon S3, choose **S3 object path** for **Source data file location**\.

     Enter **Amazon S3 bucket folder** and **Amazon S3 bucket for manifest file** for your source data file\.
   + If you don't store your source data file on Amazon S3, choose **Host address** for **Source data file location**\.

     Enter **URL or IP address of the host**, **Host user login name**, and **Amazon S3 bucket for manifest file** for your source data file\.

1. Choose **OK**\.

   AWS SCT converts all your selected Teradata MultiLoad job scripts to a format compatible with Amazon Redshift RSQL\. Find your converted scripts in the **Scripts** node in the target database panel\.

1. Edit your converted Amazon Redshift RSQL scripts or save them\. For more information, see [Editing and saving your converted MultiLoad job scripts](#CHAP-converting-multiload-rsql-save)\.

## Managing Teradata MultiLoad job scripts with AWS SCT<a name="CHAP-converting-multiload-rsql-manage"></a>

You can add multiple Teradata MultiLoad job scripts or remove a MultiLoad job script from your AWS SCT project\.

**To add a new MultiLoad job script to your AWS SCT project**

1. Expand the **Scripts** node in the left panel\.

1. Choose the **MultiLoad** node and open the context \(right\-click\) menu\.

1. Choose **Load scripts**\.

1. Enter the information that is required to add a new MultiLoad job script and configure substitution variables\. For more information, see [Adding MultiLoad job scripts to your AWS SCT project](#CHAP-converting-multiload-rsql-create) and [Configuring substitution variables in MultiLoad job scripts](#CHAP-converting-multiload-rsql-variables)\.

**To remove a MultiLoad job script from your AWS SCT project**

1. Expand the **MultiLoad** node under **Scripts** in the left panel\.

1. Choose the script to remove, and open the context \(right\-click\) menu\.

1. Choose **Delete script**\.

## Creating an assessment report for a Teradata MultiLoad job script conversion with AWS SCT<a name="CHAP-converting-multiload-rsql-assessment"></a>

The *MultiLoad job script conversion assessment report* provides information about converting the MultiLoad commands and SQL statements\. The conversion is from your source scripts to Amazon Redshift RSQL commands and SQL statements for Amazon Redshift\. The assessment report includes action items for MultiLoad commands and SQL statements that AWS SCT can't convert\. 

**To create a script conversion assessment report for a Teradata MultiLoad job**

1. Expand the **MultiLoad** node under **Scripts** in the left panel\.

1. Choose the scripts to create the assessment report for, open the context \(right\-click\) menu, and then choose **Create report**\.

1. View the **Summary** tab\. The **Summary** tab displays the executive summary information from the MultiLoad job script assessment report\. It includes conversion results for all MultiLoad commands and SQL statements from your source scripts\. 

1. \(Optional\) Save a local copy of the MultiLoad job script conversion assessment report as either a PDF file or comma\-separated value \(CSV\) files:
   + To save the MultiLoad job script conversion assessment report as a PDF file, choose **Save to PDF** at upper right\.

      The PDF file contains the executive summary, action items, and recommendations for scripts conversion\.
   + To save the MultiLoad job script conversion assessment report as CSV files, choose **Save to CSV ** at upper right\.

     AWS SCT creates two CSV files\. These files contain the executive summary, action items, recommended actions, and an estimated complexity of manual effort required to convert the scripts\.

1. Choose the **Action items** tab\. This tab contains a list of items that require manual conversion to Amazon Redshift RSQL\. When you select an action item from the list, AWS SCT highlights the item from your source MultiLoad job script that the action item applies to\. 

## Editing and saving your converted Teradata MultiLoad job scripts with AWS SCT<a name="CHAP-converting-multiload-rsql-save"></a>

You can edit your converted scripts in the lower panel of your AWS SCT project\. AWS SCT stores the edited script as part of your project\.

**To save your converted scripts**

1. Expand the **RSQL scripts** node under **Scripts** in the target database panel\.

1. Choose your converted script, open the context \(right\-click\) menu, and choose **Save script**\.

1. Enter the path to the folder to save the converted script and choose **Save**\.

   AWS SCT saves the converted script to a file and opens this file\.