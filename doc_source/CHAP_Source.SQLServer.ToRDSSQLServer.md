# Converting SQL Server to Amazon RDS for SQL Server<a name="CHAP_Source.SQLServer.ToRDSSQLServer"></a>

Some things to consider when migrating SQL Server schema and code to Amazon RDS for SQL Server: 
+  AWS SCT can convert SQL Server Agent to provide schedules, alerts, and jobs on an Amazon RDS for SQL Server DB instance\. After conversion, you can use an Amazon RDS for SQL Server DB instance as a data source for SQL Server Reporting Service \(SSRS\), SQL Server Analysis Services \(SSAS\), and SQL Server Integration Services \(SSIS\)\. You can’t run these services on the DB instance\.
+ Amazon RDS currently doesn’t support SQL Server Service Broker or additional T\-SQL endpoints that require you to run the CREATE ENDPOINT command\.
+ Amazon RDS has limited support for linked servers\. When converting SQL Server application code that uses linked servers, AWS SCT converts the application code but you should review the behavior of objects that use link servers before you run the converted code\.
+ The AWS SCT assessment report provides server metrics for the conversion\. These metrics about your SQL Server instance include the following:
  + Data mirroring is used\.
  + SQL Server Log Shipping is configured\.
  + AlwaysON is used\. Amazon RDS does not support Always On\.
  + Failover cluster is used\.
  + Database Mail is configured\. Amazon RDS does not support Database Mail\.
  + SQL Server Reporting Service \(SSRS\) is used\. Amazon RDS doesn't support SSRS so we recommend that you install SQL Server on an Amazon EC2 instance\.
  + SQL Server Analysis Services \(SSAS\) is used\. Amazon RDS doesn't support SSAS so we recommend that you install SQL Server on an Amazon EC2 instance\.
  + SQL Server Integration Services \(SSIS\) is used\. Amazon RDS doesn't support SSIS so we recommend that you install SQL Server on an Amazon EC2 instance\.
  + Full Text Search Service is used\. Amazon RDS for SQL Server has a limited full text search, and it does not support semantic search\.
  + Data Quality Service \(DQS\) is installed\. Amazon RDS doesn't support DQS so we recommend that you install SQL Server on an Amazon EC2 instance\.