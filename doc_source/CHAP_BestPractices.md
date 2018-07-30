# Best Practices for the AWS Schema Conversion Tool<a name="CHAP_BestPractices"></a>

Following, you can find information on best practices and options for using the AWS Schema Conversion Tool \(AWS SCT\)\. 

## General Memory Management and Performance Options<a name="CHAP_BestPractices.Memory"></a>

You can configure the AWS Schema Conversion Tool with different memory performance settings\. Increasing memory speeds up the performance of your conversion but uses more memory resources on your desktop\. 

To set your memory management option, choose **Global Settings** from the **Settings** menu, and choose the **Performance and Memory** tab\. Choose one of the following options: 
+ **Fast conversion, but large memory consumption** – This option optimizes for speed of the conversion, but might require more memory for the object reference cache\. 
+ **Low memory consumption, but slower conversion** – This option minimizes the amount of memory used, but results in a slower conversion\. Use this option if your desktop has a limited amount of memory\. 
+ **Balance speed with memory consumption** – This option optimizes provides a balance between memory use and conversion speed\. 

## Configuring Additional Memory<a name="CHAP_BestPractices.JVM"></a>

For converting large database schemas, for example a database with 3,500 stored procedures, you can configure the amount of memory available to the AWS Schema Conversion Tool\. 

**To modify the amount of memory AWS SCT consumes**

1. Locate the folder where the configuration file is \(C:\\Program Files\\AWS Schema Conversion Tool\\App\)\. 

1. Open the configuration file `AWS Schema Conversion Tool.cfg` with Notepad or your favorite text editor\. 

1. Edit the `JVMUserOptions` section to set the minimum and maximum memory available\. The following example sets the minimum to 4 GB and the maximum to 40 GB\. 

   ```
   1. [JVMUserOptions]
   2. -Xmx48960m 
   3. -Xms4096m
   ```