# Conversion Issues with Arithmetic Operators<a name="sct-reference-Microsoft-SQL-Server-PostgreSQL-Arithmeticoperators"></a>

## Issue 7775: Check the data type conversion for possible loss of accuracy<a name="sct-reference-7775"></a>

To avoid loss of accuracy for types in arithmetic operations, cast values as the intended type, as in the example following\.

```
BEGIN
    SELECT
        5.1E+1::REAL
        INTO lBinaryFloat;
    SELECT
        - 5.2E-1::DOUBLE PRECISION
        INTO lBinaryDouble;

    var1 := (var_varchar1||var_varchar2)::INTEGER;
    var2 := (var_varchar1||var_varchar3)::NUMERIC;
    
    var3 := var_varchar1::NUMERIC + var_numeric2; 
    var4 := var_timestamp2 + (var_numeric1::NUMERIC || 'day')::INTERVAL; 
END;
```

## Issue 7773: Unable to perform an automated migration of arithmetic operations with dates<a name="sct-reference-7773"></a>

The Schema Conversion Tool cannot automatically migrate arithmetic operations that use date types\. Cast values as the intended type, as in the example following\.

```
BEGIN   
    var3 := var_varchar1::NUMERIC + var_numeric2; 
    var4 := var_timestamp2 + (var_numeric1::NUMERIC || 'day')::INTERVAL; 
END;
```

## Issue 7774: Unable to perform an automated migration of the arithmetic operations with mixed types of operands<a name="sct-reference-7774"></a>

The Schema Conversion Tool cannot automatically migrate arithmetic operations that mix types\. For example, multiplying a variable of type FLOAT with a variable of type INT\. Cast values as the intended type before performing any arithmetic operations, as in the example following\.

```
BEGIN
    var1 := (var_varchar1||var_varchar2)::INTEGER;
    var2 := (var_varchar1||var_varchar3)::NUMERIC;
END;
```

## Related Topics<a name="sct-reference-Microsoft-SQL-Server-PostgreSQL-Arithmeticoperators-related"></a>

+  [Microsoft SQL Server to PostgreSQL Conversion Issue Reference](sct-reference-Microsoft-SQL-Server-PostgreSQL.md) 

+  [AWS Schema Conversion Tool Reference](CHAP_SchemaConversionTool.Reference.md) 

+  [What Is the AWS Schema Conversion Tool?](Welcome.md) 