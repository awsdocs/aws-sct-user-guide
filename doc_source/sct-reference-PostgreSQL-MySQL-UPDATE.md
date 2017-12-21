# Conversion Issues with UPDATE<a name="sct-reference-PostgreSQL-MySQL-UPDATE"></a>

## Issue 6669: FROM clause was rewritten<a name="sct-reference-6669"></a>

The FROM clause in UPDATE statements is rewritten during PostgreSQL to MySQL conversion\. For example, take the following PostgreSQL statement\. 

```
update test_pg_mysql.customers c set id = c.id +1, name = o.name, 
      postcode = o.order_sum from test_pg_mysql.orders o where o.id = c.id;
```

This statement is converted to the following MySQL statement\.

```
update customers c 
      set id = c.id +1, 
      name = (select name from orders where id = c.id), 
      postcode = (select order_sum from orders where id = c.id)
      where c.id in (select id from orders);
```

Review this code to make sure it produces the results that you expect\.

## Issue 6066: MySQL doesn't support the UPDATE statement with the RETURNING option<a name="sct-reference-6066"></a>

To perform this operation, convert the UPDATE statement with the RETURNING clause into an UPDATE statement with following INSERT statements that have the specified key conditions in the SELECT clause\.

## Issue 6670: MySQL does not support update by cursor<a name="sct-reference-6670"></a>

MySQL doesn't support updating a table from within a cursor, as shown in the following example\.

```
DECLARE c1 CURSOR FOR SELECT id FROM test_pg_mysql.customers; 
	  val numeric(14,0);
	  BEGIN
	    OPEN c1;
	    fetch c1 into val;
	    update test_pg_mysql.customers set name = 'nfhr' where current of c1;
	    CLOSE c1;
        END
```

Perform a manual conversion instead\.

## Related Topics<a name="w3ab1c37c17c11d175b9"></a>

+  [PostgreSQL to MySQL Conversion Reference](sct-reference-PostgreSQL-MySQL-overview.md) 

+  [AWS Schema Conversion Tool Reference](CHAP_SchemaConversionTool.Reference.md) 

+  [What Is the AWS Schema Conversion Tool?](Welcome.md) 