# Installing, Verifying, and Updating the AWS Schema Conversion Tool \(AWS SCT\)<a name="CHAP_Installing"></a>

The AWS Schema Conversion Tool \(AWS SCT\) is a standalone application that provides a project\-based user interface\. AWS SCT is available for Fedora Linux, macOS, Microsoft Windows, and Ubuntu Linux version 15\.04\. AWS SCT is supported only on 64\-bit operating systems\. AWS SCT also installs the Java Runtime Environment \(JRE\) version 8u45\. 

To ensure that you get the correct version of the AWS SCT distribution file, we provide verification steps after you download the compressed file\. You can verify the file using the steps provided\.

**Topics**
+ [Installing the AWS SCT](#CHAP_Installing.Procedure)
+ [Verifying the AWS SCT File Download](#CHAP_Installing.InstallValidation)
+ [Installing the Required Database Drivers](#CHAP_Installing.JDBCDrivers)
+ [Updating the AWS SCT](#CHAP_Installing.Updating)

## Installing the AWS SCT<a name="CHAP_Installing.Procedure"></a>

**To install the AWS SCT**

1. Download the compressed file that contains the AWS SCT installer, using the link for your operating system\. All compressed files have a \.zip extension\. When you extract the AWS SCT installer file, it will be in the appropriate format for your operating system\. 
   + [Microsoft Windows](https://s3.amazonaws.com/publicsctdownload/Windows/aws-schema-conversion-tool-1.0.latest.zip)
   + [Apple macOS](https://s3.amazonaws.com/publicsctdownload/MacOS/aws-schema-conversion-tool-1.0.latest.zip)
   + [Ubuntu Linux \(\.deb\)](https://s3.amazonaws.com/publicsctdownload/Ubuntu/aws-schema-conversion-tool-1.0.latest.zip)
   + [Fedora Linux \(\.rpm\)](https://s3.amazonaws.com/publicsctdownload/Fedora/aws-schema-conversion-tool-1.0.latest.zip)

1. Extract the AWS SCT installer file for your operating system, shown following\.   
****    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/CHAP_Installing.html)

1. Run the AWS SCT installer file extracted in the previous step\. Use the instructions for your operating system, shown following\.   
****    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/CHAP_Installing.html)

1. Install the Java Database Connectivity \(JDBC\) drivers for your source and target database engines\. For instructions and download links, see [ Installing the Required Database Drivers](#CHAP_Installing.JDBCDrivers)\. 

### Installing Previous Versions of the AWS SCT<a name="CHAP_Installing.PreviousVersions"></a>

 You can download and install previous versions of the AWS SCT\. Use the following format to download a previous version\. You must provide the version and OS information using this format\. 

```
https://d211wdu1froga6.cloudfront.net/builds/1.0/<version>/<OS>/aws-schema-conversion-tool-1.0.zip
```

For example, to download AWS SCT version 607, do the following:
+ MacOS \- [ https://d211wdu1froga6\.cloudfront\.net/builds/1\.0/607/MacOS/aws\-schema\-conversion\-tool\-1\.0\.zip ](https://d211wdu1froga6.cloudfront.net/builds/1.0/607/MacOS/aws-schema-conversion-tool-1.0.zip)
+ Windows \- [ https://d211wdu1froga6\.cloudfront\.net/builds/1\.0/607/Windows/aws\-schema\-conversion\-tool\-1\.0\.zip ](https://d211wdu1froga6.cloudfront.net/builds/1.0/607/Windows/aws-schema-conversion-tool-1.0.zip)
+ Ubuntu \- [ https://d211wdu1froga6\.cloudfront\.net/builds/1\.0/607/Ubuntu/aws\-schema\-conversion\-tool\-1\.0\.zip ](https://d211wdu1froga6.cloudfront.net/builds/1.0/607/Ubuntu/aws-schema-conversion-tool-1.0.zip)
+ Fedora \- [ https://d211wdu1froga6\.cloudfront\.net/builds/1\.0/607/Fedora/aws\-schema\-conversion\-tool\-1\.0\.zip ](https://d211wdu1froga6.cloudfront.net/builds/1.0/607/Fedora/aws-schema-conversion-tool-1.0.zip)

## Verifying the AWS SCT File Download<a name="CHAP_Installing.InstallValidation"></a>

There are several ways you can verify the distribution file of the AWS SCT\. The simplest is to compare the checksum of the file with the published checksum from AWS\. As an additional level of security, you can use the procedures below to verify the distribution file, based on the operating system where you installed the file\. 

This section includes the following topics\.

**Topics**
+ [Verifying the Checksum of the AWS SCT File](#CHAP_Installing.InstallValidation.Checksum)
+ [Verifying the AWS SCT RPM Files on Fedora](#CHAP_Installing.InstallValidation.RPM)
+ [Verifying the AWS SCT DEB Files on Ubuntu](#CHAP_Installing.InstallValidation.DEB)
+ [Verifying the AWS SCT MSI File on Microsoft Windows](#CHAP_Installing.InstallValidation.MSI)
+ [Verifying the AWS SCT Application on Mac OS](#CHAP_Installing.InstallValidation.Mac)

### Verifying the Checksum of the AWS SCT File<a name="CHAP_Installing.InstallValidation.Checksum"></a>

In order to detect any errors that could have been introduced when downloading or storing the AWS SCT compressed file, you can compare the file checksum with a value provided by AWS\. AWS uses the SHA256 algorithm for the checksum\.

**To verify the AWS SCT distribution file using a checksum**

1. Download the AWS SCT distribution file using the links in the Installing section\.

1. Download the latest checksum file, called [sha256Check\.txt](https://d2fk11eyrwr7ob.cloudfront.net/sha256Check.txt)\. For example, the file can appear like the following:

   ```
   Fedora   b4f5f66f91bfcc1b312e2827e960691c269a9002cd1371cf1841593f88cbb5e6
   Ubuntu   4315eb666449d4fcd95932351f00399adb6c6cf64b9f30adda2eec903c54eca4
   Windows  6e29679a3c53c5396a06d8d50f308981e4ec34bd0acd608874470700a0ae9a23
   MacOs    ed56d3ab49309e92ac4d2ef439d35449ac1326f470c23dc5866e1bf0a60b0e67
   ```

1. Run the SHA256 validation command for your operating system in the directory that contains the distribution file\. For example, the command to run on the Mac operating system is the following:

   ```
   shasum -a 256 aws-schema-conversion-tool-1.0.latest.zip
   ```

1. Compare the results of the command with the value shown in the sha256Check\.txt file\. The two values should match\.

### Verifying the AWS SCT RPM Files on Fedora<a name="CHAP_Installing.InstallValidation.RPM"></a>

AWS provides another level of validation in addition to the distribution file checksum\. All RPM files in the distribution file are signed by an AWS private key\. The public GPG key can be viewed at [amazon\.com\.public\.gpg\-key](https://d2fk11eyrwr7ob.cloudfront.net/aws-dms-team@amazon.com.public.gpg-key)\.

**To verify the AWS SCT RPM files on Fedora**

1. Download the AWS SCT distribution file using the links in the Installing section\.

1. Verifying the checksum of the AWS SCT distribution file\.

1. Extract the contents of the distribution file\. Locate the RPM file you want to verify\.

1. Download GPG public key from [ amazon\.com\.public\.gpg\-key ](https://d2fk11eyrwr7ob.cloudfront.net/aws-dms-team@amazon.com.public.gpg-key)

1. Import the public key to your RPM DB \(make sure you have the appropriate permissions\) by using the following command:

   ```
   sudo rpm --import aws-dms-team@amazon.com.public.gpg-key
   ```

1. Check that the import was successful by running the following command:

   ```
   rpm -q --qf "%{NAME}-%{VERSION}-%{RELEASE} \n %{SUMMARY} \n" gpg-pubkey-ea22abf4-5a21d30c
   ```

1. Check the RPM signature by running the following command:

   ```
   rpm --checksig -v aws-schema-conversion-tool-1.0.build number-1.x86_64.rpm
   ```

### Verifying the AWS SCT DEB Files on Ubuntu<a name="CHAP_Installing.InstallValidation.DEB"></a>

AWS provides another level of validation in addition to the distribution file checksum\. All DEB files in the distribution file are signed by a GPG detached signature\.

**To verify the AWS SCT DEB files on Ubuntu**

1. Download the AWS SCT distribution file using the links in the Installing section\.

1. Verifying the checksum of the AWS SCT distribution file\.

1. Extract the contents of the distribution file\. Locate the DEB file you want to verify\.

1. Download the detached signature from [aws\-schema\-conversion\-tool\-1\.0\.latest\.deb\.asc](https://d2fk11eyrwr7ob.cloudfront.net/Ubuntu/signatures/aws-schema-conversion-tool-1.0.latest.deb.asc)\.

1. Download the GPG public key from [amazon\.com\.public\.gpg\-key](https://d2fk11eyrwr7ob.cloudfront.net/aws-dms-team@amazon.com.public.gpg-key)\.

1. Import the GPG public key by running the following command:

   ```
   gpg --import aws-dms-team@amazon.com.public.gpg-key
   ```

1. Verify the signature by running the following command:

   ```
   gpg --verify aws-schema-conversion-tool-1.0.latest.deb.asc aws-schema-conversion-tool-1.0.build number.deb
   ```

### Verifying the AWS SCT MSI File on Microsoft Windows<a name="CHAP_Installing.InstallValidation.MSI"></a>

AWS provides another level of validation in addition to the distribution file checksum\. The MSI file has a digital signature you can check to ensure it was signed by AWS\.

**To verify the AWS SCT MSI file on Windows**

1. Download the AWS SCT distribution file using the links in the Installing section\.

1. Verifying the checksum of the AWS SCT distribution file\.

1. Extract the contents of the distribution file\. Locate the MSI file you want to verify\.

1. In Windows Explorer, right\-click the MSI file and select **Properties**\.

1. Choose the **Digital Signatures** tab\.

1. Verify that the digital signature is from Amazon Services LLC\.

### Verifying the AWS SCT Application on Mac OS<a name="CHAP_Installing.InstallValidation.Mac"></a>

AWS provides another level of validation in addition to the distribution file checksum\. Once you have installed the AWS SCT on the Mac OS, you can verify the application using the following procedure\.

**To verify the AWS SCT Application on Mac OS**

1. Download the AWS SCT distribution file using the links in the Installing section\.

1. Verifying the checksum of the AWS SCT distribution file\.

1. Extract the contents of the distribution file\. 

1. Double\-click the DMG file\.

1. Install the AWS SCT\. 

1. Verify the application by running the following command:

   ```
   codesign -dvvv /Applications/AWS\ Schema\ Conversion\ Tool.app/
   ```

## Installing the Required Database Drivers<a name="CHAP_Installing.JDBCDrivers"></a>

For the AWS SCT to work correctly, you must install the JDBC drivers for your source and target database engines\. 

After you download the drivers, you give the location of the driver files\. For more information, see [ Storing Driver Paths in the Global Settings](#CHAP_Installing.JDBCDrivers.Settings)\. 

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
| IBM DB2 (LUW) | db2jcc4\.jar (JDBC 4.0 Driver) |  [https://www-01\.ibm\.com/support/docview\.wss?uid=swg21363866](https://www-01.ibm.com/support/docview.wss?uid=swg21363866)   | 
| Microsoft SQL Server | sqljdbc4\.jar |   [https://www\.microsoft\.com/en\-us/download/details\.aspx?displaylang=en&id=11774](https://www.microsoft.com/en-us/download/details.aspx?displaylang=en&id=11774)   | 
| MySQL | mysql\-connector\-java\-5\.1\.6\.jar |   [https://www\.mysql\.com/products/connector/](https://www.mysql.com/products/connector/)   | 
| Netezza |  nzjdbc\.jar Use the client tools software\. Install driver version 7\.2\.1, which is backwards compatible with data warehouse version 7\.2\.0\.   |   [http://www\.ibm\.com/support/knowledgecenter/SSULQD\_7\.2\.1/com\.ibm\.nz\.datacon\.doc/c\_datacon\_plg\_overview\.html](http://www.ibm.com/support/knowledgecenter/SSULQD_7.2.1/com.ibm.nz.datacon.doc/c_datacon_plg_overview.html)   | 
| Oracle |  ojdbc7\.jar Driver versions 7 and later are supported\.   |   [http://www\.oracle\.com/technetwork/database/features/jdbc/jdbc\-drivers\-12c\-download\-1958347\.html](http://www.oracle.com/technetwork/database/features/jdbc/jdbc-drivers-12c-download-1958347.html)   | 
| PostgreSQL | postgresql\-9\.4\-1204\-jdbc42\.jar |   [https://jdbc\.postgresql\.org/download\.html](https://jdbc.postgresql.org/download.html)   | 
| Teradata |  terajdbc4\.jar tdgssconfig\.jar  |   [https://downloads\.teradata\.com/download/connectivity/jdbc\-driver ](https://downloads.teradata.com/download/connectivity/jdbc-driver)   | 
| Vertica |  vertica\-jdbc\-7\.2\.3\-0\_all Driver versions 7\.2\.0 and later are supported\.  |   [https://my\.vertica\.com/download/vertica/client\-drivers/](https://my.vertica.com/download/vertica/client-drivers/)   | 

### Installing JDBC Drivers on Linux<a name="CHAP_Installing.JDBCDrivers.Linux"></a>

You can use the following steps to install the JDBC drivers on your Linux system for use with AWS SCT\. 

**To install JDBC drivers on your Linux system**

1. Create a directory to store the JDBC drivers in\. 

   ```
   PROMPT>sudo mkdir –p /usr/local/jdbc-drivers
   ```

1. Install the JDBC driver for your database engine using the commands shown following\.   
****    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/CHAP_Installing.html)

### Storing Driver Paths in the Global Settings<a name="CHAP_Installing.JDBCDrivers.Settings"></a>

After you have downloaded and installed the required JDBC drivers, you can set the location of the drivers globally in the AWS SCT settings\. If you don't set the location of the drivers globally, the application asks you for the location of the drivers when you connect to a database\. 

**To update the driver file locations**

1. In the AWS SCT, choose **Settings**, and then choose **Global Settings**\.   
![\[Choose global settings\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/select_global_settings.png)

1. For **Global settings**, choose **Drivers**\. Add the file path to the JDBC driver for your source database engine and your target Amazon RDS DB instance database engine\. 
**Note**  
For Teradata, you specify two drivers separated by a semicolon\.  
![\[Global settings\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/driver-settings.png)

1. When you are finished adding the driver paths, choose **OK**\. 

## Updating the AWS SCT<a name="CHAP_Installing.Updating"></a>

AWS periodically updates the AWS SCT with new features and functionality\. If you are updating from a previous version, create a new AWS SCT project and reconvert any database objects you are using\.

You can check to see if updates exist for the AWS SCT\.

**To check for updates to AWS SCT**

1. When in the AWS SCT, choose **Help** and then choose **Check for Updates**\.

1. In the **Check for Updates dialog box**, choose **What's New**\. If the link does not appear, you have the latest version\.
