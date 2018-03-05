# Required Database Privileges for Using the AWS Schema Conversion Tool<a name="CHAP_SchemaConversionTool.GettingStarted.Privs"></a>

When you use the AWS Schema Conversion Tool \(AWS SCT\) to convert your database schema, you need certain privileges for the source and target databases\. Following, you can find lists of these privileges\. 

+ [Source: Amazon Redshift](#GettingStarted.Privs.Sources.Redshift)

+ [Source: Greenplum](#GettingStarted.Privs.Sources.Greenplum)

+ [Source: Microsoft SQL Server](#GettingStarted.Privs.Sources.MSSQL)

+ [Source: Microsoft SQL Server Data Warehouse](#GettingStarted.Privs.Sources.MSSQLDW)

+ [Source: MySQL](#GettingStarted.Privs.Sources.MySQL)

+ [Source: Netezza](#GettingStarted.Privs.Sources.Netezza)

+ [Source: Oracle](#GettingStarted.Privs.Sources.Oracle)

+ [Source: Oracle Data Warehouse](#GettingStarted.Privs.Sources.OracleDW)

+ [Source: PostgreSQL](#GettingStarted.Privs.Sources.PostgreSQL)

+ [Source: Teradata](#GettingStarted.Privs.Sources.Teradata)

+ [Source: Vertica](#GettingStarted.Privs.Sources.Vertica)

+ [Target: Amazon Aurora \(MySQL\)](#GettingStarted.Privs.Targets.AuroraMySQL)

+ [Target: Amazon Aurora \(PostgreSQL\)](#GettingStarted.Privs.Targets.AuroraPostgreSQL)

+ [Target: Amazon Redshift](#GettingStarted.Privs.Targets.Redshift)

+ [Target: Microsoft SQL Server](#GettingStarted.Privs.Targets.MSSQL)

+ [Target: MySQL](#GettingStarted.Privs.Targets.MySQL)

+ [ Target: Oracle](#GettingStarted.Privs.Targets.Oracle)

+ [Target: PostgreSQL](#GettingStarted.Privs.Targets.PostgreSQL)

## Privileges for Amazon Redshift as a Source Database<a name="GettingStarted.Privs.Sources.Redshift"></a>

The privileges required for Amazon Redshift as a source are listed following: 

+ USAGE ON SCHEMA *<schema\_name>* 

+ SELECT ON ALL TABLES IN SCHEMA *<schema\_name>* 

+ SELECT ON PG\_CATALOG\.PG\_STATISTIC 

+ SELECT ON SVV\_TABLE\_INFO 

+ SELECT ON TABLE STV\_BLOCKLIST 

+ SELECT ON TABLE STV\_TBL\_PERM 

## Privileges for Greenplum as a Source Database<a name="GettingStarted.Privs.Sources.Greenplum"></a>

The privileges required for Greenplum as a source are listed following: 

+ CONNECT ON DATABASE *<database\_name>* 

+ USAGE ON SCHEMA *<schema\_name>* 

## Privileges for Microsoft SQL Server as a Source Database<a name="GettingStarted.Privs.Sources.MSSQL"></a>

The privileges required for Microsoft SQL Server as a source are listed following: 

+ VIEW DEFINITION 

+ VIEW DATABASE STATE 

Repeat the grant for each database whose schema you are converting\. 

## Privileges for Microsoft SQL Server Data Warehouse as a Source Database<a name="GettingStarted.Privs.Sources.MSSQLDW"></a>

The privileges required for Microsoft SQL Server data warehouse as a source are listed following: 

+ VIEW DEFINITION 

+ VIEW DATABASE STATE 

+ SELECT ON SCHEMA :: *<schema\_name>* 

Repeat the grant for each database whose schema you are converting\. 

In addition, grant the following, and run the grant on the master database: 

+ VIEW SERVER STATE 

## Privileges for MySQL as a Source Database<a name="GettingStarted.Privs.Sources.MySQL"></a>

The privileges required for MySQL as a source are listed following: 

+ SELECT ON \*\.\* 

+ SELECT ON mysql\.proc 

+ SHOW VIEW ON \*\.\* 

## Privileges for Netezza as a Source Database<a name="GettingStarted.Privs.Sources.Netezza"></a>

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

## Privileges for Oracle as a Source Database<a name="GettingStarted.Privs.Sources.Oracle"></a>

The privileges required for Oracle as a source are listed following: 

+ connect 

+ select\_catalog\_role 

+ select any dictionary 

## Privileges for Oracle Data Warehouse as a Source Database<a name="GettingStarted.Privs.Sources.OracleDW"></a>

The privileges required for Oracle Data Warehouse as a source are listed following: 

+ connect 

+ select\_catalog\_role 

+ select any dictionary 

## Privileges for PostgreSQL as a Source Database<a name="GettingStarted.Privs.Sources.PostgreSQL"></a>

The privileges required for PostgreSQL as a source are listed following: 

+ CONNECT ON DATABASE *<database\_name>* 

+ USAGE ON SCHEMA *<database\_name>* 

+ SELECT ON ALL TABLES IN SCHEMA *<database\_name>* 

+ SELECT ON ALL SEQUENCES IN SCHEMA *<database\_name>* 

## Privileges for Teradata as a Source Database<a name="GettingStarted.Privs.Sources.Teradata"></a>

The privileges required for Teradata as a source are listed following: 

+ SELECT ON DBC 

## Privileges for Vertica as a Source Database<a name="GettingStarted.Privs.Sources.Vertica"></a>

The privileges required for Vertica as a source are listed following: 

+ USAGE ON SCHEMA *<schema\_name>* 

+ USAGE ON SCHEMA PUBLIC 

+ GRANT SELECT ON ALL TABLES IN SCHEMA *<schema\_name>* 

+ SELECT ON ALL SEQUENCES IN SCHEMA *<schema\_name>* 

+ EXECUTE ON ALL FUNCTIONS IN SCHEMA *<schema\_name>* 

+ EXECUTE ON PROCEDURE *<schema\_name\.procedure\_name\(procedure\_signature\)>* 

## Privileges for Amazon Aurora \(MySQL\) as a Target Database<a name="GettingStarted.Privs.Targets.AuroraMySQL"></a>

The privileges required for Amazon Aurora \(MySQL\) as a target are listed following: 

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

+ SELECT ON mysql\.proc 

If your source database is Microsoft SQL Server, grant the additional privilege INSERT,UPDATE ON AWS\_SQLSERVER\_EXT\.\* 

If your source database is Oracle, grant the additional privilege INSERT,UPDATE ON AWS\_ORACLE\_EXT\.\* 

If your source database is PostgreSQL, grant the additional privilege INSERT,UPDATE ON AWS\_POSTGRESQL\_EXT\.\* 

## Privileges for Amazon Aurora \(PostgreSQL\) as a Target Database<a name="GettingStarted.Privs.Targets.AuroraPostgreSQL"></a>

The privileges required for Amazon Aurora \(PostgreSQL\) as a target are explained following\. 

If the new schema doesn't exist yet, grant the privilege CREATE ON DATABASE *<database\_name>* 

If the new schema already exists, grant the privilege INSERT ON ALL TABLES IN SCHEMA *<schema\_name>* 

In PostgreSQL, only the owner of a schema or a superuser can drop a schema\. The owner can drop the schema, and all contained objects, even if the owner doesn't own all of the contained objects\. 

## Privileges for Amazon Redshift as a Target Database<a name="GettingStarted.Privs.Targets.Redshift"></a>

The privileges required for Amazon Redshift as a target are listed following: 

+ CREATE ON DATABASE *<database\_name>* 

+ USAGE ON LANGUAGE plpythonu 

+ SELECT ON ALL TABLES IN SCHEMA pg\_catalog 

In Amazon Redshift, only the owner of a schema or a superuser can drop a schema\. The owner can drop the schema, and all contained objects, even if the owner doesn't own all of the contained objects\. 

## Privileges for Microsoft SQL Server as a Target Database<a name="GettingStarted.Privs.Targets.MSSQL"></a>

The privileges required for Microsoft SQL Server as a target are listed following: 

+ CREATE SCHEMA 

+ CREATE TABLE 

+ CREATE VIEW 

+ CREATE TYPE 

+ CREATE DEFAULT 

+ CREATE FUNCTION 

+ CREATE PROCEDURE 

+ CREATE ASSEMBLY 

+ CREATE AGGREGATE 

+ CREATE FULLTEXT CATALOG 

## Privileges for MySQL as a Target Database<a name="GettingStarted.Privs.Targets.MySQL"></a>

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

+ SELECT ON mysql\.proc 

If your source database is Microsoft SQL Server, grant the additional privilege INSERT,UPDATE ON AWS\_SQLSERVER\_EXT\.\* 

If your source database is Oracle, grant the additional privilege INSERT,UPDATE ON AWS\_ORACLE\_EXT\.\* 

If your source database is PostgreSQL, grant the additional privilege INSERT,UPDATE ON AWS\_POSTGRESQL\_EXT\.\* 

## Privileges for Oracle as a Target Database<a name="GettingStarted.Privs.Targets.Oracle"></a>

The privileges required for Oracle as a target are listed following: 

[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/CHAP_SchemaConversionTool.GettingStarted.Privs.html)

## Privileges for PostgreSQL as a Target Database<a name="GettingStarted.Privs.Targets.PostgreSQL"></a>

The privileges required for PostgreSQL as a target are explained following\. 

If the new schema doesn't exist yet, grant the privilege CREATE ON DATABASE *<database\_name>* 

If the new schema already exists, grant the privilege INSERT ON ALL TABLES IN SCHEMA *<schema\_name>* 

In PostgreSQL, only the owner of a schema or a superuser can drop a schema\. The owner can drop the schema, and all contained objects, even if the owner doesn't own all of the contained objects\. 

## Related Topics<a name="CHAP_SchemaConversionTool.GettingStarted.Privs.Related"></a>

+ [Getting Started with the AWS Schema Conversion Tool](CHAP_SchemaConversionTool.GettingStarted.md)