# Converting Oracle to Amazon RDS for PostgreSQL or Amazon Aurora PostgreSQL<a name="CHAP_Source.Oracle.ToPostgreSQL"></a>

When you convert an Oracle database to RDS for PostgreSQL or Amazon Aurora PostgreSQL, be aware of the following\.

**Topics**
+ [Privileges for PostgreSQL as a target database](#CHAP_Source.Oracle.ToPostgreSQL.ConfigureTarget)
+ [Oracle to PostgreSQL conversion settings](#CHAP_Source.Oracle.ToPostgreSQL.ConversionSettings)
+ [Converting Oracle sequences](#CHAP_Source.Oracle.ToPostgreSQL.ConvertSequences)
+ [Converting Oracle ROWID](#CHAP_Source.Oracle.ToPostgreSQL.ConvertRowID)
+ [Converting Oracle dynamic SQL](#CHAP_Source.Oracle.ToPostgreSQL.DynamicSQL)
+ [Converting Oracle partitions](#CHAP_Source.Oracle.ToPostgreSQL.PG10Partitioning)

When converting Oracle system objects to PostgreSQL, AWS SCT performs conversions as shown in the following table\.


| Oracle system object | Description | Converted PostgreSQL object | 
| --- | --- | --- | 
| V$VERSION  | Displays version numbers of core library components in the Oracle Database | aws\_oracle\_ext\.v$version | 
| V$INSTANCE | A view that shows the state of the current instance\. | aws\_oracle\_ext\.v$instance | 

You can use AWS SCT to convert Oracle SQL\*Plus files to psql, which is a terminal\-based front\-end to PostgreSQL\. For more information, see [Converting application SQL using AWS SCT](CHAP_Converting.App.md)\.

## Privileges for PostgreSQL as a target database<a name="CHAP_Source.Oracle.ToPostgreSQL.ConfigureTarget"></a>

To use PostgreSQL as a target, AWS SCT requires the `CREATE ON DATABASE` privilege\. Make sure that you grant this privilege for each target PostgreSQL database\.

To use the converted public synonyms, change the database default search path to `"$user", public_synonyms, public`\.

You can use the following code example to create a database user and grant the privileges\.

```
CREATE ROLE user_name LOGIN PASSWORD 'your_password';
GRANT CREATE ON DATABASE db_name TO user_name;
ALTER DATABASE db_name SET SEARCH_PATH = "$user", public_synonyms, public;
```

In the preceding example, replace *user\_name* with the name of your user\. Then, replace *db\_name* with the name of your target database\. Finally, replace *your\_password* with a secure password\.

To use Amazon RDS for PostgreSQL as a target, AWS SCT requires the `rds_superuser` privilege\.

In PostgreSQL, only the schema owner or a `superuser` can drop a schema\. The owner can drop a schema and all objects that this schema includes even if the owner of the schema doesn't own some of its objects\.

When you use different users to convert and apply different schemas to your target database, you can get an error message when AWS SCT can't drop a schema\. To avoid this error message, use the `superuser` role\. 

## Oracle to PostgreSQL conversion settings<a name="CHAP_Source.Oracle.ToPostgreSQL.ConversionSettings"></a>

To edit Oracle to PostgreSQL conversion settings, choose **Settings** in AWS SCT, and then choose **Conversion settings**\. From the upper list, choose **Oracle**, and then choose **Oracle – PostgreSQL**\. AWS SCT displays all available settings for Oracle to PostgreSQL conversion\.

Oracle to PostgreSQL conversion settings in AWS SCT include options for the following:
+ To limit the number of comments with action items in the converted code\.

  For **Add comments in the converted code for the action items of selected severity and higher**, choose the severity of action items\. AWS SCT adds comments in the converted code for action items of the selected severity and higher\.

  For example, to minimize the number of comments in your converted code, choose **Errors only**\. To include comments for all action items in your converted code, choose **All messages**\.
+ To allow AWS SCT to convert Oracle materialized views to tables or materialized views on PostgreSQL\. For **Materialized view conversion as**, choose how to convert your source materialized views\.
+ To work with your source Oracle code when it includes the `TO_CHAR`, `TO_DATE`, and `TO_NUMBER` functions with parameters that PostgreSQL doesn't support\. By default, AWS SCT emulates the usage of these parameters in the converted code\.

  When your source Oracle code includes only parameters that PostgreSQL supports, you can use native PostgreSQL `TO_CHAR`, `TO_DATE`, and `TO_NUMBER` functions\. In this case, the converted code works faster\. To include only these parameters, select the following values:
  + **Function TO\_CHAR\(\) does not use Oracle specific formatting strings**
  + **Function TO\_DATE\(\) does not use Oracle specific formatting strings**
  + **Function TO\_NUMBER\(\) does not use Oracle specific formatting strings**
+ To address when your source Oracle database stores only integer values in the primary or foreign key columns of the `NUMBER` data type, AWS SCT can convert these columns to the `BIGINT` data type\. This approach improves the performance of your converted code\. To take this approach, select **Convert NUMBER primary / foreign key columns to BIGINT ones**\. Make sure that your source doesn't include floating point values in these columns to avoid data loss\.
+ To skip deactivated triggers and constraints in your source code\. To do so, choose **Ignore disabled triggers and constraints**\.
+ To use AWS SCT to convert string variables that are called as dynamic SQL\. Your database code can change the values of these string variables\. To make sure that AWS SCT always converts the latest value of this string variable, select **Convert the dynamic SQL code that is created in called routines**\.
+ To address that PostgreSQL version 10 and earlier don't support procedures\. If you or your users aren't familiar with using procedures in PostgreSQL, AWS SCT can convert Oracle procedures to PostgreSQL functions\. To do so, select **Convert procedures to functions**\.
+ To see additional information about the occurred action items\. To do so, you can add specific functions to the extension pack by selecting **Add on exception raise block for migration issues with the next severity levels**\. Then choose severity levels to raise user\-defined exceptions\.
+ To work with a source Oracle database that might include constraints with the automatically generated names\. If your source code uses these names, make sure that you select **Convert the system generated constraint names using the source original names**\. If your source code uses these constraints but doesn't use their names, clear this option to increase the conversion speed\.
+ To address whether your database and applications run in different time zones\. By default, AWS SCT emulates time zones in the converted code\. However, you don't need this emulation when your database and applications use the same time zone\. In this case, select **Time zone on the client side matches the time zone on server**\.
+ To address whether your source and target databases run in different time zones\. If they do, the function that emulates the `SYSDATE` built\-in Oracle function returns different values compared to the source function\. To make sure that your source and target functions return the same values, choose **Set default time zone for SYSDATE emulation**\.
+ To use the functions from the orafce extension in your converted code\. To do so, for **Use orafce implementation**, select the functions to use\. For more information about orafce, see [orafce](https://github.com/orafce/orafce) on GitHub\.

## Converting Oracle sequences<a name="CHAP_Source.Oracle.ToPostgreSQL.ConvertSequences"></a>

AWS SCT converts sequences from Oracle to PostgreSQL\. If you use sequences to maintain integrity constraints, make sure that the new values of a migrated sequence don't overlap the existing values\.

**To populate converted sequences with the last value from the source database**

1. Open your AWS SCT project with Oracle as the source\.

1. Choose **Settings**, and then choose **Conversion settings**\. 

1. From the upper list, choose **Oracle**, and then choose **Oracle – PostgreSQL**\. AWS SCT displays all available settings for Oracle to PostgreSQL conversion\. 

1. Choose **Populate converted sequences with the last value generated on the source side**\.

1. Choose **OK** to save the settings and close the **Conversion settings** dialog box\. 

## Converting Oracle ROWID<a name="CHAP_Source.Oracle.ToPostgreSQL.ConvertRowID"></a>

 In an Oracle database, the ROWID pseudocolumn contains the address of the table row\. The ROWID pseudocolumn is unique to Oracle, so AWS SCT converts the ROWID pseudocolumn to a data column on PostgreSQL\. By using this conversion, you can keep the ROWID information\. 

When converting the ROWID pseudocolumn, AWS SCT can create a data column with the `bigint` data type\. If no primary key exists, AWS SCT sets the ROWID column as the primary key\. If a primary key exists, AWS SCT sets the ROWID column with a unique constraint\.

If your source database code includes operations with ROWID, which you can't run using a numeric data type, AWS SCT can create a data column with the `character varying` data type\.

**To create a data column for Oracle ROWID for a project**

1. Open your AWS SCT project with Oracle as the source\.

1. Choose **Settings**, and then choose **Conversion settings**\. 

1. From the upper list, choose **Oracle**, and then choose **Oracle – PostgreSQL**\. AWS SCT displays all available settings for Oracle to PostgreSQL conversion\. 

1. For **Generate row ID**, do one of the following: 
   + Choose **Generate as identity** to create a numeric data column\.
   + Choose **Generate as character domain type** to create a character data column\.

1. Choose **OK** to save the settings and close the **Conversion settings** dialog box\. 

## Converting Oracle dynamic SQL<a name="CHAP_Source.Oracle.ToPostgreSQL.DynamicSQL"></a>

 Oracle provides two ways to implement dynamic SQL: using an EXECUTE IMMEDIATE statement or calling procedures in the DBMS\_SQL package\. If your source Oracle database includes objects with dynamic SQL, use AWS SCT to convert Oracle dynamic SQL statements to PostgreSQL\.

**To convert Oracle dynamic SQL to PostgreSQL**

1. Open your AWS SCT project with Oracle as the source\.

1. Choose a database object that uses dynamic SQL in the Oracle source tree view\.

1. Open the context \(right\-click\) menu for the object, choose **Convert schema**, and agree to replace the objects if they exist\. The following screenshot shows the converted procedure below the Oracle procedure with dynamic SQL\.  
![\[Dynamic SQL conversion\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/dynamicsql1.png)

## Converting Oracle partitions<a name="CHAP_Source.Oracle.ToPostgreSQL.PG10Partitioning"></a>

AWS SCT currently supports the following partitioning methods: 
+ Range
+ List
+ Multicolumn range
+ Hash
+ Composite \(list\-list, range\-list, list\-range, list\-hash, range\-hash, hash\-hash\)