# Using Teradata as a source for AWS SCT<a name="CHAP_Source.Teradata"></a>

You can use AWS SCT to convert schemas, code objects, and application code from Teradata to Amazon Redshift or Amazon Redshift and AWS Glue used in combination\.

## Privileges for Teradata as a source<a name="CHAP_Source.Teradata.Permissions"></a>

The following privileges are required for using Teradata as a source:
+ SELECT ON DBC 
+ SELECT ON SYSUDTLIB 
+ SELECT ON SYSLIB 
+ SELECT ON *<source\_database>* 
+ CREATE PROCEDURE ON *<source\_database>* 

In the preceding example, replace the *<source\_database>* placeholder with the name of the source database\.

AWS SCT requires the CREATE PROCEDURE privilege to perform HELP PROCEDURE against all procedures in the source database\. AWS SCT doesn't use this privilege to create any new objects in your source Teradata database\.

## Connecting to Teradata as a source<a name="CHAP_Source.Teradata.Connecting"></a>

Use the following procedure to connect to your Teradata source database with the AWS Schema Conversion Tool\. 

**To connect to a Teradata source database**

1. In the AWS Schema Conversion Tool, choose **Add source**\. 

1. Choose **Teradata**, then choose **Next**\. 

   The **Add source** dialog box appears\.

1. For **Connection name**, enter a name for your database\. AWS SCT displays this name in the tree in the left panel\. 

1. Use database credentials from AWS Secrets Manager or enter them manually:
   + To use database credentials from Secrets Manager, use the following instructions:

     1. For **AWS Secret**, choose the name of the secret\.

     1. Choose **Populate** to automatically fill in all values in the database connection dialog box from Secrets Manager\.

     For information about using database credentials from Secrets Manager, see [Using AWS Secrets Manager](CHAP_UserInterface.md#CHAP_UserInterface.SecretsManager)\.
   + To enter the Teradata source database connection information manually, use the following instructions:  
****    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/CHAP_Source.Teradata.html)

1. Choose **Test Connection** to verify that AWS SCT can connect to your source database\. 

1. Choose **Connect** to connect to your source database\.

### Using LDAP authentication with a Teradata source<a name="CHAP_Source.Teradata.Connecting.LDAP"></a>

To set up Lightweight Directory Access Protocol \(LDAP\) authentication for Teradata users who run Microsoft Active Directory in Windows, use the following procedure\. 

In the following procedure, the Active Directory domain is `test.local.com`\. The Windows server is `DC`, and it's configured with default settings\. The following script creates the `test_ldap` Active Directory account, and this account uses the `test_ldap` password\.

**To set up LDAP authentication for Teradata users who run Microsoft Active Directory in Windows**

1. In the `/opt/teradata/tdat/tdgss/site` directory, edit the file `TdgssUserConfigFile.xml` \. Change the LDAP section to the following\.

   ```
   AuthorizationSupported="no"
   
   LdapServerName="DC.test.local.com"
   LdapServerPort="389"
   LdapServerRealm="test.local.com"
   LdapSystemFQDN="dc= test, dc= local, dc=com"
   LdapBaseFQDN="dc=test, dc=local, dc=com"
   ```

1. Apply the changes by running the configuration as follows\.

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

If you change the user password in Active Directory for your LDAP user, specify this new password during connection to Teradata in LDAP mode\. In DEFAULT mode, you connect to Teradata by using the LDAP user name and any password\.

## Configuring statistics collection in your source Teradata data warehouse<a name="CHAP_Source.Teradata.ConfigureStatistics"></a>

