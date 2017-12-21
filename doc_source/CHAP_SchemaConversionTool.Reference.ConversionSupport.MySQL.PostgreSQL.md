# MySQL to PostgreSQL Supported Schema Conversion<a name="CHAP_SchemaConversionTool.Reference.ConversionSupport.MySQL.PostgreSQL"></a>

The following sections list the schema elements from a MySQL database and whether they are supported for automatic conversion to PostgreSQL using the AWS Schema Conversion Tool\. 

## DDL<a name="w3ab1c37c11b5"></a>

### Alter Statements<a name="w3ab1c37c11b5b2"></a>

#### ALTER TABLE<a name="w3ab1c37c11b5b2b2"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  ADD CONSTRAINT  |  Yes  |   | 
|  ADD INDEX  |  Yes  |   | 

### Create Statements<a name="w3ab1c37c11b5b4"></a>

#### CREATE INDEX<a name="w3ab1c37c11b5b4b2"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  INDEX  |  Yes  |   | 
|  UNIQUE index  |  Yes  |   | 

#### CREATE PROCEDURE<a name="w3ab1c37c11b5b4b4"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  PARAMETERS: IN, OUT, INOUT  |  Yes  |   | 
|  With any output parameters  |  Yes  |   | 
|  Without output parameters  |  Yes  |   | 

#### CREATE TABLE<a name="w3ab1c37c11b5b4b6"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  Regular tables  |  Yes  |   | 
|  Temporary tables   |  Yes  |   | 

#### CREATE TRIGGER<a name="w3ab1c37c11b5b4b8"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  FOR EACH ROW Triggers  |  Yes  |   | 
|  Trigger event \(Insert / Update / Delete \)  |  Yes  |   | 
|  Trigger time \(Before / After\)  |  Yes  |   | 

#### CREATE VIEW<a name="w3ab1c37c11b5b4c10"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  With ALGORITHM OPTION  |  Partial  |   [Issue 8824: ALGORITHM option is not supported](sct-reference-MySQL-PostgreSQL-VIEW.md#sct-reference-8824)   | 
|  With CHECK OPTION  |  Yes  |   | 

### Naming Objects<a name="w3ab1c37c11b5b8"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  Schemas  |  Yes  |   | 
|  Tables, Columns  |  Yes  |   | 

## DML<a name="w3ab1c37c11b7"></a>

### Clauses<a name="w3ab1c37c11b7b2"></a>

#### FROM<a name="w3ab1c37c11b7b2b2"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  CROSS JOIN  |  Yes  |   | 
|  INNER JOIN  |  Yes  |   | 
|  join\_condition: \.\.\.ON conditional\_expr  |  Yes  |   | 
|  join\_condition: … USING \(column\_list\)  |  Yes  |   | 
|  LEFT JOIN  |  Yes  |   | 
|  LEFT OUTER JOIN  |  Yes  |   | 
|  NATURAL LEFT JOIN  |  Yes  |   | 
|  NATURAL LEFT OUTER JOIN  |  Yes  |   | 
|  NATURAL RIGHT JOIN  |  Yes  |   | 
|  NATURAL RIGHT OUTER JOIN  |  Yes  |   | 
|  RIGHT JOIN  |  Yes  |   | 
|  RIGHT OUTER JOIN  |  Yes  |   | 
|  STRAIGHT\_JOIN  |  Yes  |   | 
|  Subqueries in the FROM Clause  |  Yes  |   | 
|  tables\_list  |  Yes  |   | 

### Statements<a name="w3ab1c37c11b7b4"></a>

