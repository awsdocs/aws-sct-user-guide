# Using Db2 LUW as a Source for AWS Schema Conversion Tool \(AWS SCT\)<a name="CHAP_Source.DB2LUW"></a>

You can use AWS SCT to convert data from Db2 LUW to the following targets\. AWS SCT supports as a source Db2 LUW versions 9\.1, 9\.5, 9\.7, 10\.1, 10\.5, and 11\.1\.
+ Amazon RDS for MySQL
+  Amazon Aurora \(MySQL\)
+ Amazon RDS for PostgreSQL
+ Amazon Aurora \(PostgreSQL\)

## Permissions Needed When Using Db2 LUW as a Source<a name="CHAP_Source.DB2LUW.Permissions"></a>

The privileges needed to connect to a DB2LUW database, to check available privileges and read schema metadata for a source are listed following: 
+ Privilege needed to establish a connection:

  GRANT CONNECT ON DATABASE TO USER min\_privs;
+ Privilege needed to run SQL statements:

  GRANT EXECUTE ON PACKAGE NULLID\.SYSSH200 TO USER MIN\_PRIVS;
+ Privileges needed to get instance\-level information:
  + GRANT EXECUTE ON FUNCTION SYSPROC\.ENV\_GET\_INST\_INFO TO USER MIN\_PRIVS;
  + GRANT SELECT ON SYSIBMADM\.ENV\_INST\_INFO TO USER MIN\_PRIVS;
  + GRANT SELECT ON SYSIBMADM\.ENV\_SYS\_INFO TO USER MIN\_PRIVS;
+ Privileges needed to check privileges granted through roles, groups and authorities:
  + GRANT EXECUTE ON FUNCTION SYSPROC\.AUTH\_LIST\_AUTHORITIES\_FOR\_AUTHID TO USER MIN\_PRIVS;
  + GRANT EXECUTE ON FUNCTION SYSPROC\.AUTH\_LIST\_GROUPS\_FOR\_AUTHID TO USER MIN\_PRIVS;
  + GRANT EXECUTE ON FUNCTION SYSPROC\.AUTH\_LIST\_ROLES\_FOR\_AUTHID TO USER MIN\_PRIVS;
  + GRANT SELECT ON SYSIBMADM\.PRIVILEGES TO USER MIN\_PRIVS;
+ Privileges needed on system catalogs and tables:
  + GRANT SELECT ON SYSCAT\.ATTRIBUTES TO USER MIN\_PRIVS;
  + GRANT SELECT ON SYSCAT\.CHECKS TO USER MIN\_PRIVS;
  + GRANT SELECT ON SYSCAT\.COLIDENTATTRIBUTES TO USER MIN\_PRIVS;
  + GRANT SELECT ON SYSCAT\.COLUMNS TO USER MIN\_PRIVS;
  + GRANT SELECT ON SYSCAT\.DATAPARTITIONEXPRESSION TO USER MIN\_PRIVS;
  + GRANT SELECT ON SYSCAT\.DATAPARTITIONS TO USER MIN\_PRIVS;
  + GRANT SELECT ON SYSCAT\.DATATYPEDEP TO USER MIN\_PRIVS;
  + GRANT SELECT ON SYSCAT\.DATATYPES TO USER MIN\_PRIVS;
  + GRANT SELECT ON SYSCAT\.HIERARCHIES TO USER MIN\_PRIVS;
  + GRANT SELECT ON SYSCAT\.INDEXCOLUSE TO USER MIN\_PRIVS;
  + GRANT SELECT ON SYSCAT\.INDEXES TO USER MIN\_PRIVS;
  + GRANT SELECT ON SYSCAT\.INDEXPARTITIONS TO USER MIN\_PRIVS;
  + GRANT SELECT ON SYSCAT\.KEYCOLUSE TO USER MIN\_PRIVS;
  + GRANT SELECT ON SYSCAT\.MODULEOBJECTS TO USER MIN\_PRIVS;
  + GRANT SELECT ON SYSCAT\.MODULES TO USER MIN\_PRIVS;
  + GRANT SELECT ON SYSCAT\.NICKNAMES TO USER MIN\_PRIVS;
  + GRANT SELECT ON SYSCAT\.PERIODS TO USER MIN\_PRIVS;
  + GRANT SELECT ON SYSCAT\.REFERENCES TO USER MIN\_PRIVS;
  + GRANT SELECT ON SYSCAT\.ROUTINEPARMS TO USER MIN\_PRIVS;
  + GRANT SELECT ON SYSCAT\.ROUTINES TO USER MIN\_PRIVS;
  + GRANT SELECT ON SYSCAT\.ROWFIELDS TO USER MIN\_PRIVS;
  + GRANT SELECT ON SYSCAT\.SCHEMATA TO USER MIN\_PRIVS;
  + GRANT SELECT ON SYSCAT\.SEQUENCES TO USER MIN\_PRIVS;
  + GRANT SELECT ON SYSCAT\.TABCONST TO USER MIN\_PRIVS;
  + GRANT SELECT ON SYSCAT\.TABLES TO USER MIN\_PRIVS;
  + GRANT SELECT ON SYSCAT\.TRIGGERS TO USER MIN\_PRIVS;
  + GRANT SELECT ON SYSCAT\.VARIABLEDEP TO USER MIN\_PRIVS;
  + GRANT SELECT ON SYSCAT\.VARIABLES TO USER MIN\_PRIVS;
  + GRANT SELECT ON SYSCAT\.VIEWS TO USER MIN\_PRIVS;
  + GRANT SELECT ON SYSIBM\.SYSDUMMY1 TO USER MIN\_PRIVS;