To convert your source Teradata data warehouse, AWS SCT uses statistics to optimize your converted Amazon Redshift data warehouse\. You can collect statistics in AWS SCT or upload the statistics file\. For more information, see [Collecting or uploading statistics](CHAP_Converting.DW.md#CHAP_Converting.DW.Statistics)\.

To make sure that AWS SCT can collect statistics from your data warehouse, complete the following prerequisite tasks\.

**To collect statistics from your Teradata data warehouse**

1. Run the following query to recollect statistics for all tables in your data warehouse\.

   ```
   collect summary statistics on table_name;
   ```

   In the preceding example, replace *table\_name* with the name of your source table\. Repeat the query for each table that you convert\.

1. Run the following query to determine the account string for the user, which you use to convert your data warehouse\.

   ```
   select * from dbc.accountinfo where username ='user_name'
   ```

1. Turn on query logging for a specific user using the account string from the previous example\.

   ```
   BEGIN QUERY LOGGING WITH OBJECTS, SQL ON ALL ACCOUNT=('$M$BUSI$S$D$H');
   ```

   Alternatively, turn on query logging for all database users\.

   ```
   BEGIN QUERY LOGGING WITH SQL, OBJECTS LIMIT SQLTEXT=0 ON ALL;
   ```

After you complete collecting data warehouse statistics, turn off query logging\. To do so, you can use the following code example\.

```
end query logging with explain, objects, sql on all account=(' $M$BUSI$S$D$H');
```

## Collecting statistics in an offline mode from your source Teradata data warehouse<a name="CHAP_Source.Teradata.CollectStatistics"></a>

After you configure the statistics collection in your Teradata data warehouse, you can collect statistics in your AWS SCT project\. Alternatively, you can use Basic Teradata Query \(BTEQ\) scripts to collect statistics in an offline mode\. Then, you can upload the files with collected statistics to your AWS SCT project\. For more information, see [Collecting or uploading statistics](CHAP_Converting.DW.md#CHAP_Converting.DW.Statistics)\.

**To collect statistics from your Teradata data warehouse in an offline mode**

1. Create the `off-line_stats.bteq` script with the following content\.

   ```
   .OS IF EXIST column-stats-tera.csv del /F column-stats-tera.csv
   .OS IF EXIST table-stats-tera.csv del /F table-stats-tera.csv
   .OS IF EXIST column-skew-script-tera.csv del /F column-skew-script-tera.csv
   .OS IF EXIST column-skew-stats-tera.csv del /F column-skew-stats-tera.csv
   .OS IF EXIST query-stats-tera.csv  del /F query-stats-tera.csv
   .LOGON your_teradata_server/your_login, your_password
   .EXPORT REPORT FILE = table-stats-tera.csv
   .SET TITLEDASHES OFF
   .SET WIDTH 10000
   
   SELECT
       '"' || OREPLACE(COALESCE(c.DatabaseName, ''), '"', '""') || '";' ||
       '"' || OREPLACE(COALESCE(c.TableName, ''), '"', '""') || '";' ||
       '"' || TRIM(COALESCE(s.reference_count, '0')) || '";' ||
       '"' || TRIM(COALESCE(CAST(p.RowCount AS BIGINT), '0')) || '";' ||
       '"' || CAST(CAST(w.size_in_mb AS DECIMAL (38,1) FORMAT 'Z9.9') AS VARCHAR(38)) || '";' ||
       '"' || TRIM(COALESCE(r.stat_fk_dep_count, '0')) || '";' ||
       '"' || CAST(CAST(current_timestamp(0) as timestamp(0) format 'YYYY-MM-DDBHH:MI:SS') as VARCHAR(19)) || '"'
   (TITLE '"database_name";"table_name";"reference_count";"row_count";"size_in_mb";"stat_fk_dep_count";"current_ts"')
   FROM (select databasename, tablename
           from DBC.tablesv
           where tablekind IN ('T','O')
           and databasename = 'your_database_name'
            ) c
   left join
           (select DatabaseName, TableName, max(RowCount) RowCount
           from dbc.tableStatsv
           group by 1,2)p
   on p.databasename = c.databasename
   and p.tablename = c.tablename
   left join
           (SELECT r.ChildDB as DatabaseName,
           r.ChildTable as TableName,
           COUNT(DISTINCT r.ParentTable) reference_count
           FROM DBC.All_RI_ChildrenV r
           GROUP BY r.ChildDB, r.ChildTable) s
   on s.databasename = c.databasename
   and s.tablename = c.tablename
   left join
           (SELECT r.ParentDB as DatabaseName,
           r.ParentTable as TableName,
           COUNT(DISTINCT r.ChildTable) stat_fk_dep_count
           FROM DBC.All_RI_ParentsV r
           GROUP BY r.ParentDB, r.ParentTable) r
   on r.databasename = c.databasename
   and r.tablename = c.tablename
   left join
           (select databasename, tablename,
           sum(currentperm)/1024/1024 as size_in_mb
           from dbc.TableSizeV
           group by 1,2) w
   on w.databasename = c.databasename
   and w.tablename = c.tablename
   WHERE COALESCE(r.stat_fk_dep_count,0) + COALESCE(CAST(p.RowCount AS BIGINT),0) + COALESCE(s.reference_count,0) > 0;
   
   .EXPORT RESET
   
   .EXPORT REPORT FILE = column-stats-tera.csv
   .SET TITLEDASHES OFF
   .SET WIDTH 10000
       '"' || TRIM(COALESCE(CAST(t2.card AS BIGINT), '0')) || '";' ||
   
   SELECT
   	'"' || OREPLACE(COALESCE(trim(tv.DatabaseName), ''), '"', '""') || '";' ||
       	'"' || OREPLACE(COALESCE(trim(tv.TableName), ''), '"', '""') || '";' ||
   	'"' || OREPLACE(COALESCE(trim(tv.columnname), ''), '"', '""') || '";' ||
                            '"' || TRIM(COALESCE(CAST(t2.card AS BIGINT), '0')) || '";' ||
   
   	'"' || CAST(current_timestamp AS VARCHAR(19)) || '"' (TITLE '"database_name";"table_name";"column_name";"cardinality";"current_ts"')
   FROM dbc.columnsv tv
   LEFT JOIN
   (
   	SELECT
   		c.DatabaseName	AS DATABASE_NAME,
   		c.TABLENAME 	AS TABLE_NAME,
   		c.ColumnName	AS COLUMN_NAME,
   		c.UniqueValueCount	AS CARD
   	FROM dbc.tablestatsv c
   	WHERE c.DatabaseName = 'your_database_name'
   	AND c.RowCount <> 0
   ) t2
   ON tv.DATABASENAME = t2.DATABASE_NAME
   AND tv.TABLENAME = t2.TABLE_NAME
   AND tv.COLUMNNAME = t2.COLUMN_NAME
   WHERE t2.card > 0;
   
   .EXPORT RESET
   
   .EXPORT REPORT FILE = column-skew-script-tera.csv
   .SET TITLEDASHES OFF
   .SET WIDTH 10000
   
   SELECT
   'SELECT CAST(''"' || TRIM(c.DatabaseName) || '";"' || TRIM(c.TABLENAME)  || '";"' || TRIM(c.COLUMNNAME) || '";"'' ||
   TRIM(CAST(COALESCE(MAX(cnt) * 1.0 / SUM(cnt), 0) AS NUMBER FORMAT ''9.9999'')) || ''";"'' ||
   CAST(CURRENT_TIMESTAMP(0) AS VARCHAR(19)) || ''"'' AS VARCHAR(512))
   AS """DATABASE_NAME"";""TABLE_NAME"";""COLUMN_NAME"";""SKEWED"";""CURRENT_TS"""
   FROM(
   SELECT	COUNT(*) AS cnt
   FROM "' || c.DATABASENAME || '"."' || c.TABLENAME ||
   '" GROUP BY "' || c.COLUMNNAME || '") t' ||
   	CASE WHEN ROW_NUMBER() OVER(PARTITION BY c.DATABASENAME
   	ORDER BY c.TABLENAME DESC, c.COLUMNNAME DESC) <> 1
   	THEN ' UNION ALL'
   	ELSE ';' END (TITLE '--SKEWED--')
   FROM	dbc.columnsv c
   INNER JOIN
   (SELECT databasename, TABLENAME
   FROM dbc.tablesv  WHERE tablekind = 'T'
   AND 	databasename = 'your_database_name') t
   ON t.databasename = c.databasename
   AND t.TABLENAME = c.TABLENAME
   INNER JOIN
   (SELECT databasename, TABLENAME, columnname FROM  dbc.indices GROUP BY 1,2,3
   WHERE  TRANSLATE_CHK (databasename USING LATIN_TO_UNICODE) + TRANSLATE_CHK (TABLENAME USING LATIN_TO_UNICODE) + TRANSLATE_CHK (columnname USING LATIN_TO_UNICODE) = 0
   ) i
   ON i.databasename = c.databasename
   AND i.TABLENAME = c.TABLENAME
   AND i.columnname = c.columnname
   WHERE c.ColumnType NOT IN ('CO','JN','N','++','VA','UT','AN','XM','A1','BO')
   ORDER BY c.TABLENAME, c.COLUMNNAME;
   
   .EXPORT RESET
   
   .EXPORT REPORT FILE = column-skew-stats-tera.csv
   .SET TITLEDASHES OFF
   .SET WIDTH 10000
   
   .RUN FILE = column-skew-script-tera.csv
   
   .EXPORT RESET
   
   .EXPORT REPORT FILE = query-stats-tera.csv
   .SET TITLEDASHES OFF
   .SET WIDTH 32000
   
   SELECT
     '"' || RTRIM(CAST(SqlTextInfo AS VARCHAR(31900)), ';') || '";"' ||
     TRIM(QueryCount) || '";"' ||
     TRIM(QueryId) || '";"' ||
     TRIM(SqlRowNo) || '";"' ||
     TRIM(QueryParts) || '";"' ||
     CAST(CURRENT_TIMESTAMP(0) AS VARCHAR(19)) || '"'
   (TITLE '"query_text";"query_count";"query_id";"sql_row_no";"query_parts";"current_ts"')
     FROM
     (
       SELECT  QueryId,  SqlTextInfo, SqlRowNo, QueryParts, QueryCount,
       SUM(QueryFirstRow) OVER (ORDER BY QueryCount DESC, QueryId ASC, SqlRowNo ASC
       ROWS UNBOUNDED PRECEDING) AS topN
       FROM
       (SELECT QueryId,  SqlTextInfo, SqlRowNo, QueryParts, QueryCount,
         CASE WHEN
         ROW_NUMBER() OVER (PARTITION BY QueryCount, SqlTextInfo ORDER BY QueryId, SqlRowNo) = 1 AND SqlRowNo = 1
       THEN 1 ELSE 0 END AS QueryFirstRow
       FROM (
         SELECT q.QueryId,  q.SqlTextInfo, q.SqlRowNo,
         MAX(q.SqlRowNo) OVER (PARTITION BY q.QueryId) QueryParts,
         COUNT(q.SqlTextInfo) OVER (PARTITION BY q.SqlTextInfo) QueryCount
         FROM DBC.dbqlsqltbl q
         INNER JOIN
         (
           SELECT QueryId
           FROM DBC.DBQLogTbl t
           WHERE TRIM(t.StatementType) IN ('SELECT')
           AND TRIM(t.AbortFlag) = '' AND t.ERRORCODE = 0
           AND 	(CASE WHEN 'All users' IN ('All users') THEN 'All users' ELSE TRIM(t.USERNAME) END) IN ('All users') --user_name list
           AND t.StartTime > CURRENT_TIMESTAMP - INTERVAL '30' DAY
           GROUP BY 1
         ) t
         ON q.QueryId = t.QueryId
         INNER JOIN
         (
           SELECT QueryId
           FROM DBC.QryLogObjectsV
           WHERE ObjectDatabaseName = 'your_database_name'
           AND ObjectType = 'Tab'
           AND CollectTimeStamp > CURRENT_TIMESTAMP - INTERVAL '30' DAY
           GROUP BY 1
         ) r
         ON r.QueryId = t.QueryId
         WHERE q.CollectTimeStamp > CURRENT_TIMESTAMP - INTERVAL '30' DAY
       ) t
     ) t
     WHERE SqlTextInfo NOT LIKE '%";"%'
     ) q
     WHERE
     QueryParts >=1
     AND topN <= 50
     ORDER BY QueryCount DESC, QueryId, SqlRowNo
     QUALIFY COUNT(QueryId) OVER (PARTITION BY QueryId) = QueryParts;
   
   .EXPORT RESET
   
   .LOGOFF
   
   .QUIT
   ```

1. Create the `td_run_bteq.bat` file that runs the BTEQ script that you created in the previous step\. Use the following content for this file\.

   ```
   @echo off > off-line_stats1.bteq & setLocal enableDELAYedexpansion
   @echo off > off-line_stats2.bteq & setLocal enableDELAYedexpansion
   
   set old1=your_teradata_server
   set new1=%1
   set old2=your_login
   set new2=%2
   set old3=your_database_name
   set new3=%3
   set old4=your_password
   set /p new4=Input %2 pass?
   
   for /f "tokens=* delims= " %%a in (off-line_stats.bteq) do (
   set str1=%%a
   set str1=!str1:%old1%=%new1%!
   >> off-line_stats1.bteq echo !str1!
   )
   
   for /f "tokens=* delims= " %%a in (off-line_stats1.bteq) do (
   set str2=%%a
   set str2=!str2:%old2%=%new2%!
   >> off-line_stats2.bteq echo !str2!
   )
   
   type nul > off-line_stats1.bteq
   
   for /f "tokens=* delims= " %%a in (off-line_stats2.bteq) do (
   set str3=%%a
   set str3=!str3:%old3%=%new3%!
   >> off-line_stats1.bteq echo !str3!
   )
   
   type nul > off-line_stats2.bteq
   
   for /f "tokens=* delims= " %%a in (off-line_stats1.bteq) do (
   set str4=%%a
   set str4=!str4:%old4%=%new4%!
   >> off-line_stats2.bteq echo !str4!
   )
   
   del .\off-line_stats1.bteq
   
   echo export starting...
   
   bteq -c UTF8 < off-line_stats.bteq > metadata_export.log
   
   pause
   ```

1. Create the `runme.bat` file that runs the batch file that you created in the previous step\. Use the following content for this file\.

   ```
   .\td_run_bteq.bat ServerName UserName DatabaseName
   ```

   In the `runme.bat` file, replace *ServerName*, *UserName*, and *DatabaseName* with your applicable values\.

   Then, run the `runme.bat` file\. Repeat this step for each data warehouse that you convert to Amazon Redshift\.

After you run this script, you receive three files with statistics for each database\. You can upload these files to your AWS SCT project\. To do so, choose your data warehouse from the left panel of your project, and open the context \(right\-click\) menu\. Choose **Upload Statistics**\.

## Teradata to Amazon Redshift conversion settings<a name="CHAP_Source.Teradata.ConversionSettings"></a>

To edit Teradata to Amazon Redshift conversion settings, choose **Settings** in AWS SCT, and then choose **Conversion settings**\. From the upper list, choose **Teradata**, and then choose **Teradata – Amazon Redshift**\. AWS SCT displays all available settings for Teradata to Amazon Redshift conversion\.

Teradata to Amazon Redshift conversion settings in AWS SCT include options for the following:
+ To limit the number of comments with action items in the converted code\.

  For **Add comments in the converted code for the action items of selected severity and higher**, choose the severity of action items\. AWS SCT adds comments in the converted code for action items of the selected severity and higher\.

  For example, to minimize the number of comments in your converted code, choose **Errors only**\. To include comments for all action items in your converted code, choose **All messages**\.
+ To set the maximum number of tables that AWS SCT can apply to your target Amazon Redshift cluster\.

  For **The maximum number of tables for the target Amazon Redshift cluster**, choose the number of tables that AWS SCT can apply to your Amazon Redshift cluster\.

  Amazon Redshift has quotas that limit the use tables for different cluster node types\. If you choose **Auto**, AWS SCT determines the number of tables to apply to your target Amazon Redshift cluster depending on the node type\. Optionally, choose the value manually\. For more information, see [Quotas and limits in Amazon Redshift](https://docs.aws.amazon.com/redshift/latest/mgmt/amazon-redshift-limits.html) in the *Amazon Redshift Cluster Management Guide*\.

  AWS SCT converts all your source tables, even if this is more than your Amazon Redshift cluster can store\. AWS SCT stores the converted code in your project and doesn't apply it to the target database\. If you reach the Amazon Redshift cluster quota for the tables when you apply the converted code, then AWS SCT displays a warning message\. Also, AWS SCT applies tables to your target Amazon Redshift cluster until the number of tables reaches the limit\.
+ To migrate partitions of the source table to separate tables in Amazon Redshift\. To do so, select **Use the UNION ALL view** and enter the maximum number of target tables that AWS SCT can create for a single source table\.

  Amazon Redshift doesn't support table partitioning\. To emulate this behavior and make queries run faster, AWS SCT can migrate each partition of your source table to a separate table in Amazon Redshift\. Then, AWS SCT creates a view that includes data from all these tables\.

  AWS SCT automatically determines the number of partitions in your source table\. Depending on the type of source table partitioning, this number can exceed the quota for the tables that you can apply to your Amazon Redshift cluster\. To avoid reaching this quota, enter the maximum number of target tables that AWS SCT can create for partitions of a single source table\. The default option is 368 tables, which represents a partition for 366 days of a year and two tables for `NO RANGE` and `UNKNOWN` partitions\.
+ To apply compression to Amazon Redshift table columns\. To do so, select **Use compression encoding**\.

  AWS SCT assigns compression encoding to columns automatically using the default Amazon Redshift algorithm\. For more information, see [Compression encodings](https://docs.aws.amazon.com/redshift/latest/dg/c_Compression_encodings.html) in the *Amazon Redshift Database Developer Guide*\.

  By default, Amazon Redshift doesn't apply compression to columns that are defined as sort and distribution keys\. You can change this behavior and apply compression to these columns\. To do so, select **Use compression encoding for KEY columns**\. You can select this option only when you select the **Use compression encoding** option\.
+ To use an explicit list of columns in converted code for `SELECT *` statements, select **Use explicit column declaration**\.
+ To emulate the behavior of primary and unique keys in your Amazon Redshift cluster, select **Emulate the behavior of primary and unique keys**\.

  Amazon Redshift doesn't enforce unique and primary keys and uses them for informational purposes only\. If you use these constraints in your code, then make sure that AWS SCT emulates their behavior in the converted code\.
+ To ensure data uniqueness in the target Amazon Redshift tables\. To do so, select **Emulate the behavior of SET tables**\.

  Teradata creates tables using the `SET` syntax element as a default option\. You can't add duplicate rows in a `SET` table\. If your source code doesn't use this uniqueness constraint, then turn off this option\. In this case, the converted code works faster\.

  If your source code uses the `SET` option in tables as a uniqueness constraint, turn on this option\. In this case, AWS SCT rewrites `INSERT..SELECT` statements in the converted code to emulate the behavior of your source database\.

## Teradata to Amazon Redshift conversion optimization settings<a name="CHAP_Source.Teradata.ConversionOptimizationSettings"></a>

To edit Teradata to Amazon Redshift conversion optimization settings, choose **Settings** in AWS SCT, and then choose **Conversion settings**\. From the upper list, choose **Teradata**, and then choose **Teradata – Amazon Redshift**\. In the left pane, choose **Optimization strategies**\. AWS SCT displays conversion optimization settings for Teradata to Amazon Redshift conversion\.

Teradata to Amazon Redshift conversion optimization settings in AWS SCT include options for the following:
+ To work with automatic table optimization\. To do so, select **Use Amazon Redshift automatic table tuning**\.

  Automatic table optimization is a self\-tuning process in Amazon Redshift that automatically optimizes the design of tables\. For more information, see [Working with automatic table optimization](https://docs.aws.amazon.com/redshift/latest/dg/t_Creating_tables.html) in the *Amazon Redshift Database Developer Guide*\.

  To rely only on the automatic table optimization, choose **None** for **Initial key selection strategy**\.
+ To choose sort and distribution keys using your strategy\.

  You can choose sort and distribution keys using Amazon Redshift metadata, statistical information, or both these options\. For **Initial key selection strategy** on the **Optimization strategies** tab, choose one of the following options:
  + Use metadata, ignore statistical information
  + Ignore metadata, use statistical information
  + Use metadata and statistical information

  Depending on the option that you choose, you can select optimization strategies\. Then, for each strategy, enter the value \(0–100\)\. These values define the weight of each strategy\. Using these weight values, AWS SCT defines how each rule influences on the choice of distribution and sort keys\. The default values are based on the AWS migration best practices\.

  You can define the size of small tables for the **Find small tables** strategy\. For **Min table row count** and **Max table row count**, enter the minimum and maximum number of rows in a table to define it as a small table\. AWS SCT applies the `ALL` distribution style to small tables\. In this case, a copy of the entire table is distributed to every node\.
+ To configure strategy details\.

  In addition to defining the weight for each optimization strategy, you can configure the optimization settings\. To do so, choose **Conversion optimization**\. 
  + For **Sort key columns limit**, enter the maximum number of columns in the sort key\.
  + For **Skewed threshold value**, enter the percentage \(0–100\) of a skewed value for a column\. AWS SCT excludes columns with the skew value greater than the threshold from the list of candidates for the distribution key\. AWS SCT defines the skewed value for a column as the percentage ratio of the number of occurrences of the most common value to the total number of records\.
  + For **Top N queries from the query history table**, enter the number \(1–100\) of the most frequently used queries to analyze\.
  + For **Select statistics user**, choose the database user for which you want to analyze the query statistics\.

  Also, on the **Optimization strategies** tab, you can define the size of small tables for the **Find small tables** strategy\. For **Min table row count** and **Max table row count**, enter the minimum and maximum number of rows in a table to consider it as a small table\. AWS SCT applies the `ALL` distribution style to small tables\. In this case, a copy of the entire table is distributed to every node\.