#### DELETE<a name="w3ab1c37c11b7b4b2"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  IGNORE  |  Partial  |   [Issue 8831: PostgreSQL doesn't have an option similar to IGNORE for DML statements](sct-reference-MySQL-PostgreSQL-DML.md#sct-reference-8831)   | 
|  LIMIT  |  Yes  |   | 
|  LOW\_PRIORITY  |  Partial  |   [Issue 8830: PostgreSQL doesn't have an option similar to LOW\_PRIORITY for DML statements](sct-reference-MySQL-PostgreSQL-DML.md#sct-reference-8830)   | 
|  Multiple\-Table Syntax   |  Partial  |   [Issue 8834: PostgreSQL can't delete from several tables at the same time](sct-reference-MySQL-PostgreSQL-DML.md#sct-reference-8834)   | 
|  Multiple\-Table Syntax with USING  |  Partial  |   [Issue 8834: PostgreSQL can't delete from several tables at the same time](sct-reference-MySQL-PostgreSQL-DML.md#sct-reference-8834)   | 
|  ORDER BY  |  Yes  |   | 
|  QUICK  |  Partial  |   [Issue 8832: PostgreSQL doesn't have an option similar to QUICK for DML statements](sct-reference-MySQL-PostgreSQL-DML.md#sct-reference-8832)   | 

#### INSERT<a name="w3ab1c37c11b7b4b4"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  IGNORE  |  Partial  |   [Issue 8831: PostgreSQL doesn't have an option similar to IGNORE for DML statements](sct-reference-MySQL-PostgreSQL-DML.md#sct-reference-8831)   | 
|  LOW\_PRIORITY | DELAYED | HIGH\_PRIORITY  |  Partial  |   [Issue 8830: PostgreSQL doesn't have an option similar to LOW\_PRIORITY for DML statements](sct-reference-MySQL-PostgreSQL-DML.md#sct-reference-8830)   | 
|  ON DUPLICATE KEY UPDATE  |  No  |   [Issue 8829: PostgreSQL doesn't have an analog of clause ON DUPLICATE KEY UPDATE](sct-reference-MySQL-PostgreSQL-DML.md#sct-reference-8829)   | 
|  SELECT\-statement for insert  |  Yes  |   | 
|  SET col1=expr1,\.\.  |  Yes  |   | 
|  VALUES\(,…,\)|VALUE\(,…,\)  |  Yes  |   | 

#### SELECT<a name="w3ab1c37c11b7b4b6"></a>

##### <a name="w3ab1c37c11b7b4b6b2"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  DISTINCT   |  Yes  |   | 
|  GROUP BY ASC, DESC  |  Yes  |   | 
|  GROUP BY col\_name,…  |  Yes  |   | 
|  GROUP BY expression  |  Yes  |   | 
|  GROUP BY mixed options  |  Yes  |   | 
|  GROUP BY position,…  |  Yes  |   | 
|  GROUP BY WITH ROLLUP  |  No  |  [Issue 8653: PostgreSQL doesn't support the option GROUP BY ROLLUP](sct-reference-MySQL-PostgreSQL-SELECT.md#sct-reference-8653)  | 
|  HAVING  |  Yes  |   | 
|  HIGH\_PRIORITY  |  Partial  |  [Issue 8836: PostgreSQL doesn't have an option similar to %s for DML statements](sct-reference-MySQL-PostgreSQL-DML.md#sct-reference-8836)  | 
|  LIMIT offset, row\_count  |  Yes  |   | 
|  LIMIT row\_count OFFSET offset  |  Yes  |   | 
|  MAX\_STATEMENT\_TIME = N  |  Partial  |  [Issue 8836: PostgreSQL doesn't have an option similar to %s for DML statements](sct-reference-MySQL-PostgreSQL-DML.md#sct-reference-8836)  | 
|  ORDER BY col\_name,…  |  Yes  |   | 
|  ORDER BY expression  |  Yes  |   | 
|  ORDER BY mixed options  |  Yes  |   | 
|  ORDER BY position,…  |  Yes  |   | 
|  SQL\_BIG\_RESULT  |  Partial  |  [Issue 8836: PostgreSQL doesn't have an option similar to %s for DML statements](sct-reference-MySQL-PostgreSQL-DML.md#sct-reference-8836)  | 
|  SQL\_BUFFER\_RESULT  |  Partial  |  [Issue 8836: PostgreSQL doesn't have an option similar to %s for DML statements](sct-reference-MySQL-PostgreSQL-DML.md#sct-reference-8836)  | 
|  SQL\_CACHE   |  Partial  |  [Issue 8836: PostgreSQL doesn't have an option similar to %s for DML statements](sct-reference-MySQL-PostgreSQL-DML.md#sct-reference-8836)  | 
|  SQL\_CALC\_FOUND\_ROWS  |  Partial  |  [Issue 8836: PostgreSQL doesn't have an option similar to %s for DML statements](sct-reference-MySQL-PostgreSQL-DML.md#sct-reference-8836)  | 
|  SQL\_NO\_CACHE  |  Partial  |  [Issue 8836: PostgreSQL doesn't have an option similar to %s for DML statements](sct-reference-MySQL-PostgreSQL-DML.md#sct-reference-8836)  | 
|  SQL\_SMALL\_RESULT  |  Partial  |  [Issue 8836: PostgreSQL doesn't have an option similar to %s for DML statements](sct-reference-MySQL-PostgreSQL-DML.md#sct-reference-8836)  | 
|  STRAIGHT\_JOIN  |  Partial  |  [Issue 8836: PostgreSQL doesn't have an option similar to %s for DML statements](sct-reference-MySQL-PostgreSQL-DML.md#sct-reference-8836)  | 
|  Select all columns \(using \* and aliases\)  |  Yes  |   | 
|  Select all columns \(using \*\)  |  Yes  |   | 
|  Select subset of the columns  |  Yes  |   | 
|  Select with calculations  |  Yes  |   | 
|  Select with column heading  |  Yes  |   | 
|  Select with constants  |  Yes  |   | 
|  Subquery as scalar operand  |  Yes  |   | 

#### UPDATE<a name="w3ab1c37c11b7b4b8"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  DEFAULT VALUES  |  Yes  |   | 
|  IGNORE  |  Partial  |   [Issue 8831: PostgreSQL doesn't have an option similar to IGNORE for DML statements](sct-reference-MySQL-PostgreSQL-DML.md#sct-reference-8831)   | 
|  LIMIT  |  Yes  |   | 
|  LOW\_PRIORITY  |  Partial  |   [Issue 8830: PostgreSQL doesn't have an option similar to LOW\_PRIORITY for DML statements](sct-reference-MySQL-PostgreSQL-DML.md#sct-reference-8830)   | 
|  Multiple\-table syntax  |  Yes  |   | 
|  ORDER BY  |  Yes  |   | 

## Functions<a name="w3ab1c37c11b9"></a>

### Aggregate<a name="w3ab1c37c11b9b2"></a>

#### <a name="w3ab1c37c11b9b2b2"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  AVG\(\)  |  Yes  |   | 
|  BIT\_AND\(\)  |  Yes  |   | 
|  BIT\_OR\(\)  |  Yes  |   | 
|  BIT\_XOR\(\)  |  No  |   | 
|  COUNT\(\)  |  Yes  |   | 
|  COUNT\(DISTINCT\)  |  No  |   | 
|  GROUP\_CONCAT\(\)  |  Yes  |   | 
|  MAX\(\)  |  Yes  |   | 
|  MIN\(\)  |  Yes  |   | 
|  STD\(\)  |  Yes  |   | 
|  STDDEV\(\)  |  Yes  |   | 
|  STDDEV\_POP\(\)  |  Yes  |   | 
|  STDDEV\_SAMP\(\)  |  Yes  |   | 
|  SUM\(\)  |  Yes  |   | 
|  VAR\_POP\(\)  |  Yes  |   | 
|  VAR\_SAMP\(\)  |  Yes  |   | 
|  VARIANCE\(\)  |  Yes  |   | 

### Bit<a name="w3ab1c37c11b9b4"></a>

#### <a name="w3ab1c37c11b9b4b2"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  BIT\_COUNT\(\)  |  Yes  |   | 

### Control Flow<a name="w3ab1c37c11b9b6"></a>

#### <a name="w3ab1c37c11b9b6b2"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  CASE  |  Yes  |   | 
|  IF\(\)  |  Yes  |   | 
|  IFNULL\(\)  |  Yes  |   | 
|  NULLIF\(\)  |  Yes  |   | 

### Conversion<a name="w3ab1c37c11b9b8"></a>

#### <a name="w3ab1c37c11b9b8b2"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  BINARY  |  Yes  |   | 
|  CAST\(\)  |  Yes  |   | 
|  CONVERT\(\)  |  Yes  |   | 

### Date and Time<a name="w3ab1c37c11b9c10"></a>

#### <a name="w3ab1c37c11b9c10b2"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  ADDDATE\(\)  |  Yes  |   | 
|  ADDTIME\(\)  |  Yes  |   | 
|  CONVERT\_TZ\(\)  |  Yes  |   | 
|  CURDATE\(\)  |  Yes  |   | 
|  CURRENT\_DATE\(\), CURRENT\_DATE  |  Yes  |   | 
|  CURRENT\_TIME\(\), CURRENT\_TIME  |  Yes  |   | 
|  CURRENT\_TIMESTAMP\(\), CURRENT\_TIMESTAMP  |  Yes  |   | 
|  CURTIME\(\)  |  Yes  |   | 
|  DATE\(\)  |  Yes  |   | 
|  DATE\_ADD\(\)  |  Yes  |   | 
|  DATE\_FORMAT\(\)  |  Yes  |   | 
|  DATE\_SUB\(\)  |  Yes  |   | 
|  DATEDIFF\(\)  |  Yes  |   | 
|  DAY\(\)  |  Yes  |   | 
|  DAYNAME\(\)  |  Yes  |   | 
|  DAYOFMONTH\(\)  |  Yes  |   | 
|  DAYOFWEEK\(\)  |  Yes  |   | 
|  DAYOFYEAR\(\)  |  Yes  |   | 
|  EXTRACT\(\)  |  Yes  |   | 
|  FROM\_DAYS\(\)  |  Yes  |   | 
|  FROM\_UNIXTIME\(\)  |  Yes  |   | 
|  GET\_FORMAT\(\)  |  Yes  |   | 
|  HOUR\(\)  |  Yes  |   | 
|  LAST\_DAY  |  Yes  |   | 
|  LOCALTIME\(\), LOCALTIME  |  Yes  |   | 
|  LOCALTIMESTAMP, LOCALTIMESTAMP\(\)  |  Yes  |   | 
|  MAKEDATE\(\)  |  Yes  |   | 
|  MAKETIME\(\)  |  Yes  |   | 
|  MICROSECOND\(\)  |  Yes  |   | 
|  MINUTE\(\)  |  Yes  |   | 
|  MONTH\(\)  |  Yes  |   | 
|  MONTHNAME\(\)  |  Yes  |   | 
|  NOW\(\)  |  Yes  |   | 
|  PERIOD\_ADD\(\)  |  Yes  |   | 
|  PERIOD\_DIFF\(\)  |  Yes  |   | 
|  QUARTER\(\)  |  Yes  |   | 
|  SEC\_TO\_TIME\(\)  |  Yes  |   | 
|  SECOND\(\)  |  Yes  |   | 
|  STR\_TO\_DATE\(\)  |  Yes  |   | 
|  SUBDATE\(\)  |  Yes  |   | 
|  SUBTIME\(\)  |  Yes  |   | 
|  SYSDATE\(\)  |  No  |   | 
|  TIME\(\)  |  Yes  |   | 
|  TIME\_FORMAT\(\)  |  Yes  |   | 
|  TIME\_TO\_SEC\(\)  |  Yes  |   | 
|  TIMEDIFF\(\)  |  Yes  |   | 
|  TIMESTAMP\(\)  |  Yes  |   | 
|  TIMESTAMPADD\(\)  |  Yes  |   | 
|  TIMESTAMPDIFF\(\)  |  Yes  |   | 
|  TO\_DAYS\(\)  |  Yes  |   | 
|  TO\_SECONDS\(\)  |  Yes  |   | 
|  UNIX\_TIMESTAMP\(\)  |  Yes  |   | 
|  UTC\_DATE\(\)  |  Yes  |   | 
|  UTC\_TIME\(\)  |  Yes  |   | 
|  UTC\_TIMESTAMP\(\)  |  Yes  |   | 
|  WEEK\(\)  |  No  |   | 
|  WEEKDAY\(\)  |  Yes  |   | 
|  WEEKOFYEAR\(\)  |  Yes  |   | 
|  YEAR\(\)  |  Yes  |   | 
|  YEARWEEK\(\)  |  No  |   | 

### Encryption and Compression<a name="w3ab1c37c11b9c12"></a>

#### <a name="w3ab1c37c11b9c12b2"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  AES\_DECRYPT\(\)  |  No  |   | 
|  AES\_ENCRYPT\(\)  |  No  |   | 
|  COMPRESS\(\)  |  No  |   | 
|  DECODE\(\)  |  No  |   | 
|  DES\_DECRYPT\(\) \(deprecated 5\.7\.6\)  |  No  |   | 
|  DES\_ENCRYPT\(\) \(deprecated 5\.7\.6\)  |  No  |   | 
|  ENCODE\(\)  |  No  |   | 
|  ENCRYPT\(\) \(deprecated 5\.7\.6\)  |  No  |   | 
|  MD5\(\)  |  No  |   | 
|  OLD\_PASSWORD\(\)  |  No  |   | 
|  PASSWORD\(\) \(deprecated 5\.7\.6\)  |  No  |   | 
|  RANDOM\_BYTES\(\)  |  No  |   | 
|  SHA1\(\), SHA\(\)  |  No  |   | 
|  SHA2\(\)  |  No  |   | 
|  UNCOMPRESS\(\)  |  No  |   | 
|  UNCOMPRESSED\_LENGTH\(\)  |  No  |   | 
|  VALIDATE\_PASSWORD\_STRENGTH\(\)  |  No  |   | 

### Information<a name="w3ab1c37c11b9c14"></a>

#### <a name="w3ab1c37c11b9c14b2"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  BENCHMARK\(\)  |  No  |   | 
|  CHARSET\(\)  |  No  |   | 
|  COERCIBILITY\(\)  |  No  |   | 
|  COLLATION\(\)  |  No  |   | 
|  CONNECTION\_ID\(\)  |  No  |   | 
|  CURRENT\_USER\(\), CURRENT\_USER  |  No  |   | 
|  DATABASE\(\)  |  No  |   | 
|  FOUND\_ROWS\(\)  |  No  |   | 
|  LAST\_INSERT\_ID\(\)  |  No  |   | 
|  ROW\_COUNT\(\)  |  No  |   | 
|  SCHEMA\(\)  |  No  |   | 
|  SESSION\_USER\(\)  |  No  |   | 
|  SYSTEM\_USER\(\)  |  No  |   | 
|  USER\(\)  |  No  |   | 
|  VERSION\(\)  |  No  |   | 

### Mathematical<a name="w3ab1c37c11b9c16"></a>

#### <a name="w3ab1c37c11b9c16b2"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  ABS\(\)  |  Yes  |   | 
|  ACOS\(\)  |  Yes  |   | 
|  ASIN\(\)  |  Yes  |   | 
|  ATAN\(\)  |  Yes  |   | 
|  ATAN2\(\)  |  Yes  |   | 
|  CEIL\(\)  |  Yes  |   | 
|  CEILING\(\)  |  Yes  |   | 
|  CONV\(\)  |  No  |   [Issue 8811: PostgreSQL doesn't support the %s function](sct-reference-MySQL-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-8811)   | 
|  COS\(\)  |  Yes  |   | 
|  COT\(\)  |  Yes  |   | 
|  CRC32\(\)  |  Yes  |   | 
|  DEGREES\(\)  |  Yes  |   | 
|  EXP\(\)  |  Yes  |   | 
|  FLOOR\(\)  |  Yes  |   | 
|  LN\(\)  |  Yes  |   | 
|  LOG\(\)  |  Yes  |   | 
|  LOG10\(\)  |  Yes  |   | 
|  LOG2\(\)  |  Yes  |   | 
|  MOD\(\)  |  Yes  |   | 
|  PI\(\)  |  Yes  |   | 
|  POW\(\)  |  Yes  |   | 
|  POWER\(\)  |  Yes  |   | 
|  RADIANS\(\)  |  Yes  |   | 
|  RAND\(\)  |  Yes  |   | 
|  ROUND\(X\)  |  Yes  |   | 
|  SIGN\(\)  |  Yes  |   | 
|  SIN\(\)  |  Yes  |   | 
|  SQRT\(\)  |  Yes  |   | 
|  TAN\(\)  |  Yes  |   | 
|  TRUNCATE\(\)  |  Yes  |   | 

### String<a name="w3ab1c37c11b9c18"></a>

#### <a name="w3ab1c37c11b9c18b2"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  ASCII\(\)  |  Yes  |   | 
|  BIN\(\)  |  Yes  |   | 
|  BIT\_LENGTH\(\)  |  Yes  |   | 
|  CHAR\(\)  |  Yes  |   | 
|  CHAR\_LENGTH\(\)  |  Yes  |   | 
|  CHARACTER\_LENGTH\(\)  |  Yes  |   | 
|  CONCAT\(\)  |  No  |   | 
|  CONCAT\_WS\(\)  |  No  |   | 
|  ELT\(\)  |  Yes  |   | 
|  EXPORT\_SET\(\)  |  Yes  |   | 
|  FIELD\(\)  |  Yes  |   | 
|  FIND\_IN\_SET\(\)  |  Yes  |   | 
|  FORMAT\(\)  |  No  |   [Issue 8811: PostgreSQL doesn't support the %s function](sct-reference-MySQL-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-8811)   | 
|  FROM\_BASE64\(\)  |  No  |   [Issue 8811: PostgreSQL doesn't support the %s function](sct-reference-MySQL-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-8811)   | 
|  HEX\(\)  |  Yes  |   | 
|  INSERT\(\)  |  Yes  |   | 
|  INSTR\(\)  |  Yes  |   | 
|  LCASE\(\)  |  Yes  |   | 
|  LEFT\(\)  |  Yes  |   | 
|  LENGTH\(\)  |  Yes  |   | 
|  LIKE  |  Yes  |   | 
|  LOAD\_FILE\(\)  |  No  |   [Issue 8811: PostgreSQL doesn't support the %s function](sct-reference-MySQL-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-8811)   | 
|  LOCATE\(\)  |  Yes  |   | 
|  LOWER\(\)  |  Yes  |   | 
|  LPAD\(\)  |  Yes  |   | 
|  LTRIM\(\)  |  Yes  |   | 
|  MAKE\_SET\(\)  |  Yes  |   | 
|  MATCH  |  No  |   [Issue 8811: PostgreSQL doesn't support the %s function](sct-reference-MySQL-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-8811)   | 
|  MID\(\)  |  Yes  |   | 
|  NOT REGEXP  |  Yes  |   | 
|  NOT RLIKE  |  Yes  |   | 
|  OCT\(\)  |  Yes  |   | 
|  OCTET\_LENGTH\(\)  |  Yes  |   | 
|  ORD\(\)  |  Yes  |   | 
|  POSITION\(\)  |  Yes  |   | 
|  QUOTE\(\)  |  Yes  |   | 
|  REGEXP  |  Yes  |   | 
|  REPEAT\(\)  |  Yes  |   | 
|  REPLACE\(\)  |  Yes  |   | 
|  REVERSE\(\)  |  Yes  |   | 
|  RIGHT\(\)  |  Yes  |   | 
|  RLIKE  |  Yes  |   | 
|  RPAD\(\)  |  Yes  |   | 
|  RTRIM\(\)  |  No  |   | 
|  SOUNDEX\(\)  |  No  |   [Issue 8811: PostgreSQL doesn't support the %s function](sct-reference-MySQL-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-8811)   | 
|  SOUNDS LIKE  |  No  |   [Issue 8811: PostgreSQL doesn't support the %s function](sct-reference-MySQL-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-8811)   | 
|  SPACE\(\)  |  Yes  |   | 
|  STRCMP\(\)  |  Yes  |   | 
|  SUBSTR\(\)  |  Yes  |   | 
|  SUBSTRING\(\)  |  Yes  |   | 
|  SUBSTRING\_INDEX\(\)  |  Yes  |   | 
|  TO\_BASE64\(\)  |  No  |   [Issue 8811: PostgreSQL doesn't support the %s function](sct-reference-MySQL-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-8811)   | 
|  TRIM\(\)  |  Yes  |   | 
|  UCASE\(\)  |  Yes  |   | 
|  UNHEX\(\)  |  Yes  |   | 
|  UPPER\(\)  |  Yes  |   | 
|  WEIGHT\_STRING\(\)  |  No  |   [Issue 8811: PostgreSQL doesn't support the %s function](sct-reference-MySQL-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-8811)   | 

### XML<a name="w3ab1c37c11b9c20"></a>

#### <a name="w3ab1c37c11b9c20b2"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  ExtractValue\(\)  |  No  |   [Issue 8811: PostgreSQL doesn't support the %s function](sct-reference-MySQL-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-8811)   | 
|  UpdateXML\(\)  |  No  |   [Issue 8811: PostgreSQL doesn't support the %s function](sct-reference-MySQL-PostgreSQL-BUILT-INSQLFUNCTIONS.md#sct-reference-8811)   | 

## Data Types<a name="w3ab1c37c11c11"></a>

### Date and Time<a name="w3ab1c37c11c11b2"></a>


| Data type | Automatically Converted to | Details | 
| --- | --- | --- | 
|  DATE  |  date  |   | 
|  DATETIME  |  timestamp without time zone  |   | 
|  TIME  |  time  |   | 
|  TIMESTAMP  |  timestamp without time zone  |   | 
|  YEAR  |  smallint  |   | 
|  YEAR \(M\)  |  smallint  |   | 

### JSON<a name="w3ab1c37c11c11b4"></a>


| Data type | Automatically Converted to | Details | 
| --- | --- | --- | 
|  JSON  |  VARCHAR\(8000\)  |   [Issue 8706: PostgreSQL doesn't support %s type](sct-reference-MySQL-PostgreSQL-DATATYPES.md#sct-reference-8706)   | 

### Numeric<a name="w3ab1c37c11c11b6"></a>

#### Integer Types<a name="w3ab1c37c11c11b6b2"></a>


| Data type | Automatically Converted to | Details | 
| --- | --- | --- | 
|  BIGINT \[SIGNED\]  |  bigint  |   | 
|  BIGINT UNSIGNED  |  numeric  |   | 
|  BOOL  |  boolean  |   [Issue 8848: In MySQL the BOOLEAN type is a synonym for TINYINT](sct-reference-MySQL-PostgreSQL-DATATYPES.md#sct-reference-8848)   | 
|  BOOLEAN  |  boolean  |   [Issue 8848: In MySQL the BOOLEAN type is a synonym for TINYINT](sct-reference-MySQL-PostgreSQL-DATATYPES.md#sct-reference-8848)   | 
|  INT \[INTEGER\] \[SIGNED\]  |  integer  |   | 
|  INT \[INTEGER\] UNSIGNED  |  bigint  |   | 
|  MEDIUMINT \[SIGNED\]  |  integer  |   | 
|  MEDIUMINT UNSIGNED  |  integer  |   | 
|  SMALLINT \[SIGNED\]  |  smallint  |   | 
|  SMALLINT UNSIGNED  |  integer  |   | 
|  TINYINT \[SIGNED\]  |  smallint  |   | 
|  TINYINT UNSIGNED  |  smallint  |   | 

#### Bit<a name="w3ab1c37c11c11b6b4"></a>


| Data type | Automatically Converted to | Details | 
| --- | --- | --- | 
|  BIT  |  bit  |   | 

#### Fixed\-Point<a name="w3ab1c37c11c11b6b6"></a>


| Data type | Automatically Converted to | Details | 
| --- | --- | --- | 
|  DEC  |  numeric  |   | 
|  DEC \(p\)  |  numeric  |   | 
|  DEC \(p,s\)  |  numeric  |   | 
|  DECIMAL  |  numeric  |   | 
|  DECIMAL \(p\)  |  numeric  |   | 
|  DECIMAL \(p,s\)  |  numeric  |   | 
|  NUMERIC  |  numeric  |   | 
|  NUMERIC \(p\)  |  numeric  |   | 
|  NUMERIC \(p,s\)  |  numeric  |   | 

#### Floating\-Point<a name="w3ab1c37c11c11b6b8"></a>


| Data type | Automatically Converted to | Details | 
| --- | --- | --- | 
|  DOUBLE  |  double precision  |   | 
|  DOUBLE PRECISION   |  double precision  |   | 
|  DOUBLE PRECISION \(p\)  |  double precision  |   | 
|  DOUBLE PRECISION \(p,s\)  |  double precision  |   | 
|  DOUBLE\(p\)  |  double precision  |   | 
|  DOUBLE\(p,s\)   |  double precision  |   | 
|  FLOAT  |  real  |   | 
|  FLOAT\(p\)  |  precision from 1\-24: real precision > 24: double precision  |   | 
|  FLOAT\(p,s\)  |  double precision  |   | 
|  REAL  |  double precision  |   | 
|  REAL\(p\)  |  double precision  |   | 
|  REAL\(p,s\)  |  double precision  |   | 

### Spatial Data Types<a name="w3ab1c37c11c11b8"></a>

#### <a name="w3ab1c37c11c11b8b2"></a>


| Data type | Automatically Converted to | Details | 
| --- | --- | --- | 
|  GEOMETRY  |  VARCHAR\(8000\)  |   [Issue 8706: PostgreSQL doesn't support %s type](sct-reference-MySQL-PostgreSQL-DATATYPES.md#sct-reference-8706)   | 
|  GEOMETRYCOLLECTION  |  VARCHAR\(8000\)  |   [Issue 8706: PostgreSQL doesn't support %s type](sct-reference-MySQL-PostgreSQL-DATATYPES.md#sct-reference-8706)   | 
|  LINESTRING  |  VARCHAR\(8000\)  |   [Issue 8706: PostgreSQL doesn't support %s type](sct-reference-MySQL-PostgreSQL-DATATYPES.md#sct-reference-8706)   | 
|  MULTILINESTRING  |  VARCHAR\(8000\)  |   [Issue 8706: PostgreSQL doesn't support %s type](sct-reference-MySQL-PostgreSQL-DATATYPES.md#sct-reference-8706)   | 
|  MULTIPOINT  |  VARCHAR\(8000\)  |   [Issue 8706: PostgreSQL doesn't support %s type](sct-reference-MySQL-PostgreSQL-DATATYPES.md#sct-reference-8706)   | 
|  MULTIPOLYGON  |  VARCHAR\(8000\)  |   [Issue 8706: PostgreSQL doesn't support %s type](sct-reference-MySQL-PostgreSQL-DATATYPES.md#sct-reference-8706)   | 
|  POINT  |  VARCHAR\(8000\)  |   [Issue 8706: PostgreSQL doesn't support %s type](sct-reference-MySQL-PostgreSQL-DATATYPES.md#sct-reference-8706)   | 
|  POLYGON  |  VARCHAR\(8000\)  |   [Issue 8706: PostgreSQL doesn't support %s type](sct-reference-MySQL-PostgreSQL-DATATYPES.md#sct-reference-8706)   | 

### String<a name="w3ab1c37c11c11c10"></a>

#### <a name="w3ab1c37c11c11c10b2"></a>


| Data type | Automatically Converted to | Details | 
| --- | --- | --- | 
|  BINARY  |  bytea   |   [Issue 8706: PostgreSQL doesn't support %s type](sct-reference-MySQL-PostgreSQL-DATATYPES.md#sct-reference-8706)   | 
|  BLOB  |  bytea   |   [Issue 8706: PostgreSQL doesn't support %s type](sct-reference-MySQL-PostgreSQL-DATATYPES.md#sct-reference-8706)   | 
|  CHAR  |  char  |   | 
|  CHAR\(len\)  |  char  |   | 
|  ENUM  |  CREATE ENUM user type  |   | 
|  LONGBLOB  |  bytea   |   [Issue 8706: PostgreSQL doesn't support %s type](sct-reference-MySQL-PostgreSQL-DATATYPES.md#sct-reference-8706)   | 
|  LONGTEXT  |  text  |   | 
|  MEDIUMBLOB  |  bytea   |   [Issue 8706: PostgreSQL doesn't support %s type](sct-reference-MySQL-PostgreSQL-DATATYPES.md#sct-reference-8706)   | 
|  MEDIUMTEXT  |  text  |   | 
|  SET  | VARCHAR\(8000\) |   [Issue 8706: PostgreSQL doesn't support %s type](sct-reference-MySQL-PostgreSQL-DATATYPES.md#sct-reference-8706)   | 
|  TEXT  |  text  |   | 
|  TINYBLOB  |  bytea   |   [Issue 8706: PostgreSQL doesn't support %s type](sct-reference-MySQL-PostgreSQL-DATATYPES.md#sct-reference-8706)   | 
|  TINYTEXT  |  text  |   | 
|  VARBINARY\(len\)  |  bytea   |   [Issue 8706: PostgreSQL doesn't support %s type](sct-reference-MySQL-PostgreSQL-DATATYPES.md#sct-reference-8706)   | 
|  VARCHAR\(len\)  |  varchar  |   | 