+  To run SQL statements, the user account needs a privilege to use at least one of the workloads enabled in the database\. If none of the workloads are assigned to the user, ensure that the default user workload is accessible to the user:

  GRANT USAGE ON WORKLOAD SYSDEFAULTUSERWORKLOAD TO USER MIN\_PRIVS;

To execute queries, you need to create system temporary tablespace with page size 8K, 16K and 32K, if they don't exist\. To create the temporary tablespaces, run the following scripts:

```
CREATE BUFFERPOOL BP8K
  IMMEDIATE
  ALL DBPARTITIONNUMS
  SIZE AUTOMATIC
  NUMBLOCKPAGES 0
  PAGESIZE 8K;
  
CREATE SYSTEM TEMPORARY TABLESPACE TS_SYS_TEMP_8K 
  PAGESIZE 8192 
  BUFFERPOOL BP8K;
  
CREATE BUFFERPOOL BP16K
  IMMEDIATE
  ALL DBPARTITIONNUMS
  SIZE AUTOMATIC
  NUMBLOCKPAGES 0
  PAGESIZE 16K;
  
CREATE SYSTEM TEMPORARY TABLESPACE TS_SYS_TEMP_BP16K 
  PAGESIZE 16384 
  BUFFERPOOL BP16K;  
  
CREATE BUFFERPOOL BP32K
  IMMEDIATE
  ALL DBPARTITIONNUMS
  SIZE AUTOMATIC
  NUMBLOCKPAGES 0
  PAGESIZE 32K;
  
CREATE SYSTEM TEMPORARY TABLESPACE TS_SYS_TEMP_BP32K 
  PAGESIZE 32768 
  BUFFERPOOL BP32K;
```

## Connecting to a Db2 LUW Source<a name="CHAP_Source.DB2LUW.Connecting"></a>

Use the following procedure to connect to your Db2 LUW source database with the AWS Schema Conversion Tool \(AWS SCT\)\. 

**To connect to a Db2 LUW source database**

1. In the AWS Schema Conversion Tool, choose **Connect to Source DB2 LUW**\.   
![\[Connect to source database\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/file_connect_to_db2luw.png)

   The **Connect to DB2 LUW** dialog box appears\.  
![\[Db2 LUW connection information\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/source-db2luw.png)

1. Provide the Db2 LUW source database connection information\. Use the instructions in the following table\.   
****    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/CHAP_Source.DB2LUW.html)

1. Choose **Test Connection** to verify that you can successfully connect to your source database\. 

1. Choose **OK** to connect to your source database\.