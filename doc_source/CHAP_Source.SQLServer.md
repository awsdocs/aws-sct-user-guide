# Using Microsoft SQL Server as a Source for AWS Schema Conversion Tool \(AWS SCT\)<a name="CHAP_Source.SQLServer"></a>

You can use AWS SCT to convert schemas and application code from SQL Server to the following targets: 
+ Amazon RDS for MySQL
+  Amazon Aurora \(MySQL\)
+ Amazon RDS for PostgreSQL
+ Amazon Aurora \(PostgreSQL\)
+ Amazon RDS for SQL Server

For more information, see the following sections:

**Topics**
+ [Permissions Required When Using Microsoft SQL Server as a Source](#CHAP_Source.SQLServer.Permissions)
+ [Using Windows Authentication When Using Microsoft SQL Server as a Source](#CHAP_Source.SQLServer.Permissions.WinAuth)
+ [Connecting to SQL Server as a Source](#CHAP_Source.SQLServer.Connecting)
+ [Converting SQL Server to MySQL](CHAP_Source.SQLServer.ToMySQL.md)
+ [Converting SQL Server to PostgreSQL](CHAP_Source.SQLServer.ToPostgreSQL.md)
+ [Converting SQL Server to Amazon RDS for SQL Server](CHAP_Source.SQLServer.ToRDSSQLServer.md)

## Permissions Required When Using Microsoft SQL Server as a Source<a name="CHAP_Source.SQLServer.Permissions"></a>

The privileges required for Microsoft SQL Server as a source are listed following: 
+ VIEW DEFINITION 
+ VIEW DATABASE STATE 

Repeat the grant for each database whose schema you are converting\. 

## Using Windows Authentication When Using Microsoft SQL Server as a Source<a name="CHAP_Source.SQLServer.Permissions.WinAuth"></a>

If your application runs on a Windows\-based intranet, you might be able to use Windows Authentication for database access\. Windows Authentication uses the current Windows identity established on the operating system thread to access the SQL Server database\. You can then map the Windows identity to a SQL Server database and permissions\. To connect to SQL Server using Windows Authentication, you must specify the Windows identity that your application is using\. You must also grant the Windows identity access to the SQL Server database\.

SQL Server has two modes of access: Windows Authentication mode and Mixed Mode\. Windows Authentication mode enables Windows Authentication and disables SQL Server Authentication\. Mixed Mode enables both Windows Authentication and SQL Server Authentication\. Windows Authentication is always available and cannot be disabled\. For more information about Windows Authentication, see the Microsoft Windows documentation\. 

The possible example for creating a user in TEST\_DB is shown below

```
USE [TEST_DB]
CREATE USER [TestUser] FOR LOGIN [TestDomain\TestUser]
GRANT VIEW DEFINITION TO [TestUser]
GRANT VIEW DATABASE STATE TO [TestUser]
```

### Using Windows Authentication with a JDBC Connection<a name="CHAP_Source.SQLServer.Permissions.WinAuth.JDBC"></a>

The JDBC driver does not support Windows Authentication when the driver is used on non\-Windows operating systems\. Windows Authentication credentials, such as user name and password, when connecting to SQL Server from non\-Windows operating systems\. In such cases, the applications must use SQL Server Authentication instead 

In JDBC connection string, the parameter `integratedSecurity` must be specified to connect using Windows Authentication\. The JDBC driver supports Integrated Windows Authentication on Windows operating systems through the `integratedSecurity` connection string parameter\.

To use integrated authentication

1. Install the JDBC driver\.

1. Copy the `sqljdbc_auth.dll` file to a directory on the Windows system path on the computer where the JDBC driver is installed\.

   The` sqljdbc_auth.dll` files are installed in the following location:

   <*installation directory*>\\sqljdbc\_<*version*>\\<*language*>\\auth\\

When you try to establish a connection to SQL Server database using Windows Authentication, you might get the error: This driver is not configured for integrated authentication\. This problem can be solved by performing the following actions:
+ need to declare two variables which point to the installed path of your JDBC:

  \-variable name: SQLJDBC\_HOME; variable value: D:\\lib\\JDBC4\.1\\enu \(where your sqljdbc4\.jar exists\);

  \-variable name: SQLJDBC\_AUTH\_HOME; variable value: D\\lib\\JDBC4\.1\\enu\\auth\\x86 \(if you are running 32bit OS\) or D\\lib\\JDBC4\.1\\enu\\auth\\x64 \(if you are running 64bit OS\)\. This is whe your sqljdbc\_auth\.dll is located\. 
+ copy sqljdbc\_auth\.dll to folder where your JDK/JRE is running\. You may copy to lib folder, bin folder, etc\. I copied to the following folder:

  ```
  [JDK_INSTALLED_PATH]\bin;
   [JDK_INSTALLED_PATH]\jre\bin;
   [JDK_INSTALLED_PATH]\jre\lib;
   [JDK_INSTALLED_PATH]\lib;
  ```
+ ensure that in your jdbc library folder, you only have SQLJDBC4\.jar\. Please remove other sqljdbc\*\.jar file from that folder \(or copy to other folder\)\. If you are adding the driver as part of your program, please ensure that you add only SQLJDBC4\.jar as driver to use\.
+ copy sqljdbc\_auth\.dll the file in the folder with your application\.

**Note**  
If you are running a 32\-bit Java Virtual Machine \(JVM\), use the sqljdbc\_auth\.dll file in the x86 folder, even if the operating system is the x64 version\. If you are running a 64\-bit JVM on a x64 processor, use the sqljdbc\_auth\.dll file in the x64 folder\.

When you connect to a SQL Server database, you can choose either the **Windows Authentication** or **SQL Server Authentication** for the **Authentication** option\.

## Connecting to SQL Server as a Source<a name="CHAP_Source.SQLServer.Connecting"></a>

Use the following procedure to connect to your Microsoft SQL Server source database with the AWS Schema Conversion Tool \(AWS SCT\)\. 

**To connect to a Microsoft SQL Server source database**

1. In the AWS Schema Conversion Tool, choose **Connect to Microsoft SQL Server**\.   
![\[Connect to source database\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/file_connect_to_sqlserver.png)

   The **Connect to Microsoft SQL Server** dialog box appears\.  
![\[Microsoft SQL Server connection information\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/source-sql-server.png)

1. Provide the Microsoft SQL Server source database connection information\. Use the instructions in the following table\.   
****    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/CHAP_Source.SQLServer.html)

1. Choose **Test Connection** to verify that you can successfully connect to your source database\. 

1. Choose **OK** to connect to your source database\.