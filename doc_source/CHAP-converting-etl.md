# Converting extract, transform, and load \(ETL\) processes with AWS Schema Conversion Tool<a name="CHAP-converting-etl"></a>

You can use the AWS Schema Conversion Tool \(AWS SCT\) to migrate extract, transform, and load \(ETL\) processes\. This type of migration includes the conversion of ETL\-related business logic\. This logic can reside either inside your source data warehouses or in external scripts that you run separately\. 

Currently, AWS SCT supports the conversion of ETL scripts to objects to AWS Glue and Amazon Redshift RSQL, as shown in the following table\.


****  

| Source | Target | 
| --- | --- | 
| Microsoft SQL Server Integration Services \(SSIS\) ETL packages | AWS Glue or AWS Glue Studio | 
| Microsoft SQL Server stored database code objects | AWS Glue | 
| Oracle stored database code objects | AWS Glue | 
| Shell scripts with embedded commands from Teradata Basic Teradata Query \(BTEQ\)  | Amazon Redshift RSQL | 
| Teradata BTEQ ETL scripts | AWS Glue or Amazon Redshift RSQL | 
| Teradata FastExport job scripts | Amazon Redshift RSQL | 
| Teradata FastLoad job scripts | Amazon Redshift RSQL | 
| Teradata MultiLoad job scripts | Amazon Redshift RSQL | 
| Teradata stored database code objects | AWS Glue | 

**Topics**
+ [Converting ETL processes to AWS Glue with AWS SCT](CHAP-converting-aws-glue-ui-process.md)
+ [Converting ETL processes using the Python API for AWS Glue with AWS SCT](CHAP-converting-aws-glue-api-process.md)
+ [Converting SSIS to AWS Glue with AWS SCT](CHAP-converting-aws-glue-ssis.md)
+ [Converting SSIS to AWS Glue Studio with AWS SCT](CHAP-converting-ssis-glue-studio.md)
+ [Converting Teradata BTEQ scripts to Amazon Redshift RSQL with AWS SCT](CHAP-converting-bteq-rsql.md)
+ [Converting shell scripts with embedded Teradata BTEQ commands to Amazon Redshift RSQL with AWS SCT](CHAP-converting-shell-rsql.md)
+ [Converting Teradata FastExport job scripts to Amazon Redshift RSQL with AWS SCT](CHAP-converting-fastexport-rsql.md)
+ [Converting Teradata FastLoad job scripts to Amazon Redshift RSQL with AWS SCT](CHAP-converting-fastload-rsql.md)
+ [Converting Teradata MultiLoad job scripts to Amazon Redshift RSQL with AWS SCT](CHAP-converting-multiload-rsql.md)