# Conversion Issues with UPDATE<a name="sct-reference-Microsoft-SQL-Server-PostgreSQL-UPDATE"></a>

## Issue 7796: PostgreSQL doesn't support TOP option in the operator UPDATE<a name="sct-reference-7796"></a>

Perform a manual conversion for any UPDATE statements that contain a TOP argument, as in the example following\.

```
update top(10) 
	Account 
set
	AccountBalance = AccountBalance - 1
where
	AccountBalance > 15723
;
```

or:

```
update top(5) percent
	Account 
set
	AccountBalance = AccountBalance - 1
where
	AccountBalance > 15723
;
```

In PostgreSQL, you can use the row\_number\(\) [window function](http://www.postgresql.org/docs/9.5/static/functions-window.html) in the FROM clause or a subquery in the WHERE clause of the UPDATE statement to identify the rows you want to modify\.

## Issue 7797: PostgreSQL doesn't have analog for option "OUTPUT" with using the implicit table "deleted" in the operator for UPDATE<a name="sct-reference-7797"></a>

Perform a manual conversion for any UPDATE statements that uses the OUTPUT clause and references the deleted virtual table, as in the example following\.

```
update Customer set
	name = 'Mister ' + name
output 
	deleted.id, 
	deleted.name, 
	inserted.id, 
	inserted.name
where
	TypeID = 4
```

In PostgreSQL, use a subquery in the RETURNING clause to return the information about the deleted table\. This approach requires the table to have a primary key field\.

```
update mydb_dbo.Customer c set
	name = 'Mister ' || name
where
	TypeID = 4
returning
	 (select id from mydb_dbo.Customer where id = c.id)
	,(select name from mydb_dbo.Customer where id = c.id)
	,id 
	,name
```

If the primary key is composed of multiple fields, you must reference all of those fields in the subquery\. For example, take the following statement in SQL Server where id1 and id2 are the primary key fields for the TestMultiPK table\.

```
UPDATE [TestMultiPK] 
   SET [Description] = 'Test'
output 
  deleted.id1, 
  deleted.id2, 
  deleted.Description, 
  inserted.id1, 
  inserted.id2, 
  inserted.Description 
where ID = 0
```

The PostgreSQL conversion is as follows\.

```
UPDATE [TestMultiPK] t
   SET [Description] = 'Test'
WHERE ID = 0
returning
    select (id1 from TestMultiPK where id1 = t.id1 and id2 = t.id2)
  , select (id2 from TestMultiPK where id1 = t.id1 and id2 = t.id2)
  , select (Description from TestMultiPK where id1 = t.id1 and id2 = t.id2)
  , id1
  , id2
  , Description
```

## Issue 7829: Unable to convert variable assignment by UPDATE statement<a name="sct-reference-7829"></a>

Perform a manual conversion\. This issue occurs when you use an UPDATE statement to change the value of a variable, as in the example following\.

```
CREATE PROCEDURE [dbo].[PROC_DML_UPDATE_FROM_3]
AS
BEGIN
  DECLARE @AccountBalance FLOAT = 400;

  UPDATE bank
     SET @AccountBalance = 500
    FROM bank
   WHERE id = 50005;
END
```

## Related Topics<a name="sct-reference-Microsoft-SQL-Server-PostgreSQL-UPDATE-related"></a>

+  [Microsoft SQL Server to PostgreSQL Conversion Issue Reference](sct-reference-Microsoft-SQL-Server-PostgreSQL.md) 

+  [AWS Schema Conversion Tool Reference](CHAP_SchemaConversionTool.Reference.md) 

+  [What Is the AWS Schema Conversion Tool?](Welcome.md) 