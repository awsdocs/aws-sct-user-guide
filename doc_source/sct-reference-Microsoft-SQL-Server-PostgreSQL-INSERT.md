# Conversion Issues with INSERT<a name="sct-reference-Microsoft-SQL-Server-PostgreSQL-INSERT"></a>

## Issue 7819: PostgreSQL doesn't support INSERT\.\.\.EXECUTE statements<a name="sct-reference-7819"></a>

Perform a manual conversion\. PostgreSQL doesn't support using EXECUTE within an INSERT statement to insert the results of a stored procedure into a table\.

## Issue 7799: PostgreSQL doesn't support TOP option in the operator INSERT<a name="sct-reference-7799"></a>

Perform a manual conversion for any INSERT statements that contain a TOP argument, as in the example following\.

```
insert TOP(2) percent into Customer(
	id
	,sname
	,name
	,typeid
	,taxcode
	,stateid
	,opendate
	,closedate
)select
	id+1000
	,name
	,name
	,4
	,61+id
	,1
	,getdate()
	,null
from
	employees e
where
	name not in(select name from Customer)
	and exists(select 1 from Employees where ManagerId = e.id)
```

In PostgreSQL, you can use the row\_number\(\) [window function](http://www.postgresql.org/docs/9.5/static/functions-window.html) in the FROM clause or a subquery in the WHERE clause of the SELECT statement you use to select the data to be inserted to identify the rows you want to insert\.

## Related Topics<a name="sct-reference-Microsoft-SQL-Server-PostgreSQL-INSERT-related"></a>

+  [Microsoft SQL Server to PostgreSQL Conversion Issue Reference](sct-reference-Microsoft-SQL-Server-PostgreSQL.md) 

+  [AWS Schema Conversion Tool Reference](CHAP_SchemaConversionTool.Reference.md) 

+  [What Is the AWS Schema Conversion Tool?](Welcome.md) 