# Converting Informatica ETL scripts with AWS SCT<a name="CHAP-converting-informatica"></a>

You can use AWS SCT command line interface \(CLI\) to convert your Informatica ETL scripts so that you can use the scripts with your new target database\. This conversion includes three key steps\. First, AWS SCT converts the SQL code that is embedded in your Informatica objects\. Next, AWS SCT changes the names of database objects according to the migration rules that you specified in your project\. Finally, AWS SCT redirects the connections of your Informatica ETL scripts to the new target database\.

You can convert Informatica ETL scripts as part of AWS SCT database conversion project\. Make sure that you add your source and target databases to the project when you convert Informatica ETL scripts\.

To convert Informatica ETL scripts, make sure that you use AWS SCT version 1\.0\.667 or later\. Also, familiarize yourself with the command line interface of AWS SCT\. For more information, see [AWS SCT CLI Reference](CHAP_Reference.md)\.

**To convert Informatica ETL scripts using AWS SCT**

1. Create a new AWS SCT CLI script or edit an existing scenario template\. For example, you can download and edit the `InformaticConversionTemplate.scts` template\. For more information, see [Getting CLI scenarios](CHAP_Reference.md#CHAP_Reference.Scenario)\.

1. Download the required JDBC drivers for your source and target databases\. Specify the location of these drivers using the `SetGlobalSettings` command\. Also, specify the folders where AWS SCT can save log files\.

   The following code example shows you how to add the path to Oracle and PostgreSQL drivers to the AWS SCT settings\. After you run this code example, AWS SCT stores log files in the `C:\sct_log` folder\. Also, AWS SCT stores console log files in the `C:\Temp\oracle_postgresql` folder\.

   ```
   SetGlobalSettings
   	-save: 'true'
   	-settings: '{"oracle_driver_file": "C:\\drivers\\ojdbc8.jar",    
   	"postgresql_driver_file": "C:\\drivers\\postgresql-42.2.19.jar" }'
   /
   
   SetGlobalSettings
   	-save: 'false'
   	-settings: '{
   "log_folder": "C:\\sct_log",
   "console_log_folder": "C:\\Temp\\oracle_postgresql"}'
   /
   ```

1. Create a new AWS SCT project\. Enter the name and location of your project\.

   The following code example creates the `oracle_postgresql` project in the `C:\Temp` folder\.

   ```
   CreateProject
   	-name: 'oracle_postgresql'
   	-directory: 'C:\Temp'
   /
   ```

1. Add connection information about your source and target databases\.

   The following code example adds Oracle and PostgreSQL databases as a source and target for your AWS SCT project\.

   ```
   AddSource
   	-password: 'source_password'
   	-port: '1521'
   	-vendor: 'ORACLE'
   	-name: 'ORACLE'
   	-host: 'source_address'
   	-database: 'ORCL'
   	-user: 'source_user'
   /
   AddTarget
   	-database: 'postgresql'
   	-password: 'target_password'
   	-port: '5432'
   	-vendor: 'POSTGRESQL'
   	-name: 'POSTGRESQL'
   	-host: 'target_address'
   	-user: 'target_user'
   /
   ```

   In the preceding example, replace *source\_user* and *target\_user* with the names of your database users\. Next, replace *source\_password* and *target\_password* with your passwords\. For *source\_address* and *target\_address*, enter the IP addresses of your source and target database servers\.

   To connect to an Oracle database version 19 and higher, use the Oracle service name in the `AddSource` command\. To do so, add the `-connectionType` parameter and set its value to `'basic_service_name'`\. Then, add the `-servicename` parameter and set its value to your Oracle service name\. For more information about the `AddSource` command, see the [AWS Schema Conversion Tool CLI Reference](https://s3.amazonaws.com/publicsctdownload/AWS+SCT+CLI+Reference.pdf)\.

1. Create a new AWS SCT mapping rule, which defines the target database engines for each source database schema\. For more information, see [Creating mapping rules in AWS SCT](CHAP_Mapping.md)\.

   The following code example creates a mapping rule that includes all source Oracle database schemas and defines PostgreSQL as a migration target\.

   ```
   AddServerMapping
   	-sourceTreePath: 'Servers.ORACLE'
   	-targetTreePath: 'Servers.POSTGRESQL'
   /
   ```

1. Add connection information about your Informatica source and target XML files\.

   The following code example adds the Informatica XML files from the `C:\Informatica_source` and `C:\Informatica_target` folders\.

   ```
   AddSource
   	-name: 'INFA_SOURCE'
   	-vendor: 'INFORMATICA'
   	-mappingsFolder: 'C:\Informatica_source'
   /
   AddTarget
   	-name: 'INFA_TARGET'
   	-vendor: 'INFORMATICA'
   	-mappingsFolder: 'C:\Informatica_target'
   /
   ```

1. Create another mapping rule to define the target Informatica XML file for your source Informatica XML file\.

   The following code example creates a mapping rule that includes source and target Informatica XML files used in the preceding example\.

   ```
   AddServerMapping
   -sourceTreePath: 'ETL.INFA_SOURCE'
   -targetTreePath: 'ETL.INFA_TARGET'
   /
   ```

1. Specify the database server connection that corresponds to the Informatica connection name reference\.

   The following code example configures the redirect of your Informatica ETL scripts from your source to the new target database\. This example also configures connection variables\.

   ```
   ConfigureInformaticaConnectionsRedirect
   	-treePath: 'ETL.INFA_SOURCE.Files'
   	-connections: '{
   	"ConnectionNames": [
   	{
   		"name": "Oracle_src",
   		"newName": "postgres",
   		"treePath": "Servers.ORACLE"
   	}
   	]
   	"ConnectionVariables": [
   	{
            "name": "$Source",
            "treePath": "Servers.ORACLE"
       }
       ]
   	}'
   /
   ```

1. Convert your source database schemas and Informatica ETL scripts\.

   The following code example converts all your source Oracle database schemas and your Informatica XML file\.

   ```
   Convert
   	-treePath: 'Servers.ORACLE.Schemas.%'
   /
   Convert
   	-treePath: 'ETL.INFA_SOURCE.Files'
   /
   ```

1. \(Optional\) Save your conversion project and the assessment report\. This report includes the conversion action items and recommendations about how to address each\.

   The following code example saves your project and saves a copy of the assessment report as a PDF file in the `C:\Temp` folder\.

   ```
   SaveProject
   /
   SaveReportPDF
   	-treePath: 'ETL.INFA_SOURCE.Files'
   	-file:'C:\Temp\Informatica.pdf'
   /
   ```

1. Save your converted Informatica XML file\.

   The following code example saves the converted XML file in the `C:\Temp` folder\. You specified this folder in the previous step using the `AddTarget` command\.

   ```
   SaveTargetInformaticaXML
   -treePath: 'ETL.INFA_TARGET.Files'
   /
   ```

1. Save your script as an `.scts` file and run it using the `RunSCTBatch` command in the AWS SCT CLI\. For more information, see [AWS SCT CLI script mode](CHAP_Reference.md#CHAP_Reference.ScriptMode)\.

   The following example runs the `Informatica.scts` script in the `C:\Temp` folder\. You can use this example in Windows\.

   ```
   RunSCTBatch.cmd --pathtoscts "C:\Temp\Informatica.scts"
   ```

   If you edit your source Informatica ETL scripts, then run the AWS SCT CLI script again\.