# Converting Dynamic SQL for Oracle to PostgreSQL Migrations<a name="CHAP_Converting.DynamicSQL"></a>

Dynamic SQL is a programming technique that you can use to run data definition language \(DDL\) statements inside PL/SQL code\. You can also use dynamic SQL to generate and run SQL statements at run time when you don't know the exact text or object identifiers during development\. AWS SCT can convert dynamic SQL statements used with Oracle databases to their analog statements in PostgreSQL\.

**To convert Oracle dynamic SQL to PostgreSQL SQL**

1. Create an Oracle\-to\-PostgreSQL migration project\.

1. Connect to the source and target databases\.

1. Choose a stored procedure in the Oracle source tree view\. The procedure should contain references to the DBMS\_SQL Oracle package or have an EXECUTE IMMEDIATE statement\.

1. For **Actions**, choose **Convert Schema**, and agree to replace the objects if they exist\. The following screenshot shows the converted procedure below the Oracle procedure\.  
![\[Dynamic SQL conversion\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/dynamicsql1.png)