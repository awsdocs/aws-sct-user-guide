# Converting Teradata FastExport job scripts to Amazon Redshift RSQL with AWS SCT<a name="CHAP-converting-fastexport-rsql"></a>

You can use the AWS Schema Conversion Tool \(AWS SCT\) to convert Teradata FastExport job scripts to Amazon Redshift RSQL\.

A *FastExport job script* is a set of FastExport commands and SQL statements that select and export data from the Teradata database\. AWS SCT converts FastExport commands and SQL statements to a format compatible with Amazon Redshift RSQL\. After you migrate the Teradata database to Amazon Redshift, you can use these converted scripts to export data from the Amazon Redshift database\.

## Adding FastExport job scripts to your AWS SCT project<a name="CHAP-converting-fastexport-rsql-create"></a>

You can add multiple scripts to a single AWS SCT project\.

**To add a FastExport job script to your AWS SCT project**

1. Create a new project in AWS SCT or open an existing project\. For more information, see [Creating an AWS SCT project](CHAP_UserInterface.md#CHAP_UserInterface.Project)\. 

1. Choose **Add source** from the menu, and then choose **Teradata** to add your source database to the project\. For more information, see [Using Teradata as a source](CHAP_Source.Teradata.md)\.

1. Choose **Add target** from the menu and to add a target Amazon Redshift database to your AWS SCT project\.

   You can use a virtual Amazon Redshift target database platform\. For more information, see [Using virtual targets](CHAP_Mapping.VirtualTargets.md)\.

1. Create a new mapping rule that includes your source Teradata database and your Amazon Redshift target\. For more information, see [Adding a new mapping rule](CHAP_Mapping.New.md)\. 

1. On the **View** menu, choose **Main view**\.

1. In the left panel, expand the **Scripts** node\.

1.  Choose **FastExport**, open the context \(right\-click\) menu, and then choose **Load scripts**\.

1.  Enter the location of the source code for your Teradata FastExport job scripts and choose **Select folder**\.

   AWS SCT displays the **Load scripts** window\.

1. Do one of the following:
   + If your Teradata FastExport job scripts don't include the substitution variables, choose **No substitution variables** and then choose **OK** to add scripts to your AWS SCT project\.
   + If your Teradata FastExport job scripts include the substitution variables, configure the substitution variables\. For more information, see [Configuring substitution variables in FastExport job scripts](#CHAP-converting-fastexport-rsql-variables)\.

## Configuring substitution variables in Teradata FastExport job scripts with AWS SCT<a name="CHAP-converting-fastexport-rsql-variables"></a>

Your Teradata FastExport job scripts can include substitution variables\. For example, you can use a single script with substitution variables to export data from multiple databases\. You can use AWS SCT to configure substitution variables in your Teradata scripts\.

Before you run a FastExport job script with substitution variables, make sure to assign the values for all variables\. To do this, you can use other tools or applications such as a Bash script, UC4 \(Automic\), and so on\. AWS SCT can resolve and convert substitution variables only after you assign their values\.

**To configure substitution variables in your FastExport job script**

1. Add your source Teradata FastExport job scripts to your AWS SCT project\. For more information, see [Adding BTEQ scripts to your AWS SCT project](CHAP-converting-bteq-rsql.md#CHAP-converting-bteq-rsql-create)\. 

   When you add your scripts, choose **Substitution variables are used**\.

1. For **Define variable format**, enter a regular expression that matches all substitution variables in your script\.

   For example, if the names of your substitution variables start with `${` and end with `}`, use the `\$\{\w+\}` regular expression\. To match substitution variables that start either with a dollar sign or a percent sign, use the `\$\w+|\%\w+` regular expression\.

   Regular expressions in AWS SCT conform to the Java regular expression syntax\. For more information, see [java\.util\.regex Class Pattern](https://docs.oracle.com/javase/6/docs/api/java/util/regex/Pattern.html) in the Java documentation\.

1. Choose **OK** to load scripts to your AWS SCT project, and then choose **OK** to close the **Load scripts** window\.

1. In the left panel, expand the **Scripts** node\. Choose **FastExport**, and then choose your folder with scripts\. Open the context \(right\-click\) menu, and then choose **Export variables** under **Substitution variables**\.

1. Export substitution variables for one script\. Expand your folder with scripts, choose your script, open the context \(right\-click\) menu, and choose **Export variables** under **Substitution variables**\.

1. Enter the name of the comma\-separated values \(CSV\) file to save the substitution variables and choose **Save**\.

1. Open this CSV file and fill in the values for the substitution variables\.

   Depending on the operating system, AWS SCT uses different formats for CSV files\. The values in the file might be either enclosed in quotation marks or not\. Make sure that you use the same format for the values of substitution variables as the other values in the file\. AWS SCT can't import the CSV file with values in different formats\.

1. Save the CSV file\.

1. In the left panel, expand the **Scripts** node\. Choose **FastExport**, and then choose your script\. Open the context \(right\-click\) menu, and then choose **Import variables** under **Substitution variables**\.

1. Choose your CSV file, and then choose **Open**\.

1. Choose **Variables** to view all discovered substitution variables and their values\.

## Converting Teradata FastExport job scripts with AWS SCT<a name="CHAP-converting-fastexport-rsql-convert"></a>

Following, find how to convert Teradata FastExport job to Amazon Redshift RSQL using AWS SCT\. 

**To convert a Teradata FastExport job script to Amazon Redshift RSQL**

1. Add your FastExport job scripts to your AWS SCT project\. For more information, see [Adding FastExport job scripts to your AWS SCT project](#CHAP-converting-fastexport-rsql-create)\.

1. Configure the substitution variables\. For more information, see [Configuring substitution variables in FastExport job scripts](#CHAP-converting-fastexport-rsql-variables)\.

1. In the left panel, expand the **Scripts** node\.

1. Do one of the following:
   + To convert a single FastExport job script, expand the **FastExport** node, choose the script to convert, and then choose **Convert script** from the context \(right\-click\) menu\.
   + To covert multiple scripts, make sure that you select all scripts to convert\. Then choose **FastExport**, open the context \(right\-click\) menu, and then choose **Convert script**\. 

   AWS SCT converts all your selected Teradata FastExport job scripts to a format compatible with Amazon Redshift RSQL\. Find your converted scripts in the **Scripts** node in the target database panel\.

1. Edit your converted Amazon Redshift RSQL scripts or save them\. For more information, see [Editing and saving your converted FastExport job scripts](#CHAP-converting-fastexport-rsql-save)\.

## Managing Teradata FastExport job scripts with AWS SCT<a name="CHAP-converting-fastexport-rsql-manage"></a>

You can add multiple Teradata FastExport job scripts or remove a FastExport job script from your AWS SCT project\.

**To add a new FastExport job script to your AWS SCT project**

1. Expand the **Scripts** node in the left panel\.

1. Choose the **FastExport** node, and open the context \(right\-click\) menu\.

1. Choose **Load scripts**\.

1. Enter the information that is required to add a new FastExport job script and configure substitution variables\. For more information, see [Adding FastExport job scripts to your AWS SCT project](#CHAP-converting-fastexport-rsql-create) and [Configuring substitution variables in FastExport job scripts](#CHAP-converting-fastexport-rsql-variables)\.

**To remove a FastExport job script from your AWS SCT project**

1. Expand the **FastExport** node under **Scripts** in the left panel\.

1. Choose the script to remove, and open the context \(right\-click\) menu\.

1. Choose **Delete script**\.

## Creating an assessment report for a Teradata FastExport job script conversion with AWS SCT<a name="CHAP-converting-fastexport-rsql-assessment"></a>

The *FastExport job script conversion assessment report* provides information about converting the FastExport commands and SQL statements from your FastExport scripts to a format compatible with Amazon Redshift RSQL\. The assessment report includes action items for FastExport commands and SQL statements that AWS SCT can't convert\. 

**To create a script conversion assessment report for a Teradata FastExport job**

1. Expand the **FastExport** node under **Scripts** in the left panel\.

1. Choose the script to convert, open the context \(right\-click\) menu, and then choose **Create report**\.

1. View the **Summary** tab\. The **Summary** tab displays the executive summary information from the FastExport job script assessment report\. It includes conversion results for all FastExport commands and SQL statements from your source scripts\. 

1. You can save a local copy of the FastExport job script conversion assessment report as either a PDF file or a comma\-separated values \(CSV\) file\.

   1. To save the FastExport job script conversion assessment report as a PDF file, choose **Save to PDF** at upper right\.

       The PDF file contains the executive summary, action items, and recommendations for scripts conversion\.

   1. To save the FastExport job script conversion assessment report as a CSV file, choose **Save to CSV ** at upper right\.

      The CSV file contains action items, recommended actions, and an estimated complexity of manual effort required to convert the scripts\.

1. Choose the **Action items** tab\. This tab contains a list of items that require manual conversion to Amazon Redshift RSQL\. When you select an action item from the list, AWS SCT highlights the item from your source FastExport job script that the action item applies to\. 

## Editing and saving your converted Teradata FastExport job scripts with AWS SCT<a name="CHAP-converting-fastexport-rsql-save"></a>

You can edit your converted scripts in the lower panel of your AWS SCT project\. AWS SCT stores the edited script as part of your project\.

**To save your converted scripts**

1. Expand the **RSQL scripts** node under **Scripts** in the target database panel\.

1. Choose your converted script, open the context \(right\-click\) menu, and choose **Save script**\.

1. Enter the path to the folder to save the converted script and choose **Save**\.

   AWS SCT saves the converted script to a file and opens this file\.