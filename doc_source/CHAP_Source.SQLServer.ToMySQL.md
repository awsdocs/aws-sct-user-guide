# Converting SQL Server to MySQL<a name="CHAP_Source.SQLServer.ToMySQL"></a>

To emulate Microsoft SQL Server database functions in your converted MySQL code, use the SQL Server to MySQL extension pack in AWS SCT\. For more information about extension packs, see [Using AWS SCT extension packs](CHAP_ExtensionPack.md)\. 

**Topics**
+ [Privileges for MySQL as a target](#CHAP_Source.SQLServer.ToMySQL.ConfigureTarget)
+ [SQL Server to MySQL conversion settings](#CHAP_Source.SQLServer.ToMySQL.ConversionSettings)
+ [Migration considerations](#CHAP_Source.SQLServer.ToMySQL.MigrationConsiderations)

## Privileges for MySQL as a target<a name="CHAP_Source.SQLServer.ToMySQL.ConfigureTarget"></a>

The privileges required for MySQL as a target are listed following:
+ CREATE ON \*\.\*
+ ALTER ON \*\.\*
+ DROP ON \*\.\*
+ INDEX ON \*\.\*
+ REFERENCES ON \*\.\*
+ SELECT ON \*\.\*
+ CREATE VIEW ON \*\.\*
+ SHOW VIEW ON \*\.\*
+ TRIGGER ON \*\.\*
+ CREATE ROUTINE ON \*\.\*
+ ALTER ROUTINE ON \*\.\*
+ EXECUTE ON \*\.\*
+ INSERT, UPDATE ON AWS\_SQLSERVER\_EXT\.\*
+ INSERT, UPDATE, DELETE ON AWS\_SQLSERVER\_EXT\_DATA\.\*
+ CREATE TEMPORARY TABLES ON AWS\_SQLSERVER\_EXT\_DATA\.\*

You can use the following code example to create a database user and grant the privileges\.

```
CREATE USER 'user_name' IDENTIFIED BY 'your_password';
GRANT CREATE ON *.* TO 'user_name';
GRANT ALTER ON *.* TO 'user_name';
GRANT DROP ON *.* TO 'user_name';
GRANT INDEX ON *.* TO 'user_name';
GRANT REFERENCES ON *.* TO 'user_name';
GRANT SELECT ON *.* TO 'user_name';
GRANT CREATE VIEW ON *.* TO 'user_name';
GRANT SHOW VIEW ON *.* TO 'user_name';
GRANT TRIGGER ON *.* TO 'user_name';
GRANT CREATE ROUTINE ON *.* TO 'user_name';
GRANT ALTER ROUTINE ON *.* TO 'user_name';
GRANT EXECUTE ON *.* TO 'user_name';
GRANT SELECT ON mysql.proc TO 'user_name';
GRANT INSERT, UPDATE ON AWS_SQLSERVER_EXT.* TO 'user_name';
GRANT INSERT, UPDATE, DELETE ON AWS_SQLSERVER_EXT_DATA.* TO 'user_name';
GRANT CREATE TEMPORARY TABLES ON AWS_SQLSERVER_EXT_DATA.* TO 'user_name';
```

In the example preceding, replace *user\_name* with the name of your user\. Then, replace *your\_password* with a secure password\.

To use Amazon RDS for MySQL as a target, set the `log_bin_trust_function_creators` parameter to true, and the `character_set_server` to `latin1`\. To configure these parameters, create a new DB parameter group or modify an existing DB parameter group\.

To use Aurora MySQL as a target, set the `log_bin_trust_function_creators` parameter to true, and the `character_set_server` to `latin1`\. Also, set the `lower_case_table_names` parameter to true\. To configure these parameters, create a new DB parameter group or modify an existing DB parameter group\.

## SQL Server to MySQL conversion settings<a name="CHAP_Source.SQLServer.ToMySQL.ConversionSettings"></a>

To edit SQL Server to MySQL conversion settings, in AWS SCT choose **Settings**, and then choose **Conversion settings**\. From the upper list, choose **SQL Server**, and then choose **SQL Server – MySQL**\. AWS SCT displays all available settings for SQL Server to MySQL conversion\.

SQL Server to MySQL conversion settings in AWS SCT include options for the following:
+ To limit the number of comments with action items in the converted code\.

  For **How detailed should comments be in the converted SQL**, choose the severity of action items\. AWS SCT adds comments in the converted code for action items of the selected severity and higher\.

  For example, to minimize the number of comments in your converted code, choose **Errors only**\. To include comments for all action items in your converted code, choose **All messages**\.
+ To allow your source SQL Server database to store the output of `EXEC` in a table\. AWS SCT creates temporary tables and an additional procedure to emulate this feature\. To use this emulation, select **Create additional routines for handling open datasets**\.

## Migration considerations<a name="CHAP_Source.SQLServer.ToMySQL.MigrationConsiderations"></a>

Consider these things when migrating a SQL Server schema to MySQL:
+ MySQL doesn’t support the `MERGE` statement\. However, AWS SCT can emulate the `MERGE` statement during conversion by using the `INSERT ON DUPLICATE KEY` clause and the `UPDATE FROM and DELETE FROM` statements\.

  For correct emulation using `INSERT ON DUPLICATE KEY`, make sure that a unique constraint or primary key exists on the target MySQL database\.
+ You can use a `GOTO` statement and a label to change the order that statements are run in\. Any Transact\-SQL statements that follow a `GOTO` statement are skipped, and processing continues at the label\. You can use `GOTO` statements and labels anywhere within a procedure, batch, or statement block\. You can also nest `GOTO` statements\.

  MySQL doesn’t use `GOTO` statements\. When AWS SCT converts code that contains a `GOTO` statement, it converts the statement to use a `BEGIN…END` or `LOOP…END LOOP` statement\. You can find examples of how AWS SCT converts `GOTO` statements in the table following\.  
****    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/CHAP_Source.SQLServer.ToMySQL.html)
+ MySQL doesn't support multistatement table\-valued functions\. AWS SCT simulates table\-valued functions during a conversion by creating temporary tables and rewriting statements to use these temporary tables\.