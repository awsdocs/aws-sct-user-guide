# Conversion Issues with Tables<a name="sct-reference-PostgreSQL-MySQL-Tables"></a>

## Issue 6111: MySQL doesn't support deferrable constraints<a name="sct-reference-6111"></a>

Check your schema and ensure that nondeferrable constraints can provide the necessary level of integrity\. Otherwise, perform a manual conversion on the constraints\.

## Issue 6112: MySQL doesn't support exclusion constraints<a name="sct-reference-6112"></a>

Perform a manual conversion of the exclusion constraint to provide the same level of data integrity\.

## Issue 6113: MySQL doesn't support check constraints; the source constraint is converted to a conditional error raising in triggers<a name="sct-reference-6113"></a>

In MySQL, check constraints are parsed but ignored\. Instead, PostgreSQL check constraints are converted to triggers that fire before INSERT and UPDATE events\. Review this code to see if it meets your needs, and if necessary perform a manual conversion of the check constraint to provide the expected level of data integrity\.

## Issue 6114: MySQL doesn't support SET DEFAULT as a referential action in foreign keys<a name="sct-reference-6114"></a>

MySQL doesn't support using SET DEFAULT when creating a foreign key\. Any SET DEFAULT statements are converted to SET NULL statements\. Review this code and modify it if necessary\.

## Issue 6115: MySQL doesn't support expressions in DEFAULT constraints, so they are converted to a BEFORE INSERT trigger<a name="sct-reference-6115"></a>

MySQL doesn’t support using expressions as default values when creating a table, so during conversion a BEFORE INSERT trigger is created to insert the default values instead\. CHARACTER VARYING columns are converted into TEXT or LONGTEXT columns \(depending on the length of the source column\), which can't have default values in MySQL\. Therefore, any default values in such columns are treated as expressions and are also included in the BEFORE INSERT trigger\.

For example, take the following PostgreSQL code\.

```
CREATE TABLE IF NOT EXISTS test_pg_mysql.constraint_default_expression
  ( n numeric( 10, 0 ) DEFAULT 12345+98765
  , d date DEFAULT now()
  , d2 date DEFAULT '2016-01-06'::date
  , s character varying (10) DEFAULT 'A string'
  );
```

This code is converted into the following MySQL code\.

```
CREATE TRIGGER constraint_default_expression_bir
  BEFORE INSERT 
  ON test_pg_mysql.constraint_default_expression
  FOR EACH ROW
  BEGIN
    default_values_expr: BEGIN
  -- default value for n column
      IF NEW.n IS NULL THEN
        SET NEW.n = 123456 + 98765;
      END IF;
      -- default value for d column
      IF NEW.d IS NULL THEN
        SET NEW.d = now( 6 );
      END IF;
      -- default value for d2 column
      IF NEW.d2 IS NULL THEN
        SET NEW.d2 = CAST( '2016-01-06' AS DATE );
      END IF;
      -- default value for s column
      IF NEW.s IS NULL THEN
        SET NEW.s = 'A string';
      END IF;
    END default_values_expr;
  END;
```

## Issue 6117: Unable to keep the NOT NULL constraint for %s column while converting its DEFAULT constraint based on an expression<a name="sct-reference-6117"></a>

MySQL doesn’t support using expressions as default values when creating a table, so during conversion a BEFORE INSERT trigger is created to insert the default values instead\. For more details, see [Issue 6115: MySQL doesn't support expressions in DEFAULT constraints, so they are converted to a BEFORE INSERT trigger](#sct-reference-6115)\.

If a column that has a default value and so is converted in this way also has a NOT NULL constraint, the NOT NULL constraint is converted as part of the same trigger rather than remaining as part of the CREATE TABLE statement\.

## Issue 6110: MySQL doesn't support tables without columns<a name="sct-reference-6110"></a>

MySQL doesn't support using the CREATE TABLE statement without specifying at least one column\. This usage is something you might do when creating a table based on a user\-defined type, for example\. Perform a manual conversion instead\.

## Issue 6107: MySQL doesn't support unlogged tables<a name="sct-reference-6107"></a>

Unlogged tables in PostgreSQL are converted to regular tables in MySQL\. Review this code to see if it meets your needs, and revise it if necessary\.

## Issue 6108: MySQL doesn't support inherited tables<a name="sct-reference-6108"></a>

Perform a manual conversion\.

## Issue 6109: MySQL doesn't support typed tables<a name="sct-reference-6109"></a>

Perform a manual conversion\.

## Related Topics<a name="w3ab1c37c17c11d167c23"></a>

+  [PostgreSQL to MySQL Conversion Reference](sct-reference-PostgreSQL-MySQL-overview.md) 

+  [AWS Schema Conversion Tool Reference](CHAP_SchemaConversionTool.Reference.md) 

+  [What Is the AWS Schema Conversion Tool?](Welcome.md) 