# PostgreSQL to MySQL Supported Schema Conversion<a name="CHAP_SchemaConversionTool.Reference.ConversionSupport.PostgreSQL"></a>

The following sections list the schema elements from a PostgreSQL database and whether they are supported for automatic conversion to MySQL using the AWS Schema Conversion Tool\. 

## DDL<a name="w3ab1c37c17b5"></a>

### Statements<a name="w3ab1c37c17b5b2"></a>

#### Tables<a name="w3ab1c37c17b5b2b2"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  ALTER TABLE  |  Yes  |   | 
|  Auto\-incremented columns  |  Yes  |   | 
|  Columns with default values  |  Partial  |   [Issue 6115: MySQL doesn't support expressions in DEFAULT constraints, so they are converted to a BEFORE INSERT trigger](sct-reference-PostgreSQL-MySQL-Tables.md#sct-reference-6115)   | 
|  CREATE TABLE  |  Yes  |   | 
|  Deferrable constraints  |  Partial  |   [Issue 6111: MySQL doesn't support deferrable constraints](sct-reference-PostgreSQL-MySQL-Tables.md#sct-reference-6111)   | 
|  DROP TABLE  |  Yes  |   | 
|  Expression as default value for column  |  Partial  |   [Issue 6115: MySQL doesn't support expressions in DEFAULT constraints, so they are converted to a BEFORE INSERT trigger](sct-reference-PostgreSQL-MySQL-Tables.md#sct-reference-6115)   [Issue 6117: Unable to keep the NOT NULL constraint for %s column while converting its DEFAULT constraint based on an expression](sct-reference-PostgreSQL-MySQL-Tables.md#sct-reference-6117)   | 
|  Foreign keys  |  Partial  |   [Issue 6114: MySQL doesn't support SET DEFAULT as a referential action in foreign keys](sct-reference-PostgreSQL-MySQL-Tables.md#sct-reference-6114)   | 
|  Not\-null columns  |  Partial  |   [Issue 6117: Unable to keep the NOT NULL constraint for %s column while converting its DEFAULT constraint based on an expression](sct-reference-PostgreSQL-MySQL-Tables.md#sct-reference-6117)   | 
|  Primary keys  |  Yes  |   | 
|  Regular tables  |  Yes  |   | 
|  Table inheritance  |  No  |   [Issue 6108: MySQL doesn't support inherited tables](sct-reference-PostgreSQL-MySQL-Tables.md#sct-reference-6108)   | 
|  Tables with check constraints  |  Partial  |   [Issue 6113: MySQL doesn't support check constraints; the source constraint is converted to a conditional error raising in triggers](sct-reference-PostgreSQL-MySQL-Tables.md#sct-reference-6113)      | 
|  Tables with exclusion constraints  |  Partial  |   [Issue 6112: MySQL doesn't support exclusion constraints](sct-reference-PostgreSQL-MySQL-Tables.md#sct-reference-6112)   | 
|  Tables without columns  |  No  |   [Issue 6109: MySQL doesn't support typed tables](sct-reference-PostgreSQL-MySQL-Tables.md#sct-reference-6109)   | 
|  Trigger disablement  |  No  |   [Issue 6087: MySQL doesn't support disabling triggers](sct-reference-PostgreSQL-MySQL-Triggers.md#sct-reference-6087)   | 
|  Typed tables  |  No  |   [Issue 6110: MySQL doesn't support tables without columns](sct-reference-PostgreSQL-MySQL-Tables.md#sct-reference-6110)   [Issue 6120: MySQL doesn't support user\-defined data types](sct-reference-PostgreSQL-MySQL-UDT.md#sct-reference-6120)   | 
|  Unique keys  |  Yes  |   | 
|  Unlogged tables  |  No  |   [Issue 6107: MySQL doesn't support unlogged tables](sct-reference-PostgreSQL-MySQL-Tables.md#sct-reference-6107)   | 

## DML<a name="w3ab1c37c17b7"></a>

### Built\-In SQL Functions<a name="w3ab1c37c17b7b2"></a>

#### Aggregate<a name="w3ab1c37c17b7b2b2"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  All  |  Partial  |   [Issue 6667: MySQL doesn't support the %s function](sct-reference-PostgreSQL-MySQL-BUILT-INSQLFUNCTIONS.md#sct-reference-6667)   | 

#### Character<a name="w3ab1c37c17b7b2b4"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
| All |  Partial  |   [Issue 6667: MySQL doesn't support the %s function](sct-reference-PostgreSQL-MySQL-BUILT-INSQLFUNCTIONS.md#sct-reference-6667)   | 

#### Conversion<a name="w3ab1c37c17b7b2b6"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  All  |  Partial  |   [Issue 6667: MySQL doesn't support the %s function](sct-reference-PostgreSQL-MySQL-BUILT-INSQLFUNCTIONS.md#sct-reference-6667)   | 

#### DateTime<a name="w3ab1c37c17b7b2b8"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  All  |  Partial  |   [Issue 6667: MySQL doesn't support the %s function](sct-reference-PostgreSQL-MySQL-BUILT-INSQLFUNCTIONS.md#sct-reference-6667)   | 

#### Numeric<a name="w3ab1c37c17b7b2c10"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  All  |  Partial  |   [Issue 6667: MySQL doesn't support the %s function](sct-reference-PostgreSQL-MySQL-BUILT-INSQLFUNCTIONS.md#sct-reference-6667)   | 

#### Other<a name="w3ab1c37c17b7b2c12"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  All  |  Partial  |   [Issue 6667: MySQL doesn't support the %s function](sct-reference-PostgreSQL-MySQL-BUILT-INSQLFUNCTIONS.md#sct-reference-6667)   | 

#### Window<a name="w3ab1c37c17b7b2c14"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  All  |  No  |   [Issue 6667: MySQL doesn't support the %s function](sct-reference-PostgreSQL-MySQL-BUILT-INSQLFUNCTIONS.md#sct-reference-6667)   | 

#### XML<a name="w3ab1c37c17b7b2c16"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  All  |  No  |   [Issue 6667: MySQL doesn't support the %s function](sct-reference-PostgreSQL-MySQL-BUILT-INSQLFUNCTIONS.md#sct-reference-6667)   | 

### Joins<a name="w3ab1c37c17b7b4"></a>

#### TRUNCATE TABLE<a name="w3ab1c37c17b7b4b2"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  \[NATURAL \] \[ INNER \] JOIN  |  Yes  |   | 
|  \[NATURAL \] \{LEFT |RIGHT |FULL \} \[ OUTER \] JOIN  |  Yes  |   | 
|  CROSS JOIN  |  Yes  |   | 
|  USING \( join\_column \[, \.\.\.\] \)  |  Yes  |   | 

### Operators and Date Functions<a name="w3ab1c37c17b7b6"></a>

#### Bit String Operators<a name="w3ab1c37c17b7b6b2"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  ||,&,|,\#,\~,<<,>>,  |  Yes  |   | 

#### Date/Time Operators<a name="w3ab1c37c17b7b6b4"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|   \+,\-,\*,/   |  Partial  |   [Issue 6660: Unable to convert the %s operation with the interval value as one or more arguments](sct-reference-PostgreSQL-MySQL-OperatorsandDateFunctions.md#sct-reference-6660)   [Issue 6661: The operation will return the number of days instead of the interval value](sct-reference-PostgreSQL-MySQL-OperatorsandDateFunctions.md#sct-reference-6661)   | 

#### Mathematical Operators<a name="w3ab1c37c17b7b6b6"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  \+,\-,\*,/,%,^,|/,||/,\!,\!\!,@,&,|,\#,\~,<<,>>,  |  Yes  |   | 

#### String Operators<a name="w3ab1c37c17b7b6b8"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  ||  |  Yes  |   | 

### Predicates<a name="w3ab1c37c17b7b8"></a>

#### SIMILAR Predicate<a name="w3ab1c37c17b7b8b2"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
| SIMILAR |  No  |   [Issue 6607: Could not convert pattern to MySQL version; check pattern manually](sct-reference-PostgreSQL-MySQL-Patterns.md#sct-reference-6607)   | 

#### Boolean Conditions<a name="w3ab1c37c17b7b8b4"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  All  |  Yes  |   | 

#### Comparison Condition<a name="w3ab1c37c17b7b8b6"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  '=, <>, <, <=, >, >=  |  Yes  |   | 
|  ANY, SOME, ALL  |  Yes  |   | 

#### Exists Conditions<a name="w3ab1c37c17b7b8b8"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  EXISTS  |  Yes  |   | 

#### In Conditions<a name="w3ab1c37c17b7b8c10"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  IN  |  Yes  |   | 

#### Null Conditions<a name="w3ab1c37c17b7b8c12"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  NULL  |  Yes  |   | 

#### Pattern\-Matching Conditions<a name="w3ab1c37c17b7b8c14"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  All  |  Yes  |   | 

#### Range Conditions<a name="w3ab1c37c17b7b8c16"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  All  |  Yes  |   | 

### Set Operators<a name="w3ab1c37c17b7c10"></a>

#### Text Search Functions and Operators<a name="w3ab1c37c17b7c10b2"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  EXCEPT  |  Yes  |   | 
|  INTERSECT  |  Yes  |   | 
|  UNION  |  Yes  |   | 

### Statements<a name="w3ab1c37c17b7c12"></a>

#### INSERT<a name="w3ab1c37c17b7c12b2"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  INSERT INTO table DEFAULT VALUES;  |  Yes  |   | 
|  INSERT INTO table query;  |  Yes  |   | 
|  INSERT INTO table VALUES\(\) RETURNING \*;  |  No  |   [Issue 6172: MySQL doesn't support the INSERT statement with the RETURNING option](sct-reference-PostgreSQL-MySQL-INSERT.md#sct-reference-6172)   | 
|  INSERT INTO table VALUES\(\) RETURNING \{output\_expression \[ AS output\_name \] \[, \.\.\.\]\};  |  No  |   [Issue 6172: MySQL doesn't support the INSERT statement with the RETURNING option](sct-reference-PostgreSQL-MySQL-INSERT.md#sct-reference-6172)   | 
|  INSERT INTO table VALUES\(\);  |  Yes  |   | 
|  INSERT INTO table VALUES\(\{ expression | DEFAULT \} \[, \.\.\.\] \),VALUES\(\{ expression | DEFAULT \} \[, \.\.\.\] \) \[, \.\.\.\];  |  Yes  |   | 
|  INSERT INTO table VALUES\(\{ expression | DEFAULT \} \[, \.\.\.\] \);  |  Yes  |   | 
|  INSERT INTO table\(array\) VALUES\(\{'\{' '\}\[,\.\.\]'\}\);  |  Yes  |   | 
|  INSERT INTO table\[\( column \[, \.\.\.\] \)\] VALUES\(\);  |  Yes  |   | 
|  WITH RECURSIVE with\_query \[, \.\.\.\] UPDATE table\_name SET \{ column\_name = \{ expression | DEFAULT \}\} \[, \.\.\.\]  |  No  |   [Issue 6127: MySQL doesn't support the WITH RECURSIVE clause](sct-reference-PostgreSQL-MySQL-SELECT-UPDATE-INSERT-DELETE.md#sct-reference-6127)   | 
|  WITH with\_query \[, \.\.\.\] UPDATE table\_name SET \{ column\_name = \{ expression | DEFAULT \}\} \[, \.\.\.\]  |  Yes  |   | 

#### SELECT<a name="w3ab1c37c17b7c12b4"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  Add or subtract operators  |  Yes  |   | 
|  EXCEPT \[ALL\]  |  Partial  |   [Issue 6612: Query with INTERSECT/EXCEPT ALL operator was transformed](sct-reference-PostgreSQL-MySQL-INTERSECT-EXCEPT.md#sct-reference-6612)   | 
|  FROM \[ONLY\] tablename \[\*\]   |  No  |      | 
|  FROM \{ with\_query\_name | function\_name\(\)\}  |  No  |   [Issue 6603: Can't use function in from clause](sct-reference-PostgreSQL-MySQL-FROM.md#sct-reference-6603)   | 
|  FROM \{\(subquery\) \[ AS \] alias |\(VALUES\(\{ expression | DEFAULT \} \[, \.\.\.\]\)\) \[ AS \] alias \}  |  Yes  |   | 
|  FROM tablename \[ \[ AS \] alias \]  |  Yes  |   | 
|  GROUP BY  |  Yes  |   | 
|  HAVING  |  Yes  |   | 
|  INTERSECT \[ALL\]  |  Partial  |   [Issue 6612: Query with INTERSECT/EXCEPT ALL operator was transformed](sct-reference-PostgreSQL-MySQL-INTERSECT-EXCEPT.md#sct-reference-6612)   | 
|  LIMIT \{ count | ALL \} OFFSET start \{ ROW | ROWS \}  |  Partial  |   [Issue 6611: LIMIT/OFFSET option was omitted](sct-reference-PostgreSQL-MySQL-LIMIT.md#sct-reference-6611)   | 
|  OFFSET start \{ ROW | ROWS \} FETCH \{ FIRST | NEXT \} \[ count \] \{ ROW | ROWS \} ONLY  |  Partial  |   [Issue 6611: LIMIT/OFFSET option was omitted](sct-reference-PostgreSQL-MySQL-LIMIT.md#sct-reference-6611)   | 
|  ORDER BY \[ ASC | DESC | USING operator \] \[ NULLS \{ FIRST | LAST \} \] \[, \.\.\.\]  |  Yes  |   | 
|  SELECT \{\* | expression \[ \[ AS \] output\_name \] \[, \.\.\.\]\} FROM table  |  Yes  |   | 
|  SELECT \{expression \[ \[ AS \] output\_name \] \[, \.\.\.\]\}  |  Yes  |   | 
|  SELECT ALL  |  Yes  |   | 
|  SELECT DISTINCT   |  Yes  |   | 
|  SELECT DISTINCT ON  |  No  |      | 
|  UNION \[ALL\]  |  Yes  |   | 
|  WHERE \(field\_name1,…,fieldnameN\) IN \(subquery\_with\_multiple\_fields\)  |  Yes  |   | 
|  WHERE comparison\_condition \(=;<>;\!=;<;>;>=;<=;ANY;SOME;ALL\)  |  Yes  |   | 
|  WHERE compound\_condition\_with\_or\_and\_not  |  Yes  |   | 
|  WHERE field\_name BETWEEN arg1 AND arg2   |  Yes  |   | 
|  WHERE field\_name IN \(const1,\.\.\.,constN\)  |  Yes  |   | 
|  WHERE field\_name IN \(subquery\)  |  Yes  |   | 
|  WHERE like\_condition \(operator LIKE\)  |  Yes  |   | 
|  WITH RECURSIVE with\_query \[, \.\.\.\]  |  No  |   [Issue 6127: MySQL doesn't support the WITH RECURSIVE clause](sct-reference-PostgreSQL-MySQL-SELECT-UPDATE-INSERT-DELETE.md#sct-reference-6127)   | 
|  WITH with\_query \[, \.\.\.\]  |  Yes  |   | 

### WINDOW DEFINITION<a name="w3ab1c37c17b7c14"></a>

#### DELETE<a name="w3ab1c37c17b7c14b2"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  DELETE FROM table\_name WHERE CURRENT OF cursor\_name  |  No  |   [Issue 6672: MySQL does not support delete by cursor](sct-reference-PostgreSQL-MySQL-DELETE.md#sct-reference-6672)   | 
|  DELETE FROM table\_name FROM from\_list WHERE condition  |  Yes  |   | 
|  DELETE FROM table\_name RETURNING \{output\_expression \[ AS output\_name \] \[, \.\.\.\]\}  |  No  |   [Issue 6069: MySQL doesn't support the DELETE statement with the RETURNING option](sct-reference-PostgreSQL-MySQL-DELETE.md#sct-reference-6069)   | 
|  DELETE FROM table\_name RETURNING \*  |  No  |   [Issue 6069: MySQL doesn't support the DELETE statement with the RETURNING option](sct-reference-PostgreSQL-MySQL-DELETE.md#sct-reference-6069)   | 
|  DELETE FROM table\_name WHERE condition  |  Yes  |   | 
|  DELETE FROM ONLY table \[ \[ AS \] alias \]  |  No  |      | 
|  DELETE FROM table \[ \[ AS \] alias \]  |  Yes  |   | 
|  DELETE FROM table \* \[ \[ AS \] alias \]  |  No  |   [Issue 6603: Can't use function in from clause](sct-reference-PostgreSQL-MySQL-FROM.md#sct-reference-6603)   | 

#### SELECT<a name="w3ab1c37c17b7c14b4"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  \[ existing\_window\_name \] \[ PARTITION BY expression \[, \.\.\.\] \] \[ ORDER BY expression \[ ASC | DESC | USING operator \] \[ NULLS \{ FIRST | LAST \} \] \[, \.\.\.\] \] \[ frame\_clause \]  |  No  |   [Issue 6678: MySQL doesn't support function %s with OVER/ORDER BY/WITHIN GROUP/FILTER clause](sct-reference-PostgreSQL-MySQL-AGGREGATEFUNCTION.md#sct-reference-6678)   | 

#### UPDATE<a name="w3ab1c37c17b7c14b6"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  UPDATE ONLY table\_name SET \{ column\_name = \{ expression | DEFAULT \}\} \[, \.\.\.\]  |  No  |      | 
|  UPDATE table\_name \* SET \{ column\_name = \{ expression | DEFAULT \}\} \[, \.\.\.\]  |  No  |      | 
|  UPDATE table\_name \[ \[ AS \] alias \] SET \{ column\_name = \{ expression | DEFAULT \}\} \[, \.\.\.\]  |  Yes  |   | 
|  UPDATE table\_name SET \{ column\_name = \{ expression | DEFAULT \}\} \[, \.\.\.\]  |  Yes  |   | 
|  UPDATE table\_name SET \{ column\_name = \{ expression | DEFAULT \}\} \[, \.\.\.\] WHERE CURRENT OF cursor\_name  |  No  |   [Issue 6672: MySQL does not support delete by cursor](sct-reference-PostgreSQL-MySQL-DELETE.md#sct-reference-6672)   | 
|  UPDATE table\_name SET \{ column\_name = \{ expression | DEFAULT \}\} \[, \.\.\.\] FROM from\_list WHERE condition  |  Partial  |   [Issue 6669: FROM clause was rewritten](sct-reference-PostgreSQL-MySQL-UPDATE.md#sct-reference-6669)   | 
|  UPDATE table\_name SET \{ column\_name = \{ expression | DEFAULT \}\} \[, \.\.\.\] RETURNING \{output\_expression \[ AS output\_name \] \[, \.\.\.\]\}  |  No  |   [Issue 6066: MySQL doesn't support the UPDATE statement with the RETURNING option](sct-reference-PostgreSQL-MySQL-UPDATE.md#sct-reference-6066)   | 
|  UPDATE table\_name SET \{ column\_name = \{ expression | DEFAULT \}\} \[, \.\.\.\] RETURNING \*  |  No  |   [Issue 6066: MySQL doesn't support the UPDATE statement with the RETURNING option](sct-reference-PostgreSQL-MySQL-UPDATE.md#sct-reference-6066)   | 
|  UPDATE table\_name SET \{ column\_name = \{ expression | DEFAULT \}\} \[, \.\.\.\] WHERE condition  |  Yes  |   | 
|  UPDATE table\_name SET \{\( column\_name \[, \.\.\.\] \) = \( \{ expression | DEFAULT \} \[, \.\.\.\] \) \} \[, \.\.\.\]  |  Yes  |   | 
|  UPDATE table\_name SET \{\( column\_name \[, \.\.\.\] \) = \( query \) \}   |  Yes  |   | 
|  WITH RECURSIVE with\_query \[, \.\.\.\] UPDATE table\_name SET \{ column\_name = \{ expression | DEFAULT \}\} \[, \.\.\.\]  |  No  |   [Issue 6127: MySQL doesn't support the WITH RECURSIVE clause](sct-reference-PostgreSQL-MySQL-SELECT-UPDATE-INSERT-DELETE.md#sct-reference-6127)   | 
|  WITH with\_query \[, \.\.\.\] UPDATE table\_name SET \{ column\_name = \{ expression | DEFAULT \}\} \[, \.\.\.\]  |  Yes  |   | 

## PL/pgSQL<a name="w3ab1c37c17b9"></a>

### Basic Statements<a name="w3ab1c37c17b9b2"></a>

#### Assignment<a name="w3ab1c37c17b9b2b2"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  Variable assignment  |  Partial  |   [Issue 6668: MySQL doesn't support ROW/RECORD type](sct-reference-PostgreSQL-MySQL-ROW-RECORDtype.md#sct-reference-6668)   | 

#### Executing a Command with No Result<a name="w3ab1c37c17b9b2b4"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  PERFORM  |  Yes  |   | 

#### Executing a Query with a Single\-Row Result<a name="w3ab1c37c17b9b2b6"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  INTO  |  No  |   [Issue 6668: MySQL doesn't support ROW/RECORD type](sct-reference-PostgreSQL-MySQL-ROW-RECORDtype.md#sct-reference-6668)   | 

#### Executing Dynamic Commands<a name="w3ab1c37c17b9b2b8"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  EXECUTE, INTO, STRICT, USING  |  No  |   [Issue 6334: MySQL doesn't support the dynamic SQL statement RETURN QUERY EXECUTE](sct-reference-PostgreSQL-MySQL-DYNAMICSQL.md#sct-reference-6334)   | 

### Category<a name="w3ab1c37c17b9b4"></a>

#### Simple Structure of PL/pgSQL<a name="w3ab1c37c17b9b4b2"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  DECLARE, BEGIN, END  |  Yes  |   | 

### Conditionals<a name="w3ab1c37c17b9b6"></a>

#### IF\-THEN<a name="w3ab1c37c17b9b6b2"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  IF, THEN, END IF  |  Yes  |   | 

#### IF\-THEN\-ELSE<a name="w3ab1c37c17b9b6b4"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  IF, THEN, ELSE, END IF  |  Yes  |   | 

#### IF\-THEN\-ELSIF<a name="w3ab1c37c17b9b6b6"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  IF, THEN, ELSE, ELSIF, END IF  |  Yes  |   | 

#### Searched CASE<a name="w3ab1c37c17b9b6b8"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  CASE,WHEN, THEN, ELSE, END CASE  |  Yes  |   | 

#### Simple CASE<a name="w3ab1c37c17b9b6c10"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  CASE,WHEN, THEN, ELSE, END CASE  |  Yes  |   | 

### Cursors<a name="w3ab1c37c17b9b8"></a>

#### CLOSE<a name="w3ab1c37c17b9b8b2"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  CLOSE  |  Yes  |   | 

#### Declaring Cursor Variables<a name="w3ab1c37c17b9b8b4"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  NO, SCROLL, CURSOR, FOR  |  No  |   [Issue 6337: MySQL doesn't support a variable of REFCURSOR type](sct-reference-PostgreSQL-MySQL-CURSOR.md#sct-reference-6337)   | 

#### FETCH<a name="w3ab1c37c17b9b8b6"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  FETCH \[ direction \{ FROM | IN \} \] cursor INTO target;  |  Partial  |   [Issue 6639: MySQL doesn't support the direction clause](sct-reference-PostgreSQL-MySQL-CURSOR.md#sct-reference-6639)   | 

#### MOVE<a name="w3ab1c37c17b9b8b8"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  MOVE \[ direction \{ FROM | IN \} \] cursor;  |  No  |   [Issue 6640: MySQL doesn't support the MOVE option](sct-reference-PostgreSQL-MySQL-CURSOR.md#sct-reference-6640)   | 

#### OPEN FOR EXECUTE<a name="w3ab1c37c17b9b8c10"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  OPEN, NO, SCROLL, FOR, EXECUTE, USING  |  No  |   [Issue 6337: MySQL doesn't support a variable of REFCURSOR type](sct-reference-PostgreSQL-MySQL-CURSOR.md#sct-reference-6337)   | 

#### OPEN FOR Query<a name="w3ab1c37c17b9b8c12"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  OPEN, NO, SCROLL, FOR  |  No  |   [Issue 6638: MySQL doesn't support the SCROLL option in cursors](sct-reference-PostgreSQL-MySQL-CURSOR.md#sct-reference-6638)   | 

#### Opening a Bound Cursor<a name="w3ab1c37c17b9b8c14"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  OPEN bound\_cursorvar \[ \( \[ argument\_name := \] argument\_value \[, \.\.\.\] \) \];  |  Yes  |   | 

### Declarations<a name="w3ab1c37c17b9c10"></a>

#### ALIAS<a name="w3ab1c37c17b9c10b2"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  ALIAS FOR  |  Yes  |   | 

#### Collation of PL/pgSQL Variables<a name="w3ab1c37c17b9c10b4"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  COLLATE  |  No  |   [Issue 6343: MySQL doesn't support the COLLATE option; automatic conversion cannot be performed](sct-reference-PostgreSQL-MySQL-SQLFunctions.md#sct-reference-6343)   | 

#### Copying Types<a name="w3ab1c37c17b9c10b6"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  %TYPE, %ROWTYPE  |  Yes  |   | 

#### Declaring Function Parameters<a name="w3ab1c37c17b9c10b8"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  Declaring function parameters  |  Yes  |   | 

#### Record Types<a name="w3ab1c37c17b9c10c10"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  Record types  |  Yes  |   [Issue 6613: Unable to convert a function without OUT parameters returning a RECORD type](sct-reference-PostgreSQL-MySQL-FUNCTION.md#sct-reference-6613)   | 

#### Variable Declaration<a name="w3ab1c37c17b9c10c12"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  Variable declaration  |  Yes  |   | 

### Errors and Messages<a name="w3ab1c37c17b9c12"></a>

#### CLOSE<a name="w3ab1c37c17b9c12b2"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  RAISE ;  |  No  |   [Issue 6329: MySQL doesn't support the RAISE exception](sct-reference-PostgreSQL-MySQL-Errorhandling.md#sct-reference-6329)   | 
|  RAISE \[ level \] condition\_name \[ USING option = expression \[, \.\.\. \] \];  |  No  |   [Issue 6329: MySQL doesn't support the RAISE exception](sct-reference-PostgreSQL-MySQL-Errorhandling.md#sct-reference-6329)   | 
|  RAISE \[ level \] 'format' \[, expression \[, \.\.\. \]\] \[ USING option = expression \[, \.\.\. \] \];  |  Partial  |   [Issue 6332: MySQL doesn't support the RAISE statement to report messages](sct-reference-PostgreSQL-MySQL-Messagefromstoredroutines.md#sct-reference-6332)   | 
|  RAISE \[ level \] SQLSTATE 'sqlstate' \[ USING option = expression \[, \.\.\. \] \];  |  No  |   [Issue 6329: MySQL doesn't support the RAISE exception](sct-reference-PostgreSQL-MySQL-Errorhandling.md#sct-reference-6329)   | 
|  RAISE \[ level \] USING option = expression \[, \.\.\. \];  |  Partial  |   [Issue 6332: MySQL doesn't support the RAISE statement to report messages](sct-reference-PostgreSQL-MySQL-Messagefromstoredroutines.md#sct-reference-6332)   | 

#### Obtaining the Result Status<a name="w3ab1c37c17b9c12b4"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  GET \[ CURRENT \] DIAGNOSTICS variable = item \[ , \.\.\. \];  |  No  |   [Issue 6665: MySQL doesn't support the GET \[ CURRENT \] DIAGNOSTICS command](sct-reference-PostgreSQL-MySQL-Errorhandling.md#sct-reference-6665)   | 

#### Options<a name="w3ab1c37c17b9c12b6"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  EXCEPTION WHEN condition \[ OR condition \.\.\. \] THEN handler\_statements \[\.\.\] END;  |  Partial  |   [Issue 6664: MySQL doesn't support the condition information %s](sct-reference-PostgreSQL-MySQL-Errorhandling.md#sct-reference-6664)   | 
|  MESSAGE, DETAIL, HINT, ERRCODE,   |  No  |   [Issue 6332: MySQL doesn't support the RAISE statement to report messages](sct-reference-PostgreSQL-MySQL-Messagefromstoredroutines.md#sct-reference-6332)   | 

#### Result Status Parameters<a name="w3ab1c37c17b9c12b8"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  COLUMN\_NAME  |  Yes  |   | 
|  CONSTRAINT\_NAME  |  Yes  |   | 
|  MESSAGE\_TEXT  |  No  |   [Issue 6664: MySQL doesn't support the condition information %s](sct-reference-PostgreSQL-MySQL-Errorhandling.md#sct-reference-6664)   | 
|  PG\_DATATYPE\_NAME  |  No  |   [Issue 6664: MySQL doesn't support the condition information %s](sct-reference-PostgreSQL-MySQL-Errorhandling.md#sct-reference-6664)   | 
|  PG\_EXCEPTION\_CONTEXT  |  No  |   [Issue 6664: MySQL doesn't support the condition information %s](sct-reference-PostgreSQL-MySQL-Errorhandling.md#sct-reference-6664)   | 
|  PG\_EXCEPTION\_DETAIL  |  No  |   [Issue 6664: MySQL doesn't support the condition information %s](sct-reference-PostgreSQL-MySQL-Errorhandling.md#sct-reference-6664)   | 
|  PG\_EXCEPTION\_HINT  |  No  |   [Issue 6664: MySQL doesn't support the condition information %s](sct-reference-PostgreSQL-MySQL-Errorhandling.md#sct-reference-6664)   | 
|  RETURNED\_SQLSTATE  |  Yes  |   | 
|  SCHEMA\_NAME  |  No  |   [Issue 6664: MySQL doesn't support the condition information %s](sct-reference-PostgreSQL-MySQL-Errorhandling.md#sct-reference-6664)   | 
|  TABLE\_NAME  |  No  |   [Issue 6664: MySQL doesn't support the condition information %s](sct-reference-PostgreSQL-MySQL-Errorhandling.md#sct-reference-6664)   | 

### Loops<a name="w3ab1c37c17b9c14"></a>

#### CONTINUE<a name="w3ab1c37c17b9c14b2"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  CONTINUE, WHEN  |  Yes  |   | 

#### EXIT<a name="w3ab1c37c17b9c14b4"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  EXIT, WHEN  |  Yes  |   | 

#### FOR \(Integer Variant\)<a name="w3ab1c37c17b9c14b6"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  FOR, IN, LOOP, END LOOP, REVERSE, BY  |  Yes  |   | 

#### LOOP<a name="w3ab1c37c17b9c14b8"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  LOOP, END LOOP  |  Yes  |   | 

#### Looping Through Arrays<a name="w3ab1c37c17b9c14c10"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  FOREACH, IN, LOOP, END LOOP, SLICE, IN ARRAY  |  No  |   [Issue 6608: MySQL doesn't support arrays](sct-reference-PostgreSQL-MySQL-ARRAY.md#sct-reference-6608)   | 

#### Looping Through Query Results<a name="w3ab1c37c17b9c14c12"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  FOR, IN, LOOP, END LOOP, EXECUTE, USING  |  Yes  |   | 

#### WHILE<a name="w3ab1c37c17b9c14c14"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  WHILE, LOOP, END LOOP  |  Yes  |   | 

### RETURN Statement<a name="w3ab1c37c17b9c16"></a>

#### NULL; Command<a name="w3ab1c37c17b9c16b2"></a>


| Clause | Automatically Converted | Details | 
| --- | --- | --- | 
|  RETURN  |  Yes  |   | 
|  RETURN NEXT   |  No  |   [Issue 6604: MySQL doesn't support RETURN NEXT clause](sct-reference-PostgreSQL-MySQL-Functions.md#sct-reference-6604)   | 
|  RETURN QUERY  |  Yes  |   | 
|  RETURN QUERY EXECUTE  |  No  |   [Issue 6334: MySQL doesn't support the dynamic SQL statement RETURN QUERY EXECUTE](sct-reference-PostgreSQL-MySQL-DYNAMICSQL.md#sct-reference-6334)   | 