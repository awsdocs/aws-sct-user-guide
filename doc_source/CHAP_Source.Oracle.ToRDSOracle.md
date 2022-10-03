# Converting Oracle to Amazon RDS for Oracle<a name="CHAP_Source.Oracle.ToRDSOracle"></a>

Some things to consider when migrating Oracle schema and code to Amazon RDS for Oracle: 
+ AWS SCT can add directory objects to the object tree\. *Directory objects* are logical structures that each represent a physical directory on the server's file system\. You can use directory objects with packages such as DBMS\_LOB, UTL\_FILE, DBMS\_FILE\_TRANSFER, the DATAPUMP utility, and so on\.
+ AWS SCT supports converting Oracle tablespaces to an Amazon RDS for Oracle DB instance\. Oracle stores data logically in tablespaces and physically in data files associated with the corresponding tablespace\. In Oracle, you can create a tablespace with data file names\. Amazon RDS supports Oracle Managed Files \(OMF\) for data files, log files, and control files only\. AWS SCT creates the needed data files during conversion\.
+ AWS SCT can convert server\-level roles and privileges\. The Oracle database engine uses role\-based security\. A role is a collection of privileges that you can grant to or revoke from a user\. A predefined role in Amazon RDS, called DBA, normally allows all administrative privileges on an Oracle database engine\. The following privileges are not available for the DBA role on an Amazon RDS DB instance using the Oracle engine:
  + Alter database
  + Alter system
  + Create any directory
  + Grant any privilege
  + Grant any role
  + Create external job

  You can grant all other privileges to an Amazon RDS for Oracle user role, including advanced filtering and column privileges\.
+ AWS SCT supports converting Oracle jobs into jobs that can run on Amazon RDS for Oracle\. There are a few limitations to the conversion, including the following:
  + Executable jobs are not supported\.
  + Schedule jobs that use the ANYDATA data type as an argument are not supported\.
+ Oracle Real Application Clusters \(RAC\) One Node is an option to the Oracle Database Enterprise Edition that was introduced with Oracle Database 11g Release 2\. Amazon RDS for Oracle doesn’t support the RAC feature\. For high availability, use Amazon RDS Multi\-AZ\. 

  In a Multi\-AZ deployment, Amazon RDS automatically provisions and maintains a synchronous standby replica in a different Availability Zone\. The primary DB instance is synchronously replicated across Availability Zones to a standby replica\. This functionality provides data redundancy, eliminates I/O freezes, and minimizes latency spikes during system backups\.
