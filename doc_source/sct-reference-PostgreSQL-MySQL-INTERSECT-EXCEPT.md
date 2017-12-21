# Conversion Issues with INTERSECT, EXCEPT<a name="sct-reference-PostgreSQL-MySQL-INTERSECT-EXCEPT"></a>

## Issue 6612: Query with INTERSECT/EXCEPT ALL operator was transformed<a name="sct-reference-6612"></a>

The EXCEPT ALL and INTERSECT ALL options of the SELECT statement can't be directly converted, so they are converted to other language options that should produce the same results\. For example, take the following PostgreSQL statements\.

```
SELECT * FROM customers
except all
SELECT * FROM customers;

SELECT * FROM customers
intersect all
SELECT * FROM customers;
```

The preceding statements are converted to the following MySQL statements\.

```
SELECT customers.id, customers.name, customers.surname, customers.postcode FROM customers
where (customers.id, customers.name, customers.surname, customers.postcode) 
not in (SELECT customers.id, customers.name, customers.surname, customers.postcode FROM customers);

SELECT customers.id, customers.name, customers.surname, customers.postcode 
FROM customers inner join (SELECT customers.id, customers.name, customers.surname, customers.postcode FROM customers) nn 
on (customers.id=nn.id or (customers.id is null and nn.id is null))
  and customers.name=nn.name
  and (customers.surname=nn.surname or (customers.surname is null and nn.surname is null))
  and (customers.postcode=nn.postcode or (customers.postcode is null and nn.postcode is null));
```

Review the converted code, and revise it if necessary\.

## Related Topics<a name="w3ab1c37c17c11d133b5"></a>

+  [PostgreSQL to MySQL Conversion Reference](sct-reference-PostgreSQL-MySQL-overview.md) 

+  [AWS Schema Conversion Tool Reference](CHAP_SchemaConversionTool.Reference.md) 

+  [What Is the AWS Schema Conversion Tool?](Welcome.md) 