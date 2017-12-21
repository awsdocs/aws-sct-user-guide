# Oracle to PostgreSQL Supported Schema Conversion<a name="CHAP_SchemaConversionTool.Reference.ConversionSupport.Oracle.PostgreSQL"></a>

The following sections list the schema elements from an Oracle database and whether they are supported for automatic conversion to PostgreSQL using the AWS Schema Conversion Tool\. 

## DDL<a name="w3ab1c37c15b5"></a>

### Statements<a name="w3ab1c37c15b5b2"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  ALTER CLUSTER  |  No  |      | 
|  ALTER DATABASE  |  No  |      | 
|  ALTER DIMENSION  |  No  |      | 
|  ALTER DISKGROUP  |  No  |      | 
|  ALTER FLASHBACK ARCHIVE  |  No  |      | 
|  ALTER FUNCTION  |  No  |      | 
|  ALTER TABLESPACE  |  No  |      | 
|  CREATE \[OR REPLACE\] FUNCTION  |  Yes  |   | 
|  CREATE \[TEMPORARY\] TABLESPACE  |  No  |      | 
|  CREATE CLUSTER  |  No  |      | 
|  CREATE CONTEXT  |  No  |      | 
|  CREATE CONTROLFILE  |  No  |      | 
|  CREATE DATABASE  |  Yes  |   | 
|  CREATE DATABASE LINK  |  No  |      | 
|  CREATE DIMENSION  |  No  |      | 
|  CREATE DIRECTORY  |  No  |      | 
|  CREATE DISKGROUP  |  No  |      | 
|  CREATE FLASHBACK ARCHIVE  |  No  |      | 
|  DROP CLUSTER  |  No  |      | 
|  DROP DATABASE  |  No  |      | 
|  DROP DATABASE LINK  |  No  |      | 
|  DROP DIMENSION  |  No  |      | 
|  DROP DIRECTORY  |  No  |      | 
|  DROP DISKGROUP  |  No  |      | 
|  DROP FLASHBACK ARCHIVE  |  No  |      | 
|  DROP FUNCTION  |  No  |      | 
|  DROP TABLE  |  No  |      | 
|  DROP TABLESPACE  |  No  |      | 
|  DROP VIEW  |  Yes  |   | 

#### ALTER TABLE<a name="w3ab1c37c15b5b2b4"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  ADD CONSTRAINT  |  Yes  |   | 
|  ADD column  |  No  |      | 
|  DEALLOCATE UNUSED  |  No  |      | 
|  DISCARD/IMPORT TABLESPACE  |  No  |      | 
|  DROP CONSTRAINT  |  No  |      | 
|  ENABLE/DISABLE constraint  |  No  |      | 
|  ENABLE/DISABLE triggers  |  No  |      | 
|  MODIFY  |  No  |      | 
|  MODIFY COLUMN  |  No  |      | 
|  PARTITION operations  |  No  |      | 
|  REMOVE PARTITIONING  |  No  |      | 
|  RENAME  |  No  |      | 
|  RENAME COLUMN  |  No  |      | 

#### CREATE \[OR REPLACE\] VIEW Statement<a name="w3ab1c37c15b5b2b6"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  FORCE  |  Yes  |   | 
|  NOFORCE  |  Yes  |   | 
|  READ ONLY  |  Yes  |   | 
|  Updatable Views  |  Yes  |   | 
|  WITH OBJECT IDENTIFIER  |  Yes  |   | 

