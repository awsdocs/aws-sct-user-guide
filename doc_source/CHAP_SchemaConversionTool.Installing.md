# Installing and Updating the AWS Schema Conversion Tool<a name="CHAP_SchemaConversionTool.Installing"></a>

The AWS Schema Conversion Tool \(AWS SCT\) is a standalone application that provides a project\-based user interface\. AWS SCT is available for Fedora Linux, macOS, Microsoft Windows, and Ubuntu Linux version 15\.04\. AWS SCT is supported only on 64\-bit operating systems\. AWS SCT also installs the Java Runtime Environment \(JRE\) version 8u45\. 

## Installing the AWS Schema Conversion Tool<a name="CHAP_SchemaConversionTool.Installing.Procedure"></a>

**To install the AWS Schema Conversion Tool**

1. Download the \.zip file that contains the AWS SCT installer, using the link for your operating system, shown following: 

   + [Fedora Linux download](https://s3.amazonaws.com/publicsctdownload/Fedora/aws-schema-conversion-tool-1.0.latest.zip)

   + [macOS download](https://s3.amazonaws.com/publicsctdownload/MacOS/aws-schema-conversion-tool-1.0.latest.zip)

   + [Microsoft Windows download](https://s3.amazonaws.com/publicsctdownload/Windows/aws-schema-conversion-tool-1.0.latest.zip)

   + [Ubuntu Linux version 15\.04 download](https://s3.amazonaws.com/publicsctdownload/Ubuntu/aws-schema-conversion-tool-1.0.latest.zip)

1. Extract the AWS SCT installer file for your operating system, shown following\.   
****    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/CHAP_SchemaConversionTool.Installing.html)

1. Run the AWS SCT installer file extracted in the previous step\. Use the instructions for your operating system, shown following\.   
****    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/CHAP_SchemaConversionTool.Installing.html)

1. Install the Java Database Connectivity \(JDBC\) drivers for your source and target database engines\. For instructions and download links, see [Installing the Required Database Drivers](#CHAP_SchemaConversionTool.Installing.JDBCDrivers)\. 

## Installing the Required Database Drivers<a name="CHAP_SchemaConversionTool.Installing.JDBCDrivers"></a>

For the AWS Schema Conversion Tool to work correctly, you must install the JDBC drivers for your source and target database engines\. 

After you download the drivers, you give the location of the driver files\. For more information, see [Storing Driver Paths in the Global Settings](#CHAP_SchemaConversionTool.Installing.JDBCDrivers.Settings)\. 

You can download the database drivers from the following locations\. 

**Important**  
Install the latest version of the driver available\. The versions in the table following are example version numbers\. 


****  

| Database Engine | Drivers | Download Location | 
| --- | --- | --- | 
| Amazon Aurora \(MySQL compatible\) | mysql\-connector\-java\-5\.1\.6\.jar |   [https://www\.mysql\.com/products/connector/](https://www.mysql.com/products/connector/)   | 
| Amazon Aurora \(PostgreSQL compatible\) | postgresql\-9\.4\-1204\-jdbc42\.jar |   [https://jdbc\.postgresql\.org/download\.html](https://jdbc.postgresql.org/download.html)   | 
| Amazon Redshift | RedshiftJDBC41\-1\.1\.10\.1010\.jar |   [http://docs\.aws\.amazon\.com/redshift/latest/mgmt/configure\-jdbc\-connection\.html](http://docs.aws.amazon.com/redshift/latest/mgmt/configure-jdbc-connection.html)   | 
| Greenplum Database | postgresql\-9\.4\-1204\-jdbc42\.jar |  [https://jdbc\.postgresql\.org/](https://jdbc.postgresql.org/)   | 
| Microsoft SQL Server | sqljdbc4\.jar |   [https://www\.microsoft\.com/en\-us/download/details\.aspx?displaylang=en&id=11774](https://www.microsoft.com/en-us/download/details.aspx?displaylang=en&id=11774)   | 
| MySQL | mysql\-connector\-java\-5\.1\.6\.jar |   [https://www\.mysql\.com/products/connector/](https://www.mysql.com/products/connector/)   | 
| Netezza |  nzjdbc\.jar Use the client tools software\. Install driver version 7\.2\.1, which is backwards compatible with data warehouse version 7\.2\.0\.   |   [http://www\.ibm\.com/support/knowledgecenter/SSULQD\_7\.2\.1/com\.ibm\.nz\.datacon\.doc/c\_datacon\_plg\_overview\.html](http://www.ibm.com/support/knowledgecenter/SSULQD_7.2.1/com.ibm.nz.datacon.doc/c_datacon_plg_overview.html)   | 
| Oracle |  ojdbc7\.jar Driver versions 7 and later are supported\.   |   [http://www\.oracle\.com/technetwork/database/features/jdbc/jdbc\-drivers\-12c\-download\-1958347\.html](http://www.oracle.com/technetwork/database/features/jdbc/jdbc-drivers-12c-download-1958347.html)   | 
| PostgreSQL | postgresql\-9\.4\-1204\-jdbc42\.jar |   [https://jdbc\.postgresql\.org/download\.html](https://jdbc.postgresql.org/download.html)   | 
| Teradata |  terajdbc4\.jar tdgssconfig\.jar  |   [https://downloads\.teradata\.com/download/connectivity/jdbc\-driver ](https://downloads.teradata.com/download/connectivity/jdbc-driver)   | 
| Vertica |  vertica\-jdbc\-7\.2\.3\-0\_all Driver versions 7\.2\.0 and later are supported\.  |   [https://my\.vertica\.com/download/vertica/client\-drivers/](https://my.vertica.com/download/vertica/client-drivers/)   | 

### Installing JDBC Drivers on Linux<a name="CHAP_SchemaConversionTool.Installing.JDBCDrivers.Linux"></a>

You can use the following steps to install the JDBC drivers on your Linux system for use with AWS SCT\. 

**To install JDBC drivers on your Linux system**

1. Create a directory to store the JDBC drivers in\. 

   ```
   PROMPT>sudo mkdir –p /usr/local/jdbc-drivers
   ```

1. Install the JDBC driver for your database engine using the commands shown following\.   
****    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/CHAP_SchemaConversionTool.Installing.html)

### Storing Driver Paths in the Global Settings<a name="CHAP_SchemaConversionTool.Installing.JDBCDrivers.Settings"></a>

After you have downloaded and installed the required JDBC drivers, you can set the location of the drivers globally in the AWS SCT settings\. If you don't set the location of the drivers globally, the application asks you for the location of the drivers when you connect to a database\. 

**To update the driver file locations**

1. In the AWS Schema Conversion Tool, choose **Settings**, and then choose **Global Settings**\.   
![\[Choose global settings\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/select_global_settings.png)

1. For **Global settings**, choose **Drivers**\. Add the file path to the JDBC driver for your source database engine and your target Amazon RDS DB instance database engine\. 
**Note**  
For Teradata, you specify two drivers separated by a semicolon\.  
![\[Global settings\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/driver-settings.png)

1. When you are finished adding the driver paths, choose **OK**\. 

## Updating the AWS Schema Conversion Tool<a name="CHAP_SchemaConversionTool.Installing.Updating"></a>

To check whether new version of AWS SCT is available, choose **Help**, and then choose **Check for Updates**\. If there is a newer version of AWS SCT available, you are prompted to download and install the newer version\. 