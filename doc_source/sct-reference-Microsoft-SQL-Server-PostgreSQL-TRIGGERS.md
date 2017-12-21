# Conversion Issues with TRIGGERS<a name="sct-reference-Microsoft-SQL-Server-PostgreSQL-TRIGGERS"></a>

## Issue 7809: In PostgreSQL there are no analogues of the tables 'inserted' and 'deleted'<a name="sct-reference-7809"></a>

PostgreSQL doesn't support the inserted or deleted virtual tables\. To manually convert a trigger that uses these tables from Microsoft SQL Server to PostgreSQL, perform the following steps:

1. Create a trigger function\. The trigger function must be declared as a function taking no arguments and returning type trigger\. The returned value must be NEW, OLD or NULL, depending on the type of a trigger\. The function’s body must be PostgreSQL\-supported SQL to replace the body of the Microsoft SQL Server trigger without using the virtual tables\. The name of the function should be formed as **schema\_name\.fn\_<%trigger\_name%>\(\)**\.

1. Create a trigger with CREATE TRIGGER that executes the trigger function\.

For example, consider the following Microsoft SQL Server trigger\.

```
CREATE TRIGGER [dbo].[tr_customerStateExt_aiu]
   ON  [dbo].[CustomerStateExt]
AFTER INSERT, UPDATE
AS 
BEGIN
  IF EXISTS (SELECT *
               FROM inserted 
              WHERE LEN(Name) < 5)
  BEGIN
    RAISERROR ('The name must be longer than five characters.', 16, 1);
    ROLLBACK TRANSACTION;
    RETURN 
  END;
END
GO
```

Using the approach described, this trigger is converted into the following PostgreSQL trigger\.

```
CREATE OR REPLACE FUNCTION mydb_dbo.fn_tr_customerStateExt_aiu()
RETURNS trigger
AS
$BODY$
BEGIN
<SQL to write around use of the inserted and deleted virtual tables>
END;
$BODY$
LANGUAGE plpgsql;

CREATE TRIGGER tr_customerStateExt_aiu 
AFTER INSERT OR UPDATE 
ON mydb_dbo.CustomerStateExt
FOR EACH STATEMENT 
EXECUTE PROCEDURE mydb_dbo.fn_tr_customerStateExt_aiu();
```

## Related Topics<a name="sct-reference-Microsoft-SQL-Server-PostgreSQL-TRIGGERS-related"></a>

+  [Microsoft SQL Server to PostgreSQL Conversion Issue Reference](sct-reference-Microsoft-SQL-Server-PostgreSQL.md) 

+  [AWS Schema Conversion Tool Reference](CHAP_SchemaConversionTool.Reference.md) 

+  [What Is the AWS Schema Conversion Tool?](Welcome.md) 