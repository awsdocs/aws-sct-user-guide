# Converting Db2 LUW to Amazon RDS for PostgreSQL or Amazon Aurora PostgreSQL\-Compatible Edition<a name="CHAP_Source.DB2LUW.ToPostgreSQL"></a>

When you migrate IBM Db2 LUW to PostgreSQL, AWS SCT can convert various trigger statements used with Db2 LUW\. These trigger statements include the following:
+ **Trigger events** – INSERT, DELETE, and UPDATE trigger events specify that the triggered action runs whenever the event is applied to the subject table or subject view\. You can specify any combination of the INSERT, DELETE, and UPDATE events, but you can specify each event only once\. AWS SCT supports single and multiple trigger events\. For events, PostgreSQL has practically the same functionality\. 
+ **Event OF COLUMN** – You can specify a column name from a base table\. The trigger is activated only by the update of a column that is identified in the column\-name list\. PostgreSQL has the same functionality\.
+ **Statement triggers** – These specify that the triggered action is applied only once for the whole statement\. You can’t specify this type of trigger granularity for a BEFORE trigger or an INSTEAD OF trigger\. If specified, an UPDATE or DELETE trigger is activated, even if no rows are affected\. PostgreSQL also has this functionality and trigger declaration for statement triggers is identical for PostgreSQL and Db2 LUW\.
+ **Referencing clauses** – These specify the correlation names for transition variables and the table names for transition tables\. Correlation names identify a specific row in the set of rows affected by the triggering SQL operation\. Table names identify the complete set of affected rows\. Each row affected by a triggering SQL operation is available to the triggered action by qualifying columns with specified correlation\-names\. PostgreSQL doesn’t support this functionality, and only uses a NEW or OLD correlation name\.
+ **INSTEAD OF triggers** – AWS SCT supports these\.

## Converting Db2 LUW partitioned tables to PostgreSQL version 10 partitioned tables<a name="CHAP_Source.DB2LUW.ToPostgreSQL.PartitionedTables"></a>

AWS SCT can convert Db2 LUW tables to partitioned tables in PostgreSQL 10\. There are several restrictions when converting a Db2 LUW partitioned table to PostgreSQL:
+ You can create a partitioned table with a nullable column in Db2 LUW, and you can specify a partition to store NULL values\. However, PostgreSQL doesn’t support NULL values for RANGE partitioning\.
+ Db2 LUW can use an INCLUSIVE or EXCLUSIVE clause to set range boundary values\. PostgreSQL only supports INCLUSIVE for a starting boundary and EXCLUSIVE for an ending boundary\. The converted partition name is in the format <original\_table\_name>\_<original\_partition\_name>\.
+ You can create primary or unique keys for partitioned tables in Db2 LUW\. PostgreSQL requires you to create primary or unique key for each partition directly\. Primary or unique key constraints must be removed from the parent table\. The converted key name is in the format <original\_key\_name>\_<original\_partition \_name>\.
+ You can create a foreign key constraint from and to a partitioned table in Db2 LUW\. However, PostgreSQL doesn’t support foreign keys references in partitioned tables\. PostgreSQL also doesn’t support foreign key references from a partitioned table to another table\.
+ You can create an index on a partitioned table in Db2 LUW\. However, PostgreSQL requires you to create an index for each partition directly\. Indexes must be removed from the parent table\. The converted index name is in the format <original\_index\_name>\_<original\_partition\_name>\.
+ You must define row triggers on individual partitions, not on the partitioned table\. Triggers must be removed from the parent table\. The converted trigger name is in the format <original\_trigger\_name>\_<original\_partition\_name>\.

## Privileges for PostgreSQL as a target<a name="CHAP_Source.DB2LUW.ToPostgreSQL.ConfigureTarget"></a>

To use PostgreSQL as a target, AWS SCT requires the `CREATE ON DATABASE` privilege\. Make sure that you grant this privilege for each target PostgreSQL database\.

To use the converted public synonyms, change the database default search path to `"$user", public_synonyms, public`\.

You can use the following code example to create a database user and grant the privileges\.

```
CREATE ROLE user_name LOGIN PASSWORD 'your_password';
GRANT CREATE ON DATABASE db_name TO user_name;
ALTER DATABASE db_name SET SEARCH_PATH = "$user", public_synonyms, public;
```

In the example preceding, replace *user\_name* with the name of your user\. Then, replace *db\_name* with the name of your target Amazon Redshift database\. Finally, replace *your\_password* with a secure password\.

In PostgreSQL, only the schema owner or a `superuser` can drop a schema\. The owner can drop a schema and all objects that this schema includes even if the owner of the schema doesn't own some of its objects\.

When you use different users to convert and apply different schemas to your target database, you can get an error message when AWS SCT can't drop a schema\. To avoid this error message, use the `superuser` role\. 