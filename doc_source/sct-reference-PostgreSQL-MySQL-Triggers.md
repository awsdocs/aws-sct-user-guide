# Conversion Issues with Triggers<a name="sct-reference-PostgreSQL-MySQL-Triggers"></a>

## Issue 6083: MySQL doesn't support conditional triggers that fire on updates of particular column\(s\); a conversion will omit such a condition<a name="sct-reference-6083"></a>

MySQL doesn't support conditional triggers that rely on the update of a specific column\. For example, take the following statement in PostgreSQL\.

```
CREATE TRIGGER triggering_cond_bur_of
  BEFORE UPDATE OF n
```

This statement is converted to the following statement in MySQL:

```
CREATE TRIGGER triggering_cond_bur
  BEFORE UPDATE
```

If you require this functionality, perform a manual conversion instead\.

## Issue 6082: MySQL doesn't support constraint triggers<a name="sct-reference-6082"></a>

MySQL doesn't support constraint triggers, so any CREATE CONSTRAINT TRIGGER statements are converted to CREATE TRIGGER statements\. Review this code and modify it if necessary\.

## Issue 6087: MySQL doesn't support disabling triggers<a name="sct-reference-6087"></a>

PostgreSQL allows users to disable table triggers so that they aren't fired, and then re\-enable them at a later time\. MySQL doesn’t support this, so you must perform a manual conversion of this code\.

## Issue 6086: Unable to automatically transform dropping a trigger<a name="sct-reference-6086"></a>

DROP TRIGGER statements aren't automatically converted\. Perform a manual conversion instead\.

## Issue 6084: MySQL doesn't support INSTEAD OF triggers<a name="sct-reference-6084"></a>

Perform a manual conversion\.

## Issue 6085: MySQL doesn't support multiple triggers on the same event; triggers are merged into one in alphabetical order by trigger name<a name="sct-reference-6085"></a>

Multiple triggers on one event are automatically merged into a single trigger, with their functionality inserted into the new trigger in alphabetic order by trigger name\. Review this trigger code after conversion and revise it if necessary\. 

For example, take the following PostgreSQL code\.

```
CREATE TRIGGER triggering_multiple_inc
  BEFORE INSERT
  ON test_pg_mysql.triggering_multiple
  FOR EACH ROW
  EXECUTE PROCEDURE test_pg_mysql.fu_triggering_simple_inc();

CREATE TRIGGER triggering_multiple_inc_2
  BEFORE INSERT
  ON test_pg_mysql.triggering_multiple
  FOR EACH ROW
  EXECUTE PROCEDURE test_pg_mysql.fu_triggering_simple_inc();
```

This code is converted into the following MySQL code\.

```
CREATE TRIGGER triggering_multiple_bir
  BEFORE INSERT
  ON test_pg_mysql.triggering_multiple
  FOR EACH ROW
  BEGIN
    tr1: BEGIN
    -- triggering_multiple_inc
	SET NEW.n = NEW.n + 1;
    END tr1;
    
    tr2: BEGIN
    -- triggering_multiple_inc_2
    SET NEW.n = NEW.n + 1;
    END tr2;
  END;
```

## Issue 6081: MySQL doesn't support triggers firing on multiple events; such a trigger is converted to multiple single\-event triggers with the same body<a name="sct-reference-6081"></a>

PostgreSQL supports specifying multiple events with the CREATE TRIGGER statement, for example CREATE TRIGGER *trigger\_name* BEFORE INSERT OR UPDATE\. However, MySQL only supports specifying one event, for example CREATE TRIGGER *trigger\_name* BEFORE UPDATE\. PostgreSQL triggers that specify multiple events are converted to several triggers with the same trigger body, one for each event specified\. Review this trigger code after conversion and revise it if necessary\.

For example, take the following PostgreSQL code\.

```
CREATE TRIGGER
      triggering_simple_inc  BEFORE INSERT
        OR UPDATE   ON
        test_pg_mysql.triggering_simple  FOR EACH
        ROW  EXECUTE PROCEDURE
      test_pg_mysql.fu_triggering_simple_inc();
```

This code is converted into the following MySQL code:

```
CREATE TRIGGER triggering_simple_bir
  BEFORE INSERT
  ON test_pg_mysql.triggering_simple
  FOR EACH ROW
  BEGIN
    tr1: BEGIN
      SET NEW.n = NEW.n + 1;
    END tr1;
  END;

CREATE TRIGGER triggering_simple_bur
  BEFORE UPDATE
  ON test_pg_mysql.triggering_simple
  FOR EACH ROW
  BEGIN
    tr1: BEGIN
      SET NEW.n = NEW.n + 1;
    END tr1;
  END;
```

## Issue 6080: MySQL doesn't support statement\-level triggers<a name="sct-reference-6080"></a>

MySQL doesn't support the FOR EACH STATEMENT clause for CREATE TRIGGER statements\. Perform a manual conversion of this code\.

## Issue 6650: Unable to convert the statement with TG\_ARGV automatically<a name="sct-reference-6650"></a>

CREATE TRIGGER statements that use TG\_ARGV to work with trigger arguments can't be converted\. Perform a manual conversion instead\.

## Issue 6651: Unsupported using of RETURN statement in the trigger converted to LEAVE statement<a name="sct-reference-6651"></a>

Check flow of execution and perform a manual conversion if necessary\.

## Issue 6652: MySQL doesn't support OLD record in triggers on INSERT or NEW record in triggers on DELETE<a name="sct-reference-6652"></a>

MySQL doesn’t support the NEW variable in triggers that use DELETE, and it also doesn't support the OLD variable in triggers that use INSERT\. In these cases, the variable reference is replaced with NULL For example, `NEW.n > 0` is replaced by `NULL > 0`\. Review this code to see if using NULL instead of a field of the unsupported record is appropriate, and revise as necessary\.

## Issue 6088: MySQL doesn't support TRUNCATE event for triggers<a name="sct-reference-6088"></a>

Perform a manual conversion\.

## Related Topics<a name="w3ab1c37c17c11d169c27"></a>

+  [PostgreSQL to MySQL Conversion Reference](sct-reference-PostgreSQL-MySQL-overview.md) 

+  [AWS Schema Conversion Tool Reference](CHAP_SchemaConversionTool.Reference.md) 

+  [What Is the AWS Schema Conversion Tool?](Welcome.md) 