#### CREATE INDEX Statement<a name="w3ab1c37c15b5b2b8"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  BITMAP  |  No  |   [Issue 5206: PostgreSQL doesn't support bitmap indexes](sct-reference-Oracle-PostgreSQL-CREATEINDEX.md#sct-reference-5206)   | 
|  DOMAIN  |  No  |   [Issue 5208: PostgreSQL doesn't support domain indexes](sct-reference-Oracle-PostgreSQL-CREATEINDEX.md#sct-reference-5208)   | 
|  FUNCTION\-BASED BITMAP  |  No  |   [Issue 5206: PostgreSQL doesn't support bitmap indexes](sct-reference-Oracle-PostgreSQL-CREATEINDEX.md#sct-reference-5206)   | 
|  FUNCTION\-BASED NORMAL  |  Yes  |   [Issue 5555: PostgreSQL doesn't support functional indexes that aren't single\-column](sct-reference-Oracle-PostgreSQL-CREATEINDEX.md#sct-reference-5555)   | 
|  NONUNIQUE  |  Yes  |   | 
|  NORMAL  |  Yes  |   | 
|  UNIQUE  |  Yes  |   | 

#### CREATE TABLE<a name="w3ab1c37c15b5b2c10"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  Clustered tables  |  No  |   [Issue 5199: PostgreSQL doesn't support CLUSTERED TABLE](sct-reference-Oracle-PostgreSQL-CREATETABLE.md#sct-reference-5199)   | 
|  External table  |  No  |   [Issue 5200: PostgreSQL doesn't support EXTERNAL TABLES](sct-reference-Oracle-PostgreSQL-CREATETABLE.md#sct-reference-5200)   | 
|  Function as default value for column  |  Yes  |   | 
|  Object table  |  No  |   [Issue 5196: PostgreSQL doesn't support OBJECT TABLE](sct-reference-Oracle-PostgreSQL-CREATETABLE.md#sct-reference-5196)   | 
|  Partitioned table  |  No  |   [Issue 5201: PostgreSQL doesn't support all partition types](sct-reference-Oracle-PostgreSQL-CREATETABLE.md#sct-reference-5201)   | 
|  Regular tables  |  Yes  |   | 
|  Temporary tables  |  Partial  |   [Issue 5198: PostgreSQL doesn't support GLOBAL TEMPORARY TABLE](sct-reference-Oracle-PostgreSQL-CREATETABLE.md#sct-reference-5198)   | 

#### Sequences<a name="w3ab1c37c15b5b2c12"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  CREATE  |  Yes  |   | 
|  Using  |  Yes  |   | 

## DML<a name="w3ab1c37c15b7"></a>

### Built\-in SQL Functions<a name="w3ab1c37c15b7b2"></a>

#### Aggregate Functions<a name="w3ab1c37c15b7b2b2"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  AVG  |  Yes  |   | 
|  COLLECT  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  CORR  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  CORR\_\*  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  COUNT  |  Yes  |   | 
|  COVAR\_POP  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  COVAR\_SAMP  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  CUME\_DIST  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  DENSE\_RANK  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  FIRST  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  GROUP\_ID  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  GROUPING  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  GROUPING\_ID  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  LAST  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  MAX  |  Yes  |   | 
|  MEDIAN  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  MIN  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  PERCENT\_RANK  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  PERCENTILE\_CONT  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  PERCENTILE\_DISC  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  RANK  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  REGR\_ \(Linear Regression\) Functions  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  STATS\_BINOMIAL\_TEST  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  STATS\_CROSSTAB  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  STATS\_F\_TEST  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  STATS\_KS\_TEST  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  STATS\_MODE  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  STATS\_MW\_TEST  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  STATS\_ONE\_WAY\_ANOVA  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  STATS\_T\_TEST\_\*  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  STATS\_WSR\_TEST  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  STDDEV  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  STDDEV\_POP  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  STDDEV\_SAMP  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  SUM  |  Yes  |   | 
|  VAR\_POP  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  VAR\_SAMP  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  VARIANCE  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 

#### Analytic Functions<a name="w3ab1c37c15b7b2b4"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  AVG \*  |  Yes  |   | 
|  CORR \*  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  COUNT \*  |  Yes  |   | 
|  COVAR\_POP \*  |  Yes  |   | 
|  COVAR\_SAMP \*  |  Yes  |   | 
|  CUME\_DIST  |  Yes  |   | 
|  DENSE\_RANK  |  Yes  |   | 
|  FIRST  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  FIRST\_VALUE \*  |  Yes  |   | 
|  LAG  |  Yes  |   | 
|  LAST  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  LAST\_VALUE \*  |  Yes  |   | 
|  LEAD  |  Yes  |   | 
|  MAX \*  |  Yes  |   | 
|  MIN \*  |  Yes  |   | 
|  NTILE  |  Yes  |   | 
|  PERCENT\_RANK  |  Yes  |   | 
|  PERCENTILE\_CONT  |  Yes  |   | 
|  PERCENTILE\_DISC  |  Yes  |   | 
|  RANK  |  Yes  |   | 
|  RATIO\_TO\_REPORT  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  REGR\_ \(Linear Regression\) Functions \*  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  ROW\_NUMBER  |  Yes  |   | 
|  STDDEV \*  |  Yes  |   | 
|  STDDEV\_POP \*  |  Yes  |   | 
|  STDDEV\_SAMP \*  |  Yes  |   | 
|  SUM \*  |  Yes  |   | 
|  VAR\_POP \*  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  VAR\_SAMP \*  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  VARIANCE \*  |  Yes  |   | 

#### Character Functions Returning Character Values<a name="w3ab1c37c15b7b2b6"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  CHR\(num\)  |  Yes  |   | 
|  CONCAT\(char1, char2\)  |  Yes  |   | 
|  INITCAP\(string\)  |  Yes  |   | 
|  LOWER\(string\)  |  Yes  |   | 
|  LPAD\(string, len\)  |  Yes  |   | 
|  LPAD\(string, len, pad\)  |  Yes  |   | 
|  LTRIM\(string\)  |  Yes  |   | 
|  NLS\_INITCAP  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  NLS\_LOWER  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  NLS\_UPPER  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  NLSSORT  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  REGEXP\_REPLACE  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  REGEXP\_SUBSTR  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  REPLACE\(str, search\)  |  Yes  |   | 
|  REPLACE\(str, search, replace\)  |  Yes  |   | 
|  RPAD\(string, len\)  |  Yes  |   | 
|  RTRIM\(string\)  |  Yes  |   | 
|  RTRIM\(string, set\)  |  Yes  |   | 
|  SOUNDEX\(string\)  |  Yes  |   | 
|  SUBSTR\(string, pos, len\)  |  Yes  |   | 
|  TRANSLATE\(string, from, to\)  |  Yes  |   | 
|  TREAT  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  TRIM\(\[type trim FROM\] string\)  |  Yes  |   | 
|  UPPER\(string\)  |  Yes  |   | 

#### Character Functions Returning Number Values<a name="w3ab1c37c15b7b2b8"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  ASCII\(str\)  |  Yes  |   | 
|  INSTR\(str, substr\)  |  Yes  |   | 
|  INSTR\(str, substr, pos\)  |  Implemented in Extension Library  |   | 
|  INSTR\(str, substr, pos, num\)  |  Implemented in Extension Library  |   | 
|  LENGTH\(string\)  |  Yes  |   | 
|  REGEXP\_INSTR  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 

#### Collection Functions<a name="w3ab1c37c15b7b2c10"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  CARDINALITY  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  COLLECT  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  SET  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 

#### Conversion Functions<a name="w3ab1c37c15b7b2c12"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  ASCIISTR\(string\)  |  Implemented in Extension Library  |   | 
|  BIN\_TO\_NUM\(bit1, bit2, …\)  |  Yes  |   | 
|  CAST  |  Yes  |   | 
|  CHARTOROWID  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  COMPOSE  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  CONVERT\(string, charset\)  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  DECOMPOSE  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  HEXTORAW  |  Yes  |   | 
|  NUMTODSINTERVAL  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  NUMTOYMINTERVAL  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  RAWTOHEX  |  Yes  |   | 
|  RAWTONHEX  |  Yes  |   | 
|  ROWIDTOCHAR  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  ROWIDTONCHAR  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  SCN\_TO\_TIMESTAMP  |  Yes  |   | 
|  TIMESTAMP\_TO\_SCN  |  Yes  |   | 
|  TO\_BINARY\_DOUBLE  |  Yes  |   | 
|  TO\_BINARY\_FLOAT  |  Yes  |   | 
|  TO\_CHAR \(character\)  |  Yes  |   | 
|  TO\_CHAR \(datetime, format\)  |  Yes  |   | 
|  TO\_CHAR \(number, format\)  |  Implemented in Extension Library  |   | 
|  TO\_CLOB  |  Yes  |   | 
|  TO\_DATE  |  Implemented in Extension Library  |   | 
|  TO\_DSINTERVAL  |  Yes  |   | 
|  TO\_LOB  |  Yes  |   | 
|  TO\_MULTI\_BYTE  |  Yes  |   | 
|  TO\_NCHAR \(character\)  |  Yes  |   | 
|  TO\_NCHAR \(datetime\)  |  Implemented in Extension Library  |   | 
|  TO\_NCHAR \(number\)  |  Implemented in Extension Library  |   | 
|  TO\_NCLOB  |  Implemented in Extension Library  |   | 
|  TO\_NUMBER  |  Implemented in Extension Library  |   | 
|  TO\_SINGLE\_BYTE  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  TRANSLATE \.\.\. USING  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  UNISTR  |  Implemented in Extension Library  |   | 

#### Data Mining Functions<a name="w3ab1c37c15b7b2c14"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  CLUSTER\_ID  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  CLUSTER\_PROBABILITY  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  CLUSTER\_SET  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  FEATURE\_ID  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  FEATURE\_SET  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  FEATURE\_VALUE  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  PREDICTION  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  PREDICTION\_COST  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  PREDICTION\_DETAILS  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  PREDICTION\_PROBABILITY  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  PREDICTION\_SET  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 

#### Datetime Functions<a name="w3ab1c37c15b7b2c16"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  ADD\_MONTHS\(date, num\)  |  Implemented in Extension Library  |   | 
|  CURRENT\_DATE  |  Yes  |   | 
|  CURRENT\_TIMESTAMP  |  Yes  |   | 
|  DBTIMEZONE  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  EXTRACT\(DAY FROM date\)  |  Yes  |   | 
|  EXTRACT\(HOUR FROM time\)  |  Yes  |   | 
|  EXTRACT\(MINUTE FROM time\)  |  Yes  |   | 
|  EXTRACT\(MONTH FROM date\)  |  Yes  |   | 
|  EXTRACT\(SECOND FROM time\)  |  Yes  |   | 
|  EXTRACT\(YEAR FROM date\)  |  Yes  |   | 
|  FROM\_TZ  |  Implemented in Extension Library  |   | 
|  LAST\_DAY\(date\)  |  Implemented in Extension Library  |   | 
|  LOCALTIMESTAMP  |  Yes  |   | 
|  LOCALTIMESTAMP\(\[prec\]\)  |  Yes  |   | 
|  MONTHS\_BETWEEN\(date1, date2\)  |  Yes  |   | 
|  NEW\_TIME  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  NEXT\_DAY  |  Implemented in Extension Library  |   | 
|  NUMTODSINTERVAL  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  NUMTOYMINTERVAL  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  ROUND \(date\)  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  SESSIONTIMEZONE  |  Yes  |   | 
|  SYS\_EXTRACT\_UTC  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  SYSDATE  |  Yes  |   | 
|  SYSTIMESTAMP  |  Yes  |   | 
|  TO\_CHAR \(datetime, format\)  |  Yes  |   | 
|  TO\_DSINTERVAL  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  TO\_TIMESTAMP\(exp\)  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  TO\_TIMESTAMP\_TZ  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  TO\_YMINTERVAL  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  TRUNC \(datetime\)  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  TZ\_OFFSET  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 

#### dbms\_output<a name="w3ab1c37c15b7b2c18"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  dbms\_output\.put\(\)   |  Yes  |   | 
|  dbms\_output\.put\_line\(\)   |  Yes  |   | 

#### Encoding and Decoding Functions<a name="w3ab1c37c15b7b2c20"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  DECODE\(exp, when, then, …\)  |  Yes  |   | 
|  DUMP  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  ORA\_HASH  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  VSIZE  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 

#### Environment and Identifier Functions<a name="w3ab1c37c15b7b2c22"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  SYS\_CONTEXT  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  SYS\_GUID  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  SYS\_TYPEID  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  UID  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  USER  |  Yes  |   | 
|  USERENV\('parameter'\)  |  Yes  |   | 

#### General Comparison Functions<a name="w3ab1c37c15b7b2c24"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  GREATEST\(exp, exp2, …\)  |  Yes  |   | 
|  LEAST\(exp, exp2, …\)  |  Yes  |   | 

#### Hierarchical Functions<a name="w3ab1c37c15b7b2c26"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  SYS\_CONNECT\_BY\_PATH  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 

#### Large Object Functions<a name="w3ab1c37c15b7b2c28"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  BFILENAME  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  EMPTY\_BLOB, EMPTY\_CLOB  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 

#### Model Functions<a name="w3ab1c37c15b7b2c30"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  CV  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  ITERATION\_NUMBER  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  PRESENTNNV  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  PRESENTV  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  PREVIOUS  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 

#### NLS Character Functions<a name="w3ab1c37c15b7b2c32"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  NLS\_CHARSET\_DECL\_LEN  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  NLS\_CHARSET\_ID  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  NLS\_CHARSET\_NAME  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 

#### NULL\-Related Functions<a name="w3ab1c37c15b7b2c34"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  COALESCE\(exp1, exp2, …\)  |  Yes  |   | 
|  LNNVL  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  NULLIF\(exp1, exp2\)  |  Yes  |   | 
|  NVL\(exp, replacement\)  |  Yes  |   | 
|  NVL2\(exp1, exp2, exp3\)  |  Yes  |   | 

#### Numeric Functions<a name="w3ab1c37c15b7b2c36"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  ABS\(num\)  |  Yes  |   | 
|  ACOS\(num\)  |  Yes  |   | 
|  ASIN\(num\)  |  Yes  |   | 
|  ATAN\(num\)  |  Yes  |   | 
|  ATAN2\(x,y\)  |  Yes  |   | 
|  BITAND\(exp1, exp2\)  |  Yes  |   | 
|  CEIL\(num\)  |  Yes  |   | 
|  COS\(num\)  |  Yes  |   | 
|  COSH\(num\)  |  Yes  |   | 
|  EXP\(n\)  |  Yes  |   | 
|  FLOOR\(num\)  |  Yes  |   | 
|  LN\(num\)  |  Yes  |   | 
|  LOG\(num1, num2\)  |  Yes  |   | 
|  MOD\(dividend, divisor\)  |  Yes  |   | 
|  NANVL\(n2, n1\)  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  POWER\(value, n\)  |  Yes  |   | 
|  REMAINDER\(n1, n2\)  |  Yes  |   | 
|  ROUND \(num, integer\)  |  Yes  |   | 
|  SIGN\(exp\)  |  Yes  |   | 
|  SIN\(num\)  |  Yes  |   | 
|  SINH\(num\)  |  Yes  |   | 
|  SQRT\(num\)  |  Yes  |   | 
|  TAN\(num\)  |  Yes  |   | 
|  TANH\(num\)  |  Yes  |   | 
|  TRUNC \(number\)  |  Yes  |   | 
|  WIDTH\_BUCKET  |  Yes  |   | 

#### Object Reference Functions<a name="w3ab1c37c15b7b2c38"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  DEREF  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  MAKE\_REF  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  REF  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  REFTOHEX  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  VALUE  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 

#### XML Functions<a name="w3ab1c37c15b7b2c40"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  APPENDCHILDXML  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  DELETEXML  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  DEPTH  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  EXISTSNODE  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  EXTRACT \(XML\)  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  EXTRACTVALUE  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  INSERTCHILDXML  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  INSERTXMLBEFORE  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  PATH  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  SYS\_DBURIGEN  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  SYS\_XMLAGG  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  SYS\_XMLGEN  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  UPDATEXML  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  XMLAGG  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  XMLCDATA  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  XMLCOLATTVAL  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  XMLCOMMENT  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  XMLCONCAT  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  XMLFOREST  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  XMLPARSE  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  XMLPI  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  XMLQUERY  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  XMLROOT  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  XMLSEQUENCE  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  XMLSERIALIZE  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  XMLTABLE  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 
|  XMLTRANSFORM  |  No  |   [Issue 5340: PostgreSQL doesn't support the %s function](sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-5340)   | 

### Hints<a name="w3ab1c37c15b7b4"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  Index and Cluster  |  No  |   [Issue 5103: PostgreSQL doesn't support the %s hint](sct-reference-Oracle-PostgreSQL-OptimizerHints.md#sct-reference-5103)   | 
|  Join Order  |  No  |   [Issue 5103: PostgreSQL doesn't support the %s hint](sct-reference-Oracle-PostgreSQL-OptimizerHints.md#sct-reference-5103)   | 
|  Joins  |  No  |   [Issue 5103: PostgreSQL doesn't support the %s hint](sct-reference-Oracle-PostgreSQL-OptimizerHints.md#sct-reference-5103)   | 
|  Optimizer Mode  |  No  |   [Issue 5103: PostgreSQL doesn't support the %s hint](sct-reference-Oracle-PostgreSQL-OptimizerHints.md#sct-reference-5103)   | 
|  Parallel Execution  |  No  |   [Issue 5103: PostgreSQL doesn't support the %s hint](sct-reference-Oracle-PostgreSQL-OptimizerHints.md#sct-reference-5103)   | 
|  Query Transformation  |  No  |   [Issue 5103: PostgreSQL doesn't support the %s hint](sct-reference-Oracle-PostgreSQL-OptimizerHints.md#sct-reference-5103)   | 
|  Other  |  No  |   [Issue 5103: PostgreSQL doesn't support the %s hint](sct-reference-Oracle-PostgreSQL-OptimizerHints.md#sct-reference-5103)   | 

### Joins<a name="w3ab1c37c15b7b6"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  Cross Joins  |  Yes  |   | 
|  Inner Joins  |  Yes  |   | 
|  Outer Joins  |  Yes  |   | 

### Operators and Date Functions<a name="w3ab1c37c15b7b8"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  Arithmetic operators  |  Yes  |   | 
|  Concatenation operators  |  Yes  |   | 

### Predicates<a name="w3ab1c37c15b7c10"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  Boolean conditions  |  Yes  |   | 
|  Comparison conditions: '=, <>, <, <=, >, >=, ANY, SOME, ALL  |  Yes  |   | 
|  Exists conditions  |  Yes  |   | 
|  In conditions  |  Yes  |   | 
|  Null conditions  |  Yes  |   | 
|  Pattern matching conditions  |  Yes  |   | 
|  Range conditions  |  Yes  |   | 

### Set operators<a name="w3ab1c37c15b7c12"></a>

#### Concatenation operators<a name="w3ab1c37c15b7c12b2"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  INTERSECT, EXCEPT  |  Yes  |   | 
|  MINUS  |  Yes  |   | 
|  UNION, UNION ALL  |  Yes  |   | 

### Statements<a name="w3ab1c37c15b7c14"></a>

#### DELETE<a name="w3ab1c37c15b7c14b2"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  DELETE FROM MATERIALIZED VIEW  |  No  |   [Issue 5095: PostgreSQL doesn't support using a materialized VIEW](sct-reference-Oracle-PostgreSQL-MATERIALIZEDVIEW.md#sct-reference-5095)   | 
|  DELETE FROM SUBQUERY  |  No  |   [Issue 5068: PostgreSQL doesn't support the DELETE statement for a subquery](sct-reference-Oracle-PostgreSQL-DELETE.md#sct-reference-5068)   | 
|  DELETE FROM TABLE  |  Yes  |   | 
|  DELETE FROM VIEW  |  Yes  |   | 
|  DELETE with Error Logging clause  |  No  |   [Issue 5067: PostgreSQL doesn't support the DELETE statement with the ERROR LOG option](sct-reference-Oracle-PostgreSQL-DELETE.md#sct-reference-5067)   | 
|  DELETE with RETURNING clause  |  Yes  |   | 

#### HIERARCHICAL QUERY AND HIERARCHICAL QUERY PSEUDOCOLUMNS<a name="w3ab1c37c15b7c14b4"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  CONNECT BY CLAUSE  |  Yes  |   | 
|  CONNECT BY NOCYCLE  |  No  |   [Issue 5586: Automatic conversion for queries with NOCYCLE clause not supported](sct-reference-Oracle-PostgreSQL-SELECT.md#sct-reference-5586)   | 
|  CONNECT\_BY\_ISLEAF pseudocolumn  |  Yes  |   | 
|  LEVEL PSEUDOCOLUMN  |  Yes  |   | 
|  ORDER SIBLINGS BY  |  Yes  |   | 
|  START WITH CLAUSE  |  Yes  |   | 
|  SYS\_CONNECT\_BY\_PATH  |  Yes  |   | 

#### Hierarchical query operators<a name="w3ab1c37c15b7c14b6"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  CONNECT\_BY\_ROOT  |  Yes  |   | 
|  PRIOR  |  Yes  |   | 

#### INSERT<a name="w3ab1c37c15b7c14b8"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  ALL  |  Yes  |   | 
|  DEFAULT  |  Yes  |   | 
|  ELSE   |  Yes  |   | 
|  FIRST  |  Yes  |   | 
|  INSERT from clause "SUBQUERY"  |  Yes  |   | 
|  INSERT from clause "VALUES\(\.\.\.\)"  |  Yes  |   | 
|  INSERT INTO SUBQUERY  |  No  |   [Issue 5071: PostgreSQL doesn't support the INSERT statement for a subquery](sct-reference-Oracle-PostgreSQL-INSERT.md#sct-reference-5071)   | 
|  INSERT INTO TABLE  |  Yes  |   | 
|  INSERT INTO VIEW  |  Yes  |   | 
|  INSERT with partition\_extension\_clause  |  No  |   [Issue 5024: PostgreSQL doesn't support the INSERT statement with partition\_extension\_clause](sct-reference-Oracle-PostgreSQL-INSERT.md#sct-reference-5024)   | 
|  Inserting Into a Table with Error Logging clause  |  No  |   [Issue 5070: PostgreSQL doesn't support the INSERT statement with the ERROR LOG option](sct-reference-Oracle-PostgreSQL-INSERT.md#sct-reference-5070)   | 
|  RETURNING INTO  |  Yes  |   | 
|  WHEN  |  Yes  |   | 

#### LOCK TABLE<a name="w3ab1c37c15b7c14c10"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  Locking table in exclusive mode  |  Yes  |   | 
|  Locking table in share mode  |  Yes  |   | 
|  Locking without waiting  |  Yes  |   | 

#### SELECT<a name="w3ab1c37c15b7c14c12"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  Add or subtract operators  |  Yes  |   | 
|  BULK COLLECT INTO  |  No  |   [Issue 5140: PostgreSQL doesn't support BULK COLLECT INTO](sct-reference-Oracle-PostgreSQL-SELECT.md#sct-reference-5140)   | 
|  CUBE  |  No  |   [Issue 5557: PostgreSQL doesn't support GROUPING SETS, CUBE, and ROLLUP functions](sct-reference-Oracle-PostgreSQL-SELECT.md#sct-reference-5557)   | 
|  FOR UPDATE  |  No  |   [Issue 5139: PostgreSQL doesn't support FOR UPDATE SKIP LOCKED](sct-reference-Oracle-PostgreSQL-SELECT.md#sct-reference-5139)   | 
|  GROUP BY  |  Yes  |   | 
|  GROUPING SETS  |  No  |   [Issue 5557: PostgreSQL doesn't support GROUPING SETS, CUBE, and ROLLUP functions](sct-reference-Oracle-PostgreSQL-SELECT.md#sct-reference-5557)   | 
|  HAVING  |  Yes  |   | 
|  INTERSECT  |  Yes  |   | 
|  INTO  |  Yes  |   | 
|  MINUS  |  Yes  |   | 
|  MODEL  |  No  |   [Issue 5126: PostgreSQL doesn't support the MODEL statement](sct-reference-Oracle-PostgreSQL-SELECT.md#sct-reference-5126)   | 
|  ORDER BY  |  Yes  |   | 
|  PIVOT clause  |  No  |   [Issue 5077: PostgreSQL doesn't support the PIVOT clause for the SELECT statement](sct-reference-Oracle-PostgreSQL-VIEW.md#sct-reference-5077)   | 
|  ROLLUP  |  No  |   [Issue 5557: PostgreSQL doesn't support GROUPING SETS, CUBE, and ROLLUP functions](sct-reference-Oracle-PostgreSQL-SELECT.md#sct-reference-5557)   | 
|  ROWNUM pseudocolumn  |  Yes  |   | 
|  SELECT ALL  |  Yes  |   | 
|  SELECT DISTINCT  |  Yes  |   | 
|  SELECT LIST  |  Yes  |   | 
|  SELECT UNIQUE  |  Yes  |   | 
|  UNION  |  Yes  |   | 
|  UNION ALL  |  Yes  |   | 
|  UNPIVOT clause  |  Yes  |   | 
|  WHERE\( field\_name1,…,fieldnameN\) IN \(subquery\_with\_multiple\_fields\)  |  Yes  |   | 
|  WHERE comparison\_condition \(=;<>;\!=;<;>;>=;<=;ANY;SOME;ALL\)  |  Yes  |   | 
|  WHERE compound\_condition\_with\_or\_and\_not  |  Yes  |   | 
|  WHERE field\_name BETWEEN arg1 AND arg2  |  Yes  |   | 
|  WHERE field\_name IN \(const1,\.\.\.,constN\)  |  Yes  |   | 
|  WHERE field\_name IN \(subquery\)  |  Yes  |   | 
|  WHERE like\_condition \(operator LIKE\)  |  Yes  |   | 
|  WITH  |  Yes  |   | 

#### UPDATE<a name="w3ab1c37c15b7c14c14"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  UPDATE \(subquery\)  |  No  |   [Issue 5065: PostgreSQL doesn't support the UPDATE statement for a subquery](sct-reference-Oracle-PostgreSQL-UPDATE.md#sct-reference-5065)   | 
|  UPDATE MATERIALIZED VIEW  |  No  |   [Issue 5095: PostgreSQL doesn't support using a materialized VIEW](sct-reference-Oracle-PostgreSQL-MATERIALIZEDVIEW.md#sct-reference-5095)   | 
|  UPDATE TABLE  |  Yes  |   | 
|  UPDATE VIEW  |  Yes  |   | 
|  UPDATE with Error Logging clause  |  No  |   [Issue 5064: PostgreSQL doesn't support the UPDATE statement with the ERROR LOG option](sct-reference-Oracle-PostgreSQL-UPDATE.md#sct-reference-5064)   | 
|  UPDATE with partition extension clause  |  No  |   [Issue 5558: PostgreSQL doesn't support the UPDATE statement for a PARTITION](sct-reference-Oracle-PostgreSQL-UPDATE.md#sct-reference-5558)   | 
|  UPDATE with RETURNING…INTO clause  |  Yes  |   | 
|  UPDATE with subqueries into SET\-clause  |  Yes  |   | 
|  UPDATE\-operator which based on data from others tables  |  Yes  |   | 

#### MERGE<a name="w3ab1c37c15b7c14c16"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  MERGE  |  No  |   [Issue 5102: PostgreSQL doesn't support the MERGE statement](sct-reference-Oracle-PostgreSQL-MERGE.md#sct-reference-5102)   | 
|  TRUNCATE TABLE  |  Yes  |   | 

## PLSQL<a name="w3ab1c37c15b9"></a>

### Arguments of functions and procedures<a name="w3ab1c37c15b9b2"></a>

#### <a name="w3ab1c37c15b9b2b2"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  Built\-in datatype scalar arguments  |  Yes  |   | 
|  Cursor\-type arguments  |  Yes  |   | 
| Default clause in declaration of arguments |  Yes  |   | 
|  IN, OUT, IN OUT type of arguments  |  Yes  |   | 
|  Ref cursor\-type arguments  |  Yes  |   | 
|  UDT collection\-type arguments  |  Yes  |   | 
|  UDT object\-type arguments  |  Yes  |   | 
|  UDT record\-type   |  Yes  |   | 

### Functions<a name="w3ab1c37c15b9b4"></a>

#### <a name="w3ab1c37c15b9b4b2"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  Functions with DML  |  Yes  |   | 
|  Functions without DML  |  Yes  |   | 
|  Return pipelined table  |  Yes  |   | 
|  Return ref cursor  |  Yes  |   | 
|  Return scalar  |  Yes  |   | 
|  Return table  |  Yes  |   | 
|  Return UDT collection\-type   |  Yes  |   | 
|  Return UDT object\-type   |  Yes  |   | 
|  Return UDT record\-type   |  Yes  |   | 

### Packages<a name="w3ab1c37c15b9b6"></a>

#### <a name="w3ab1c37c15b9b6b2"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  Global cursor declaration  |  No  |   [Issue 5569: PostgreSQL only supports session variables using SQL standard date and time types](sct-reference-Oracle-PostgreSQL-PACKAGES.md#sct-reference-5569)   | 
|  Global user exception declaration  |  No  |   [Issue 5569: PostgreSQL only supports session variables using SQL standard date and time types](sct-reference-Oracle-PostgreSQL-PACKAGES.md#sct-reference-5569)   | 
|  Initialization block BEGIN … END in packages  |  Yes  |   | 
|  Package functions  |  Yes  |   | 
|  Package procedures  |  Yes  |   | 
|  Package variables  |  Yes  |   | 
|  User type declaration  |  Yes  |   | 

### PL SQL constructions<a name="w3ab1c37c15b9b8"></a>

#### <a name="w3ab1c37c15b9b8b2"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  block EXCEPTION when exception\_name then…  |  Yes  |   | 
|  CASE\_NOT\_FOUND  |  Yes  |   | 
|  case when conditions then…else… end case;  |  Yes  |   | 
|  close cursor\_variable  |  Yes  |   | 
|  COMMIT  |  Yes  |   | 
|  CURSOR\_ALREADY\_OPEN  |  Yes  |   | 
|  DUP\_VAL\_ON\_INDEX  |  Yes  |   | 
|  execute immediate SQL\_string\_variable into variables\_list use variables\_list  |  No  |   [Issue 5334: PostgreSQL doesn't support the dynamic SQL statement](sct-reference-Oracle-PostgreSQL-DYNAMICSQL.md#sct-reference-5334)   | 
|  fetch cursor\_variable into variables\_list  |  Yes  |   | 
|  FORALL \-cycle  |  No  |   [Issue 5121: PostgreSQL doesn't support the FORALL statement](sct-reference-Oracle-PostgreSQL-UDTcollection-typearguments.md#sct-reference-5121)   | 
|  for I in\(begN\.\.endN\) loop… end loop  |  Yes  |   | 
|  for I in\(cursor\_name\) loop… end loop  |  Yes  |   | 
|  for I in\(select\_statement\) loop… end loop  |  Yes  |   | 
|  FOR i IN REVERSE begN\.\.endN LOOP… END LOOP;  |  Yes  |   | 
|  goto label;  |  No  |   [Issue 5335: PostgreSQL doesn't support the GOTO operator](sct-reference-Oracle-PostgreSQL-Statements.md#sct-reference-5335)   | 
|  if conditions then…else if conditions then… end if;  |  Yes  |   | 
|  if conditions then… end if;  |  Yes  |   | 
|  INVALID\_CURSOR  |  Yes  |   | 
|  INVALID\_NUMBER  |  Yes  |   | 
|  LOGIN\_DENIED  |  Yes  |   | 
|  LOOP…exit when conditions; END LOOP;  |  Yes  |   | 
|  NO\_DATA\_FOUND  |  Yes  |   | 
|  NOT\_LOGGED\_ON  |  Yes  |   | 
|  NULL Statement  |  Yes  |   | 
|  open cursor\_variable  |  Yes  |   | 
|  open cursor\_variable for select\_statemet\_string\_variable  |  Yes  |   | 
|  others  |  Yes  |   | 
|  PRAGMA AUTONOMOUS\_TRANSACTION  |  No  |   [Issue 5350: The function can't use statements that explicitly or implicitly begin or end a transaction, such as START TRANSACTION, COMMIT, or ROLLBACK](sct-reference-Oracle-PostgreSQL-FUNCTION.md#sct-reference-5350)   | 
|  PROGRAM\_ERROR  |  Yes  |   | 
|  raise\_application\_error\(exept\_code, message\)  |  Yes  |   | 
|  raise exeption\_name  |  Yes  |   | 
|  ROLLBACK  |  Yes  |   | 
|  select…bulk collect into table\_variable from table\_name  |  No  |   [Issue 5140: PostgreSQL doesn't support BULK COLLECT INTO](sct-reference-Oracle-PostgreSQL-SELECT.md#sct-reference-5140)   | 
|  SQL%BULK\_ROWCOUNT  |  No  |      | 
|  SQL%FOUND  |  Yes  |   | 
|  SQL%ISOPEN  |  No  |   [Issue 5084: PostgreSQL doesn't support the cursor attribute %ISOPEN](sct-reference-Oracle-PostgreSQL-CURSOR.md#sct-reference-5084)   | 
|  SQL%NOTFOUND  |  Yes  |   | 
|  SQL%ROWCOUNT  |  Yes  |   | 
|  STORAGE\_ERROR  |  Yes  |   | 
|  TIMEOUT\_ON\_RESOURCE  |  Yes  |   | 
|  TOO\_MANY\_ROWS  |  Yes  |   | 
|  TRANSACTION\_BACKED\_OUT  |  Yes  |   | 
|  VALUE\_ERROR  |  Yes  |   | 
|  while conditions loop… end loop;  |  Yes  |   | 
|  ZERO\_DIVIDE  |  Yes  |   | 

### PL SQL declaration block<a name="w3ab1c37c15b9c10"></a>

#### <a name="w3ab1c37c15b9c10b2"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  Declare built\-in scalar variable  |  Yes  |   | 
|  Declare ref\-cursor variable  |  Yes  |   | 
|  Declare static cursor  |  Yes  |   | 
|  Declare UDT collection variable  |  Yes  |   | 
|  Declare UDT object variable  |  Yes  |   | 
|  Declare UDT record variable  |  Yes  |   | 
|  Declare UDT array types  |  Yes  |   | 
|  Declare user\-exception  |  Yes  |   | 
|  Declare with %rowtype option  |  Yes  |   | 
|  Declare with %type option  |  Yes  |   | 

### Procedures<a name="w3ab1c37c15b9c12"></a>

#### <a name="w3ab1c37c15b9c12b2"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  CREATE PROCEDURE statement  |  Yes  |   | 

### Triggers<a name="w3ab1c37c15b9c14"></a>

#### <a name="w3ab1c37c15b9c14b2"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  BEFORE, AFTER \- options  |  Yes  |   | 
|  FOR EACH ROW \-option  |  Yes  |   | 
|  INSTEAD OF \- options  |  Yes  |   | 
|  NESTED TABLE \- clause  |  No  |   [Issue 5240: PostgreSQL doesn't support triggers on nested table columns in views](sct-reference-Oracle-PostgreSQL-TRIGGERS.md#sct-reference-5240)   | 
|  REFERENCING \- clause  |  No  |   [Issue 5238: PostgreSQL doesn't support the REFERENCING clauses](sct-reference-Oracle-PostgreSQL-TRIGGERS.md#sct-reference-5238)   | 
|  Statement\-trigger  |  No  |      | 
|  trigger on TABLE  |  Yes  |   | 
|  Trigger on VIEW  |  Yes  |   | 
|  WHEN\(condition\)\- option  |  No  |      | 

## Data Types<a name="w3ab1c37c15c11"></a>


| Data type | Automatically Converted to | Details | 
| --- | --- | --- | 
| BFILE | character varying | [Issue 5212: PostgreSQL doesn't have a data type BFILE](sct-reference-Oracle-PostgreSQL-CREATETABLE.md#sct-reference-5212) | 
| BINARY\_FLOAT | real |  | 
| BINARY\_DOUBLE | double precision |  | 
| BLOB | bytea |  | 
| CHAR\(n\) | character |  | 
| CHARACTER\(n\) | character |  | 
| CLOB | text |  | 
| DATE | timestamp\(0\) without time zone |  | 
| DECIMAL\(p,s\) | numeric |  | 
| DEC\(p,s\) | numeric |  | 
| FLOAT | double precision |  | 
| INTEGER | numeric |  | 
| INT | numeric |  | 
| INTERVAL YEAR\(p\) TO MONTH | interval year to month |  | 
| INTERVAL DAY\(p\) TO SECOND\(s\) | interval day to second\(s\) |  | 
| LONG | text |  | 
| LONG RAW | bytea |  | 
| NCHAR\(n\) | character |  | 
| NCHAR VARYING\(n\) | character varying |  | 
| NCLOB | text |  | 
| NUMBER\(p\) | numeric |  | 
| NUMBER\(p,0\) | numeric |  | 
| NUMBER\(\*,0\) | numeric |  | 
| NUMBER\(p,s\) | numeric |  | 
| NUMBER\(\*\) | double precision |  | 
| NUMBER | double precision |  | 
| NVARCHAR2\(n\) | character varying |  | 
| RAW\(n\) | bytea |  | 
| ROWID | character | [Issue 5550: PostgreSQL doesn't have a data type ROWID](sct-reference-Oracle-PostgreSQL-CREATETABLE.md#sct-reference-5550) | 
| TIMESTAMP\(p\) | timestamp\(p\) without time zone |  | 
| TIMESTAMP\(p\) | timestamp\(6\) without time zone | [Issue 5213: PostgreSQL expands fractional seconds support for TIME, DATETIME, and TIMESTAMP values, with up to microseconds \(6 digits\) of precision](sct-reference-Oracle-PostgreSQL-CREATETABLE.md#sct-reference-5213) | 
| TIMESTAMP\(p\) WITH TIME ZONE | timestamp\(p\) with time zone |  | 
| TIMESTAMP\(p\) WITH TIME ZONE | timestamp\(6\) with time zone | [Issue 5552: PostgreSQL expands fractional seconds support for TIME, DATETIME, and TIMESTAMP values, with up to microseconds \(6 digits\) of precision](sct-reference-Oracle-PostgreSQL-CREATETABLE.md#sct-reference-5552) | 
| TIMESTAMP\(p\) WITH LOCAL TIME ZONE | timestamp\(p\) without time zone |  | 
| TIMESTAMP\(p\) WITH LOCAL TIME ZONE | timestamp\(6\) without time zone | [Issue 5553: PostgreSQL expands fractional seconds support for TIME, DATETIME, and TIMESTAMP values, with up to microseconds \(6 digits\) of precision](sct-reference-Oracle-PostgreSQL-CREATETABLE.md#sct-reference-5553) | 
| UROWID | character varying | [Issue 5551: PostgreSQL doesn't have a data type UROWID](sct-reference-Oracle-PostgreSQL-CREATETABLE.md#sct-reference-5551) | 
| VARCHAR | character varying |  | 
| VARCHAR2 | character varying |  | 
| XMLTYPE | xml |  | 