+ Oracle Spatial provides a SQL schema and functions that facilitate the storage, retrieval, update, and query of collections of spatial data in an Oracle database\. Oracle Locator provides capabilities that are typically required to support internet and wireless service\-based applications and partner\-based GIS solutions\. Oracle Locator is a limited subset of Oracle Spatial\.

  To use Oracle Spatial and Oracle Locator features, add the SPATIAL option or LOCATOR option \(mutually exclusive\) to the option group of your DB instance\.

  There are some prerequisites to using Oracle Spatial and Oracle Locator on an Amazon RDS for Oracle DB instance:
  + The instance should use Oracle Enterprise Edition version 12\.1\.0\.2\.v6 or later, or 11\.2\.0\.4\.v10 or later\.
  + The instance should be inside a virtual private cloud \(VPC\)\.
  + The instance should the DB instance class that can support the Oracle feature\. For example, Oracle Spatial is not supported for the db\.m1\.small, db\.t1\.micro, db\.t2\.micro, or db\.t2\.small DB instance classes\. For more information, see [DB instance class support for Oracle](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_Oracle.html#Oracle.Concepts.InstanceClasses)\.
  + The instance must have the Auto Minor Version Upgrade option enabled\. Amazon RDS updates your DB instance to the latest Oracle PSU if there are security vulnerabilities with a CVSS score of 9\+ or other announced security vulnerabilities\. For more information, see 

    [Settings for Oracle DB instances](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_ModifyInstance.Oracle.html#USER_ModifyInstance.Oracle.Settings)\.
  + If your DB instance is version 11\.2\.0\.4\.v10 or later, you must install the XMLDB option\. For more information, see

    [Oracle XML DB](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Appendix.Oracle.Options.XMLDB.html)\.
  + You should have an Oracle Spatial license from Oracle\. For more information, see [Oracle Spatial and Graph](https://shop.oracle.com/apex/product?p1=OracleSpatialandGraph) in the Oracle documentation\.
+ Data Guard is included with Oracle Database Enterprise Edition\. For high availability, use Amazon RDS Multi\-AZ feature\. 

  In a Multi\-AZ deployment, Amazon RDS automatically provisions and maintains a synchronous standby replica in a different Availability Zone\. The primary DB instance is synchronously replicated across Availability Zones to a standby replica\. This functionality provides data redundancy, eliminates I/O freezes, and minimizes latency spikes during system backups\.
+ AWS SCT supports converting Oracle DBMS\_SCHEDULER objects when migrating to Amazon RDS for Oracle\. The AWS SCT assessment report indicates if a schedule object can be converted\. For more information on using schedule objects with Amazon RDS, see the [Amazon RDS documentation](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Appendix.Oracle.CommonDBATasks.System.html#Appendix.Oracle.CommonDBATasks.ModifyScheduler)\.
+ For Oracle to Amazon RDS for Oracle conversions, DB Links is supported\. A database link is a schema object in one database that enables you to access objects on another database\. The other database doesn’t need to be an Oracle database\. However, to access non\-Oracle databases you must use Oracle Heterogeneous Services\.

  Once you create a database link, you can use the link in SQL statements to refer to tables, views, and PL/SQL objects in the other database\. To use a database link, append `@dblink` to the table, view, or PL/SQL object name\. You can query a table or view in the other database with the SELECT statement\. For more information about using Oracle database links, see the [Oracle documentation](https://docs.oracle.com/cd/B28359_01/server.111/b28310/ds_concepts002.htm#ADMIN12083)\.

  For more information about using database links with Amazon RDS, see the [Amazon RDS documentation](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Appendix.Oracle.CommonDBATasks.Database.html#Appendix.Oracle.CommonDBATasks.DBLinks)\.
+ The AWS SCT assessment report provides server metrics for the conversion\. These metrics about your Oracle instance include the following:
  + Computation and memory capacity of the target DB instance\.
  + Unsupported Oracle features such as Real Application Clusters that Amazon RDS doesn't support\.
  + Disk read\-write load
  + Average total disk throughput
  + Server information such as server name, OS, host name, and character set\.

## Privileges for RDS for Oracle as a target<a name="CHAP_Source.Oracle.ToRDSOracle.ConfigureTarget"></a>

To migrate to Amazon RDS for Oracle, create a privileged database user\. You can use the following code example\.

```
CREATE USER user_name IDENTIFIED BY your_password;

-- System privileges
GRANT DROP ANY CUBE BUILD PROCESS TO user_name;
GRANT ALTER ANY CUBE TO user_name;
GRANT CREATE ANY CUBE DIMENSION TO user_name;
GRANT CREATE ANY ASSEMBLY TO user_name;
GRANT ALTER ANY RULE TO user_name;
GRANT SELECT ANY DICTIONARY TO user_name;
GRANT ALTER ANY DIMENSION TO user_name;
GRANT CREATE ANY DIMENSION TO user_name;
GRANT ALTER ANY TYPE TO user_name;
GRANT DROP ANY TRIGGER TO user_name;
GRANT CREATE ANY VIEW TO user_name;
GRANT ALTER ANY CUBE BUILD PROCESS TO user_name;
GRANT CREATE ANY CREDENTIAL TO user_name;
GRANT DROP ANY CUBE DIMENSION TO user_name;
GRANT DROP ANY ASSEMBLY TO user_name;
GRANT DROP ANY PROCEDURE TO user_name;
GRANT ALTER ANY PROCEDURE TO user_name;
GRANT ALTER ANY SQL TRANSLATION PROFILE TO user_name;
GRANT DROP ANY MEASURE FOLDER TO user_name;
GRANT CREATE ANY MEASURE FOLDER TO user_name;
GRANT DROP ANY CUBE TO user_name;
GRANT DROP ANY MINING MODEL TO user_name;
GRANT CREATE ANY MINING MODEL TO user_name;
GRANT DROP ANY EDITION TO user_name;
GRANT CREATE ANY EVALUATION CONTEXT TO user_name;
GRANT DROP ANY DIMENSION TO user_name;
GRANT ALTER ANY INDEXTYPE TO user_name;
GRANT DROP ANY TYPE TO user_name;
GRANT CREATE ANY PROCEDURE TO user_name;
GRANT CREATE ANY SQL TRANSLATION PROFILE TO user_name;
GRANT CREATE ANY CUBE TO user_name;
GRANT COMMENT ANY MINING MODEL TO user_name;
GRANT ALTER ANY MINING MODEL TO user_name;
GRANT DROP ANY SQL PROFILE TO user_name;
GRANT CREATE ANY JOB TO user_name;
GRANT DROP ANY EVALUATION CONTEXT TO user_name;
GRANT ALTER ANY EVALUATION CONTEXT TO user_name;
GRANT CREATE ANY INDEXTYPE TO user_name;
GRANT CREATE ANY OPERATOR TO user_name;
GRANT CREATE ANY TRIGGER TO user_name;
GRANT DROP ANY ROLE TO user_name;
GRANT DROP ANY SEQUENCE TO user_name;
GRANT DROP ANY CLUSTER TO user_name;
GRANT DROP ANY SQL TRANSLATION PROFILE TO user_name;
GRANT ALTER ANY ASSEMBLY TO user_name;
GRANT CREATE ANY RULE SET TO user_name;
GRANT ALTER ANY OUTLINE TO user_name;
GRANT UNDER ANY TYPE TO user_name;
GRANT CREATE ANY TYPE TO user_name;
GRANT DROP ANY MATERIALIZED VIEW TO user_name;
GRANT ALTER ANY ROLE TO user_name;
GRANT DROP ANY VIEW TO user_name;
GRANT ALTER ANY INDEX TO user_name;
GRANT COMMENT ANY TABLE TO user_name;
GRANT CREATE ANY TABLE TO user_name;
GRANT CREATE USER TO user_name;
GRANT DROP ANY RULE SET TO user_name;
GRANT CREATE ANY CONTEXT TO user_name;
GRANT DROP ANY INDEXTYPE TO user_name;
GRANT ALTER ANY OPERATOR TO user_name;
GRANT CREATE ANY MATERIALIZED VIEW TO user_name;
GRANT ALTER ANY SEQUENCE TO user_name;
GRANT DROP ANY SYNONYM TO user_name;
GRANT CREATE ANY SYNONYM TO user_name;
GRANT DROP USER TO user_name;
GRANT ALTER ANY MEASURE FOLDER TO user_name;
GRANT ALTER ANY EDITION TO user_name;
GRANT DROP ANY RULE TO user_name;
GRANT CREATE ANY RULE TO user_name;
GRANT ALTER ANY RULE SET TO user_name;
GRANT CREATE ANY OUTLINE TO user_name;
GRANT UNDER ANY TABLE TO user_name;
GRANT UNDER ANY VIEW TO user_name;
GRANT DROP ANY DIRECTORY TO user_name;
GRANT ALTER ANY CLUSTER TO user_name;
GRANT CREATE ANY CLUSTER TO user_name;
GRANT ALTER ANY TABLE TO user_name;
GRANT CREATE ANY CUBE BUILD PROCESS TO user_name;
GRANT ALTER ANY CUBE DIMENSION TO user_name;
GRANT CREATE ANY EDITION TO user_name;
GRANT CREATE ANY SQL PROFILE TO user_name;
GRANT ALTER ANY SQL PROFILE TO user_name;
GRANT DROP ANY OUTLINE TO user_name;
GRANT DROP ANY CONTEXT TO user_name;
GRANT DROP ANY OPERATOR TO user_name;
GRANT DROP ANY LIBRARY TO user_name;
GRANT ALTER ANY LIBRARY TO user_name;
GRANT CREATE ANY LIBRARY TO user_name;
GRANT ALTER ANY MATERIALIZED VIEW TO user_name;
GRANT ALTER ANY TRIGGER TO user_name;
GRANT CREATE ANY SEQUENCE TO user_name;
GRANT DROP ANY INDEX TO user_name;
GRANT CREATE ANY INDEX TO user_name;
GRANT DROP ANY TABLE TO user_name;
GRANT SELECT_CATALOG_ROLE TO user_name;
GRANT SELECT ANY SEQUENCE TO user_name;

-- Database Links
GRANT CREATE DATABASE LINK TO user_name;
GRANT CREATE PUBLIC DATABASE LINK TO user_name;
GRANT DROP PUBLIC DATABASE LINK TO user_name;


-- Server Level Objects (directory)
GRANT CREATE ANY DIRECTORY TO user_name;
GRANT DROP ANY DIRECTORY TO user_name;
-- (for RDS only)
GRANT EXECUTE ON RDSADMIN.RDSADMIN_UTIL TO user_name;

-- Server Level Objects (tablespace)
GRANT CREATE TABLESPACE TO user_name;
GRANT DROP TABLESPACE TO user_name;

-- Server Level Objects (user roles)
/* (grant source privileges with admin option or convert roles/privs as DBA) */

-- Queues
grant execute on DBMS_AQADM to user_name;
grant aq_administrator_role to user_name;

-- for Materialized View Logs creation
GRANT SELECT ANY TABLE TO user_name;

-- Roles
GRANT RESOURCE TO user_name;
GRANT CONNECT TO user_name;
```

In the example preceding, replace *user\_name* with the name of your user\. Then, replace *your\_password* with a secure password\.

## Limitations when converting Oracle to Amazon RDS for Oracle<a name="CHAP_Source.Oracle.ToRDSOracle.Limitations"></a>

Some limitations you should consider when migrating Oracle schema and code to Amazon RDS for Oracle: 
+  A predefined role in Amazon RDS, called DBA, normally allows all administrative privileges on an Oracle database engine\. The following privileges are not available for the DBA role on an Amazon RDS DB instance using the Oracle engine:
  + Alter database
  + Alter system
  + Create any directory
  + Grant any privilege
  + Grant any role
  + Create external job

  You can grant all other privileges to an Oracle RDS user role\.
+ Amazon RDS for Oracle supports traditional auditing, fine\-grained auditing using the DBMS\_FGA package, and Oracle Unified Auditing\.
+ Amazon RDS for Oracle doesn’t support change data capture \(CDC\)\. To do CDC during and after a database migration, use AWS Database Migration Service\.