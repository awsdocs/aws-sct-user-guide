# Source Databases for the AWS Schema Conversion Tool<a name="CHAP_Source"></a>

AWS Schema Conversion Tool \(AWS SCT\) can convert the following source database schemas to a target database\. Select the link below for information on permissions required, connection information, and information on what AWS SCT can convert for use with the target database\.

**Topics**
+ [Using Oracle as a Source for AWS Schema Conversion Tool \(AWS SCT\)](CHAP_Source.Oracle.md)
+ [Using Microsoft SQL Server as a Source for AWS Schema Conversion Tool \(AWS SCT\)](CHAP_Source.SQLServer.md)
+ [Using MySQL as a Source for AWS Schema Conversion Tool \(AWS SCT\)](CHAP_Source.MySQL.md)
+ [Using PostgreSQL as a Source for AWS Schema Conversion Tool \(AWS SCT\)](CHAP_Source.PostgreSQL.md)
+ [Using Db2 LUW as a Source for AWS Schema Conversion Tool \(AWS SCT\)](CHAP_Source.DB2LUW.md)
+ [Using Amazon Redshift as a Source for AWS Schema Conversion Tool \(AWS SCT\)](#CHAP_Source.Redshift)
+ [Using Oracle DW as a Source for AWS Schema Conversion Tool \(AWS SCT\)](#CHAP_Source.OracleDW)
+ [Using Teradata as a Source for AWS Schema Conversion Tool \(AWS SCT\)](#CHAP_Source.Teradata)
+ [Using Netezza as a Source for AWS Schema Conversion Tool \(AWS SCT\)](#CHAP_Source.Netezza)
+ [Using Greenplum as a Source for AWS Schema Conversion Tool \(AWS SCT\)](#CHAP_Source.Greenplum)
+ [Using Vertica as a Source for AWS Schema Conversion Tool \(AWS SCT\)](#CHAP_Source.Vertica)
+ [Using Microsoft SQL Server DW as a Source for AWS Schema Conversion Tool \(AWS SCT\)](#CHAP_Source.SQLServerDW)

## Using Amazon Redshift as a Source for AWS Schema Conversion Tool \(AWS SCT\)<a name="CHAP_Source.Redshift"></a>

You can use AWS SCT to convert data from Amazon Redshift to the following targets: 
+ Amazon Redshift

### Privileges for Amazon Redshift as a Source Database<a name="CHAP_Source.Redshift.Permissions"></a>

The privileges required for using Amazon Redshift as a source are listed following: 
+ USAGE ON SCHEMA *<schema\_name>* 
+ SELECT ON ALL TABLES IN SCHEMA *<schema\_name>* 
+ SELECT ON PG\_CATALOG\.PG\_STATISTIC 
+ SELECT ON SVV\_TABLE\_INFO 
+ SELECT ON TABLE STV\_BLOCKLIST 
+ SELECT ON TABLE STV\_TBL\_PERM 

### Connecting to Redshift as a Source<a name="CHAP_Source.Redshift.Connecting"></a>

Use the following procedure to connect to your Amazon Redshift source database with the AWS Schema Conversion Tool \(AWS SCT\)\. 

**To connect to an Amazon Redshift source database**

1. In the AWS Schema Conversion Tool, choose **Connect to Source Amazon Redshift**\.   
![\[Connect to source database\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/file_connect_to_redshift.png)

   The **Connect to Amazon Redshift** dialog box appears\.  
![\[Redshift connection information\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/source-redshift.png)

1. Provide the Amazon Redshift source database connection information\. Use the instructions in the following table\.   
****    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/CHAP_Source.html)

1. Choose **Test Connection** to verify that you can successfully connect to your source database\. 

1. Choose **OK** to connect to your source database\.

## Using Oracle DW as a Source for AWS Schema Conversion Tool \(AWS SCT\)<a name="CHAP_Source.OracleDW"></a>

You can use AWS SCT to convert data from Oracle DW to Amazon Redshift\. 

connecting to source, connecting to target, reference info, permissions

### Privileges for Oracle Data Warehouse as a Source<a name="CHAP_Source.OracleDW.Permissions"></a>

The privileges required for Oracle Data Warehouse as a source are listed following: 
+ connect 
+ select\_catalog\_role 
+ select any dictionary 

### Connecting to OracleDW as a Source<a name="CHAP_Source.OracleDW.Connecting"></a>

Use the following procedure to connect to your Oracle data warehouse source database with the AWS Schema Conversion Tool \(AWS SCT\)\. 

**To connect to an Oracle data warehouse source database**

1. In the AWS Schema Conversion Tool, choose **Connect to Oracle DW**\.   
![\[Connect to source database\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/file_connect_to_oracle_DW.png)

   The **Connect to Oracle** dialog box appears\.  
![\[Oracle connection information\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/source-oracle.png)

1. Provide the Oracle Data Warehouse source database connection information\. Use the instructions in the following table\.   
****    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/CHAP_Source.html)

1. Choose **Test Connection** to verify that you can successfully connect to your source database\. 

1. Choose **OK** to connect to your source database\.

## Using Teradata as a Source for AWS Schema Conversion Tool \(AWS SCT\)<a name="CHAP_Source.Teradata"></a>

You can use AWS SCT to convert data from Teradata to Amazon Redshift\. 

### Privileges for Teradata as a Source<a name="CHAP_Source.Teradata.Permissions"></a>

The privileges required for Teradata as a source are listed following: 
+ SELECT ON DBC 

### Connecting to Teradata as a Source<a name="CHAP_Source.Teradata.Connecting"></a>

Use the following procedure to connect to your Teradata source database with the AWS Schema Conversion Tool \(AWS SCT\)\. 

**To connect to a Teradata source database**

1. In the AWS Schema Conversion Tool, choose **Connect to Teradata**\.   
![\[Connect to source database\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/file_connect_to_teradata.png)

   The **Connect to Teradata** dialog box appears\.  
![\[Teradata connection information\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/source-teradata.png)

1. Provide the Teradata source database connection information\. Use the instructions in the following table\.   
****    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/CHAP_Source.html)

1. Choose **Test Connection** to verify that you can successfully connect to your source database\. 

1. Choose **OK** to connect to your source database\.

#### Using LDAP Authentication with a Teradata Source<a name="CHAP_Source.Teradata.Connecting.LDAP"></a>

To set up Lightweight Directory Access Protocol \(LDAP\) authentication for Teradata users who run Microsoft Active Directory in Windows, use the following procedure\. 

In the procedure examples, the Active Directory domain is `test.local.com`\. The Windows server is `DC`, and it is configured with default settings\. The user account created in Active Directory is `test_ldap`, and the account uses the password `test_ldap`\.

1. In the `/opt/teradata/tdat/tdgss/site` directory, edit the file `TdgssUserConfigFile.xml` \. Change the LDAP section to the following\.

   ```
   AuthorizationSupported="no"
   
   LdapServerName="DC.test.local.com"
   LdapServerPort="389"
   LdapServerRealm="test.local.com"
   LdapSystemFQDN="dc= test, dc= local, dc=com"
   LdapBaseFQDN="dc=test, dc=local, dc=com"
   ```

   Apply the changes by running the configuration as follows\.

   ```
   #cd /opt/teradata/tdgss/bin
   #./run_tdgssconfig
   ```

1. Test the configuration by running the following command\.

   ```
   # /opt/teradata/tdat/tdgss/14.10.03.01/bin/tdsbind -u test_ldap -w test_ldap
   ```

   The output should be similar to the following\.

   ```
   LdapGroupBaseFQDN: dc=Test, dc=local, dc=com
   LdapUserBaseFQDN: dc=Test, dc=local, dc=com
   LdapSystemFQDN: dc= test, dc= local, dc=com
   LdapServerName: DC.test.local.com
   LdapServerPort: 389
   LdapServerRealm: test.local.com
   LdapClientUseTls: no
   LdapClientTlsReqCert: never
   LdapClientMechanism: SASL/DIGEST-MD5
   LdapServiceBindRequired: no
   LdapClientTlsCRLCheck: none
   LdapAllowUnsafeServerConnect: yes
   UseLdapConfig: no
   AuthorizationSupported: no
   FQDN: CN=test, CN=Users, DC=Anthem, DC=local, DC=com
   AuthUser: ldap://DC.test.local.com:389/CN=test1,CN=Users,DC=test,DC=local,DC=com
   DatabaseName: test
   Service: tdsbind
   ```

1. Restart TPA using the following command\.

   ```
   #tpareset -f "use updated TDGSSCONFIG GDO"                    
   ```

1. Create the same user in the Teradata database as in Active Directory, as shown following\.

   ```
   CREATE USER test_ldap AS PERM=1000, PASSWORD=test_ldap;
   GRANT LOGON ON ALL TO test WITH NULL PASSWORD;
   ```

If you change the user password in Active Directory for your LDAP user, you should specify this new password during connection to Teradata in LDAP mode\. In DEFAULT mode, you still have to connect Teradata with the LDAP user name and any password\.

## Using Netezza as a Source for AWS Schema Conversion Tool \(AWS SCT\)<a name="CHAP_Source.Netezza"></a>

You can use AWS SCT to convert data from Netezza to Amazon Redshift\. 

### Privileges for Netezza as a Source<a name="CHAP_Source.Netezza.Permissions"></a>

The privileges required for Netezza as a source are listed following: 
+ SELECT ON SYSTEM\.DEFINITION\_SCHEMA\.SYSTEM VIEW 
+ SELECT ON SYSTEM\.DEFINITION\_SCHEMA\.SYSTEM TABLE 
+ SELECT ON SYSTEM\.DEFINITION\_SCHEMA\.MANAGEMENT TABLE 
+ LIST ON *<database\_name>* 
+ LIST ON *<database\_name>*\.ALL\.TABLE 
+ LIST ON *<database\_name>*\.ALL\.EXTERNAL TABLE 
+ LIST ON *<database\_name>*\.ALL\.VIEW 
+ LIST ON *<database\_name>*\.ALL\.MATERIALIZED VIEW 
+ LIST ON *<database\_name>*\.ALL\.PROCEDURE 
+ LIST ON *<database\_name>*\.ALL\.SEQUENCE 
+ LIST ON *<database\_name>*\.ALL\.FUNCTION 
+ LIST ON *<database\_name>*\.ALL\.AGGREGATE 

### Connecting to Netezza as a Source<a name="CHAP_Source.Netezza.Connecting"></a>

Use the following procedure to connect to your Netezza source database with the AWS Schema Conversion Tool \(AWS SCT\)\. 

**To connect to a Netezza source database**

1. In the AWS Schema Conversion Tool, choose **Connect to Netezza**\.   
![\[Connect to source database\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/file_connect_to_netezza.png)

   The **Connect to Netezza** dialog box appears\.  
![\[Netezza connection information\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/source-netezza.png)

1. Provide the Netezza source database connection information\. Use the instructions in the following table\.   
****    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/CHAP_Source.html)

1. Choose **Test Connection** to verify that you can successfully connect to your source database\. 

1. Choose **OK** to connect to your source database\.

## Using Greenplum as a Source for AWS Schema Conversion Tool \(AWS SCT\)<a name="CHAP_Source.Greenplum"></a>

You can use AWS SCT to convert data from Greenplum to Amazon Redshift\. 

### Privileges for Greenplum as a Source<a name="CHAP_Source.Greenplum.Permissions"></a>

The privileges required for Greenplum as a source are listed following: 
+ CONNECT ON DATABASE *<database\_name>* 
+ USAGE ON SCHEMA *<schema\_name>* 

### Connecting to Greenplum as a Source<a name="CHAP_Source.Greenplum.Connecting"></a>

Use the following procedure to connect to your Greenplum source database with the AWS Schema Conversion Tool \(AWS SCT\)\. 

**To connect to a Greenplum source database**

1. In the AWS Schema Conversion Tool, choose **Connect to Greenplum**\.   
![\[Connect to source database\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/file_connect_to_greenplum.png)

   The **Connect to Greenplum** dialog box appears\.  
![\[Greenplum connection information\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/source-greenplum.png)

1. Provide the Greenplum source database connection information\. Use the instructions in the following table\.   
****    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/CHAP_Source.html)

1. Choose **Test Connection** to verify that you can successfully connect to your source database\. 

1. Choose **OK** to connect to your source database\.

## Using Vertica as a Source for AWS Schema Conversion Tool \(AWS SCT\)<a name="CHAP_Source.Vertica"></a>

You can use AWS SCT to convert data from Vertica to Amazon Redshift\. 

### Privileges for Vertica as a Source<a name="CHAP_Source.Vertica.Permissions"></a>

The privileges required for Vertica as a source are listed following: 
+ USAGE ON SCHEMA *<schema\_name>* 
+ USAGE ON SCHEMA PUBLIC 
+ GRANT SELECT ON ALL TABLES IN SCHEMA *<schema\_name>* 
+ SELECT ON ALL SEQUENCES IN SCHEMA *<schema\_name>* 
+ EXECUTE ON ALL FUNCTIONS IN SCHEMA *<schema\_name>* 
+ EXECUTE ON PROCEDURE *<schema\_name\.procedure\_name\(procedure\_signature\)>* 

### Connecting to Vertica as a Source<a name="CHAP_Source.Vertica.Connecting"></a>

Use the following procedure to connect to your Vertica source database with the AWS Schema Conversion Tool \(AWS SCT\)\. 

**To connect to a Vertica source database**

1. In the AWS Schema Conversion Tool, choose **Connect to Vertica**\.   
![\[Connect to source database\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/file_connect_to_vertica.png)

   The **Connect to Vertica** dialog box appears\.  
![\[Vertica connection information\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/source-vertica.png)

1. Provide the Vertica source database connection information\. Use the instructions in the following table\.   
****    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/CHAP_Source.html)

1. Choose **Test Connection** to verify that you can successfully connect to your source database\. 

1. Choose **OK** to connect to your source database\.

## Using Microsoft SQL Server DW as a Source for AWS Schema Conversion Tool \(AWS SCT\)<a name="CHAP_Source.SQLServerDW"></a>

You can use AWS SCT to convert data from Microsoft SQL Server DW to Amazon Redshift\. 

### Privileges for Microsoft SQL Server Data Warehouse as a Source<a name="CHAP_Source.SQLServerDW.Permissions"></a>

The privileges required for Microsoft SQL Server data warehouse as a source are listed following: 
+ VIEW DEFINITION 
+ VIEW DATABASE STATE 
+ SELECT ON SCHEMA :: *<schema\_name>* 

Repeat the grant for each database whose schema you are converting\. 

In addition, grant the following, and run the grant on the master database: 
+ VIEW SERVER STATE 

### Connecting to SQLServerDW as a Source<a name="CHAP_Source.SQLServerDW.Connecting"></a>

Use the following procedure to connect to your Microsoft SQL Server data warehouse source database with the AWS Schema Conversion Tool \(AWS SCT\)\. 

**To connect to a Microsoft SQL Server data warehouse source database**

1. In the AWS Schema Conversion Tool, choose **Connect to Microsoft SQL Server DW**\.   
![\[Connect to source database\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/file_connect_to_sqlserver_dw.png)

   The **Connect to Microsoft SQL Server DW** dialog box appears\.  
![\[Microsoft SQL Server data warehouse connection information\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/source-sql-server-dw.png)

1. Provide the Microsoft SQL Server data warehouse source database connection information\. Use the instructions in the following table\.   
****    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/CHAP_Source.html)

1. Choose **Test Connection** to verify that you can successfully connect to your source database\. 

1. Choose **OK** to connect to your source database\.